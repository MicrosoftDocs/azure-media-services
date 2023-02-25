---
title: Stream live with Media Services by using .NET 7.0
description: In Azure Media Services, live events are responsible for processing live streaming content. A live event provides an input endpoint (ingest URL) that you then provide to a live encoder. The live event receives input streams from the live encoder and makes them available for streaming through one or more streaming endpoints. Live events also provide a preview endpoint (preview URL) that you use to preview and validate your stream before further processing and delivery.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: tutorial
ms.date: 02/24/2023
ms.author: inhenkel
---

# Tutorial: Stream live with Media Services by using .NET 7.0**

In Azure Media Services, [live events](/rest/api/media/liveevents) are responsible for processing live streaming content. A live event provides an
input endpoint (ingest URL) that you then provide to a live encoder. The live event receives input streams from the live encoder using the RTMP/S or Smooth
Streaming protocols and makes them available for streaming through one or more [streaming endpoints](/rest/api/media/streamingendpoints). Live events also provide a preview endpoint (preview URL) that you use to preview and validate your stream before further processing and delivery.

This tutorial shows how to use .NET 7.0 to create a *pass-through* live event. Pass-through live events are useful when you have an encoder that is capable of multi-bitrate, GOP aligned encoding on premises. It can a way to reduce cloud costs. If you wish to reduce bandwidth and send a single bitrate stream to the cloud for multi-bitrate encoding, you can use a transcoding live event with the 720P or 1080P encoding presets.

In this tutorial, you will:

- Download a sample project.
- Examine the code that performs live streaming.
- Watch the event with Azure Media Player on the [Media Player demo site](https://ampdemo.azureedge.net/).
- Set up Event Grid to monitor the live event.
- Clean up resources.

## Prerequisites

You need the following items to complete the tutorial:

- Install [Visual Studio Code for Windows/macOS/Linux](https://code.visualstudio.com/) or [Visual Studio 2022 for Windows or Mac](https://visualstudio.microsoft.com/).
- Install [.NET 7.0 SDK](https://dotnet.microsoft.com/download)
- [Create a Media Services account](account-create-how-to.md). Be sure to copy the **API Access** details for the account name, subscription ID, and resource group name in JSON format or store the values needed to connect to the Media Services account in the JSON file format used in this `appsettings.json` file.
- Follow the steps in [Access the Azure Media Services API with the Azure CLI](access-api-howto.md) and save the details. You'll need to use the account name, subscription Id, and resource group name in this sample, and enter them into the `appsettings.json` file.

You also need these items for live-streaming software:

- A camera or a device (like a laptop) that's used to broadcast an event.
- An on-premises software encoder that encodes your camera stream and sends it to the Media Services live-streaming service through the Real-Time Messaging Protocol (RTMP/S). For more information, see [Recommended on-premises live encoders](encode-recommended-on-premises-live-encoders.md). The stream has to be in RTMP/S or Smooth Streaming format. This sample assumes that you'll use Open Broadcaster Software (OBS) Studio to broadcast RTMP/S to the ingest endpoint. [Install OBS Studio](https://obsproject.com/download).
- Alternatively, you can try the [OBS Quickstart](live-event-obs-quickstart.md) to test the entire process with the Azure portal first.

For monitoring the live event using Event Grid and Event Hubs, you can:
    1. Follow the steps in [Create and monitor Media Services events with Event Grid using the Azure portal](monitor-events-portal-how-to.md) or,
    1. Follow the steps near the end of this tutorial in the [Monitoring Live Events using Event Grid and Event Hubs](#monitoring-live-events-using-event-grid-and-event-hub) section of this article.

> [!TIP]
> Review [Live streaming with Media Services v3](stream-live-streaming-concept.md) before proceeding.

## Download and configure the sample

Clone the GitHub repository that contains the live-streaming .NET sample to your machine by using the following command:

```bash
git clone https://github.com/Azure-Samples/media-services-v3-dotnet.git
```

The live-streaming sample is in the [Live/LiveEventWithDVR](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Live/LiveEventWithDVR) folder.

Open `appsettings.json` in your downloaded project. Replace the values with account name, subscription Id and the resource group name.

> [!IMPORTANT]
> This sample uses a unique suffix for each resource. If you cancel the debugging or terminate the app without running it through, you'll end up with multiple live events in your account. Be sure to stop the running live events. Otherwise, *you'll be billed*!

## Start using Media Services APIs with the .NET SDK

Program.cs creates a reference to the Media Services account resource, using the options from `appsettings.json`:

```.NET
var mediaServicesResourceId = MediaServicesAccountResource.CreateResourceIdentifier(
    subscriptionId: options.AZURE_SUBSCRIPTION_ID.ToString(),
    resourceGroupName: options.AZURE_RESOURCE_GROUP,
    accountName: options.AZURE_MEDIA_SERVICES_ACCOUNT_NAME);
var credential = new DefaultAzureCredential(includeInteractiveCredentials: true);
var armClient = new ArmClient(credential);
var mediaServicesAccount = armClient.GetMediaServicesAccountResource(mediaServicesResourceId);
```

## Create a live event

This section shows how to create a *pass-through* type of live event (LiveEventEncodingType set to None). For information about the available types, see [Live event types](live-event-concept.md). If you want to reduce your overall ingest bandwidth, or you don't have an on-premises multi-bitrate transcoder, you can use a live transcoding event for 720p or 1080p adaptive bitrate cloud encoding.

You might want to specify the following things when you're creating the live event:

- **The ingest protocol for the live event**. Currently, the RTMPS, and Smooth Streaming protocols are supported. You can't change the protocol option while the live event is running. If you need different protocols, create a separate live event for each streaming protocol.
- **IP restrictions on the ingest and preview**. You can define the IP addresses that are allowed to ingest a video to this live event. Allowed IP addresses can be specified as one of these choices:
  - A single IP address (for example, 10.0.0.1 or 2001:db8::1)
  - An IP range that uses an IP address and a Classless Inter-Domain Routing (CIDR) subnet mask (for example, 10.0.0.1/22 or 2001:db8::/48)
  - An IP range that uses an IP address and a dotted decimal subnet mask (for example, 10.0.0.1 255.255.252.0)

    If no IP addresses are specified and there's no rule definition, then no IP address will be allowed. To allow any IP address, create a rule and set 0.0.0.0/0 and ::/0. The IP addresses have to be in one of the following formats: IPv4 or IPv6 addresses with four numbers or a CIDR address range. For more information, see [Restrict access to DRM license and AES key delivery using IP allowlists](drm-content-protection-key-delivery-ip-allow.md).

- **Autostart on an event as you create it**. When autostart is set to true, the live event will start after creation. That means the billing starts as soon as the live event starts running. You must explicitly call `Stop` on the live event resource to halt further billing. For more information, see [Live event states and billing](live-event-states-billing-concept.md).

    Standby modes are available to start the live event in a lower-cost "allocated" state that makes it faster to move to a running state. It's useful for situations like hot pools that need to hand out channels quickly to streamers.

- **A static host name and a unique GUID**. For an ingest URL to be predictive and easier to maintain in a hardware-based live encoder, set the `useStaticHostname` property to true. For detailed information, see [Live event ingest URLs](live-event-concept.md).

    <!-- REPLACE SAMPLE CODE: Use region name `CreateLiveEvent`.-->
    [!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateLiveEvent)]

## Get ingest URLs

After the Live Event is created, you can get ingest URLs that you'll provide to the live encoder. The encoder uses these URLs to input a live stream.

<!-- REPLACE IN SAMPLE CODE: Use region name `GetIngestUrl`.-->
[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#GetIngestURL)]

## Get the preview URL

Use `previewEndpoint` to preview and verify that the input from the encoder is being received.

> [!IMPORTANT]
> Make sure that the video is flowing to the preview URL before you continue.

<!-- REPLACE SAMPLE CODE: Use region name `GetPreviewUrls`. -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#GetPreviewURLs)]

## Create and manage live events and live outputs

After the live stream from the on-premises encoder is streaming to the live event, you can begin the live event by creating an asset, live output, and streaming locator. The stream is archived and is available to viewers through the streaming endpoint.

The next section will walk through the creation of the asset and the live output.

### Create an asset**

Create an asset for the live output to use.

<!-- REPACE SAMPLE CODE: Use region name “CreateAsset” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateAsset)]

### Create a live output

Live outputs start when they're created and stop when they're deleted. When you delete the live output, you're not deleting the output asset or content in the asset. The asset with the recording is available for on-demand streaming as long as it exists and there's a streaming locator associated with it.

<!-- REPACE SAMPLE CODE: Use region name “CreateLiveOutput” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateLiveOutput)]

## Create a streaming locator

> [!NOTE]
> When your Media Services account is created, a default streaming endpoint is added to your account in the stopped state. To start streaming your content and take advantage of [dynamic packaging](encode-dynamic-packaging-concept.md) and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the running state.

You publish an asset by creating a streaming locator. The live event (up to the DVR window length) is viewable until the streaming locator's expiration or deletion, whichever comes first. It's how you make the video available for your viewing audience to see live and on demand. The same URL can be used to watch the live event, the DVR window, or the on-demand asset when the live event is finished and the live output is deleted.

<!-- REPACE SAMPLE CODE: Use region name “CreateStreamingLocator” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateStreamingLocator)]

## Watch the event

Run the code. Use the output streaming URLs to watch your live event. Copy the streaming locator URL. You can use a media player of your choice. You can use the [Media Player demo site](https://ampdemo.azureedge.net/) to test your stream.  Enter the URL into the URL field and select **Update player**.

## Monitoring Live Events using Event Grid and Event Hubs

The sample project can use Event Grid and Event Hubs to monitor the Live Event. You can set up and use Event Grid using the following

To enable monitoring:

1. Use the Azure portal to create Event Hubs Namespace and an Event Hubs
    1. Search for “Event Hubs” using the text box at the top of the Azure portal.
    1. Select **Event Hub** from the list, then follow the instructions to create an Event Hubs Namespace.
    1. Navigate to the Event Hubs Namespace resource.
    1. Select **Event Hubs** from the **Entities** section of the portal menu.
    1. Create an Event Hubs in the Event Hubs namespace.
    1. Navigate to the Event Hubs resource.
    1. Select **Access control** then **Add**, then **Add role assignment**.
    1. Select the **Azure Event Hubs Data Receiver** then grant the access to yourself.
    1. Select **Access control** then **Add**, then **Add role assignment**.
    1. Select the **Azure Event Hubs Data Sender** then grant it to the Managed Identity created for the Media Services account.
1. Use the Azure portal to create an Azure Storage account.
    1. After creating the storage account, navigate to the Storage Account resource.
    1. Select **Access control** then **Add**, then **Add role assignment**.
    1. Select the **Storage Blob Data Contributor** then grant this access to yourself.
1. Create an Event Subscription
    1. Navigate to the Media Services account.
    1. Select **Events** from the portal menu.
    1. Select **+ Event Subscription**.
    1. Enter a subscription name and a system article name.
    1. Set the **Endpoint Type** to `Event Hub`.
    1. Set the Event Hubs to the previously created Event Hubs and set the Managed Identity to the identity that was previously granted Sender access to the Event Hubs
1. Update the `appsetttings.json` file.
    1. Set EVENT_HUB_NAMESPACE to the full name of the namespace. It should be similar to `myeventhub.servicebus.windows.net`.
    1. Set EVENT_HUB_NAME.
    1. Set AZURE_STORAGE_ACCOUNT_NAME.

Run the sample again. With Event Hubs integration enabled, the sample logs events when the encoder connects and disconnects from the Live Event. Various other events are also logged.

After running the sample, delete the Event Hubs and storage account if they're no longer needed.

## Clean up resources in your Media Services account

If you're done streaming events and want to clean up the resources provisioned earlier, use the following procedure:

1. Stop streaming from the encoder.
1. Stop the live event. After the live event is stopped, it won't incur any charges. When you need to start it again, the same ingest URL can be used so you won't need to reconfigure your encoder.
1. Stop the streaming endpoint, unless you want to continue to provide the archive of your live event as an on-demand stream. If the live event is in a stopped state, it won't incur any charges.

<!-- REPACE SAMPLE CODE: Use region name “Cleanup” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#Cleanup)]

## Clean up remaining resources

If you no longer need the Media Services and storage accounts that you created for this tutorial, delete the resource group that you created earlier.

Run the following CLI command:

```cli

az group delete --name amsResourceGroup

```

[!INCLUDE [media-services-community](includes/media-services-community.md)]
