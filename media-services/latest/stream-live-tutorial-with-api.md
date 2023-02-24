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

In Azure Media Services, [live events](https://learn.microsoft.com/rest/api/media/liveevents) are responsible for processing live streaming content. A live event provides an
input endpoint (ingest URL) that you then provide to a live encoder. The live event receives input streams from the live encoder using the RTMP/S or Smooth
Streaming protocols and makes them available for streaming through one or more [streaming endpoints](https://learn.microsoft.com/rest/api/media/streamingendpoints). Live events also provide a preview endpoint (preview URL) that you use to preview and validate your stream before further processing and delivery.

This tutorial shows how to use .NET 7.0 to create a *pass-through* type of a live event. Pass-through type of live events are useful when you have an encoder that is capable of multi-bitrate, GOP aligned encoding, on premises and can be a simple way to reduce cloud costs. If you wish to reduce bandwidth and send a single bitrate stream to the cloud for multi-bitrate encoding, you can use a transcoding live event with the 720P or 1080P encoding presets.

In this tutorial, you will:

- Download a sample project.
- Examine the code that performs live streaming.
- Watch the event with [Azure Media Player](https://amp.azure.net/libs/amp/latest/docs/index.html) on the [Media Player demo site](https://ampdemo.azureedge.net/).
- Clean up resources.

> [!NOTE]
> Even though the tutorial uses **.NET SDK** examples, the general steps are the same for [REST API](https://learn.microsoft.com/en-us/rest/api/media/liveevents),
[CLI](https://learn.microsoft.com/en-us/cli/azure/ams/live-event), or other supported [SDKs](https://learn.microsoft.com/en-us/azure/media-services/latest/media-services-apis-overview#sdks).

## Prerequisites

You need the following items to complete the tutorial:

- Install [Visual Studio Code for Windows/macOS/Linux](https://code.visualstudio.com/) or [Visual Studio 2022 for Windows or Mac](https://visualstudio.microsoft.com/).
- Install [.NET 7.0 SDK](https://dotnet.microsoft.com/download)
- [Create a Media Services account](account-create-how-to.md). Be sure to copy the **API Access** details for the account name, subscription ID, and resource group name in JSON format or store the values needed to connect to the Media Services account in the JSON file format used in this `appsettings.json` file.
- Follow the steps in [Access the Azure Media Services API with the Azure CLI](access-api-howto.md) and save the details. You'll need to use the account name, subscription Id, and resource group name in this sample, and enter them into the `appsettings.json` file.

You need these additional items for live-streaming software:

- A camera or a device (like a laptop) that's used to broadcast an event.
- An on-premises software encoder that encodes your camera stream and sends it to the Media Services live-streaming service through the Real-Time Messaging Protocol (RTMP/S). For more information, see [Recommended on-premises live encoders](encode-recommended-on-premises-live-encoders.md). The stream has to be in RTMP/S or Smooth Streaming format. This sample assumes that you'll use Open Broadcaster Software (OBS) Studio to broadcast RTMP/S to the ingest endpoint. [Install OBS Studio](https://obsproject.com/download).

> [!TIP]
> Review [Live streaming with Media Services v3](stream-live-streaming-concept.md) before proceeding.

## Download and configure the sample

Clone the GitHub repository that contains the live-streaming .NET sample to your machine by using the following command:

```bash
git clone https://github.com/Azure-Samples/media-services-v3-dotnet.git
```

The live-streaming sample is in the [Live/LiveEventWithDVR](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Live/LiveEventWithDVR) folder.

Open `appsettings.json` in your downloaded project. Replace the values with account name, subscription Id and the resource group name that you got from [accessing APIs](access-api-howto.md).

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

This section shows how to create a *pass-through* type of live event (LiveEventEncodingType set to None). For information about the available types, see [Live event types](live-event-concept.md). In addition to pass-through, if you want to reduce your overall ingest bandwidth, or you do not have an appropriate multi-bitrate transcoder
on-premises, you can use a live transcoding event for 720p or 1080p adaptive bitrate cloud encoding.

You might want to specify the following things when you're creating the live event:

- **The ingest protocol for the live event**. Currently, the RTMPS, and Smooth Streaming protocols are supported. You can't change the protocol option while the live event is running. If you need different protocols, create a separate live event for each streaming protocol.
- **IP restrictions on the ingest and preview**. You can define the IP addresses that are allowed to ingest a video to this live event. Allowed IP addresses can be specified as one of these choices:
  - A single IP address (for example, 10.0.0.1 or 2001:db8::1)
  - An IP range that uses an IP address and a Classless Inter-Domain Routing (CIDR) subnet mask (for example, 10.0.0.1/22 or 2001:db8::/48)
  - An IP range that uses an IP address and a dotted decimal subnet mask (for example, 10.0.0.1 255.255.252.0)

    If no IP addresses are specified and there's no rule definition, then no IP address will be allowed. To allow any IP address, create a rule and set 0.0.0.0/0 and ::/0. The IP addresses have to be in one of the following formats: IPv4 or IPv6 addresses with four numbers or a CIDR address range. For more information about using IPv4 or IPv6 see [Restrict access to DRM license and AES key delivery using IP allowlists](drm-content-protection-key-delivery-ip-allow.md).

- **Autostart on an event as you create it**. When autostart is set to true, the live event will start after creation. That means the billing starts as soon as the live event starts running. You must explicitly call Stop on the live event resource to halt further billing. For more information, see [Live event states and billing](live-event-states-billing-concept.md).

    Standby modes are available to start the live event in a lower-cost "allocated" state that makes it faster to move to a running state. This is useful for situations like hot pools that need to hand out channels quickly to streamers.

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

After you have the stream flowing into the live event, you can begin the streaming event by creating an asset, live output, and streaming locator. This
will archive the stream and make it available to viewers through the streaming endpoint.

The next section will walk through the creation of the asset and the live output.

### Create an asset**

Create an asset for the live output to use. In our analogy, this will be the "tape" that we record the live video signal onto. Viewers will be able to see
the contents live or on demand from this virtual tape.

<!-- REPACE SAMPLE CODE: Use region name “CreateAsset” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateAsset)]

**Create a live output**

Live outputs start when they're created and stop when they're deleted. When you delete the live output, you're not deleting the underlying asset or content in the asset. Think of it as ejecting the "tape." The asset with the recording will last as long as you like. When it's ejected (meaning, when the live output is deleted), it will be available for on-demand viewing immediately.

<!-- REPACE SAMPLE CODE: Use region name “CreateLiveOutput” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateLiveOutput)]

## Create a streaming locator

> [!NOTE]
> When your Media Services account is created, a default streaming endpoint is added to your account in the stopped state. To start streaming your content and take advantage of [dynamic packaging](https://learn.microsoft.com/en-us/azure/media-services/latest/encode-dynamic-packaging-concept) and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the running state.

When you publish the asset by using a streaming locator, the live event (up to the DVR window length) will continue to be viewable until the streaming locator's expiration or deletion, whichever comes first. This is how you make the virtual "tape" recording available for your viewing audience to see live and on demand. The same URL can be used to watch the live event, the DVR window, or the on-demand asset when the recording is complete (when the live output is deleted).

<!-- REPACE SAMPLE CODE: Use region name “CreateStreamingLocator” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#CreateStreamingLocator)]

## Watch the event

Press **Ctrl+F5** to run the code. This will output streaming URLs that you can use to watch your live event. Copy the streaming URL that you got to create a
streaming locator. You can use a media player of your choice. [Azure Media Player](https://amp.azure.net/libs/amp/latest/docs/index.html) is available to
test your stream at the [Media Player demo site](https://ampdemo.azureedge.net/).

A live event automatically converts events to on-demand content when it's stopped. Even after you stop and delete the event, users can stream your archived content as a video on demand for as long as you don't delete the asset. An asset can't be deleted if an event is using it; the event must be deleted first.

## Monitoring Live Events using Event Grid and Event Hub

The sample project can use Event Grid and Event Hub to monitor the Live Event. To enable monitoring:

1. Use the Azure Portal to create Event Hub Namespace and an Event Hub
    1. Search for “Event Hub” using the text box at the top of the Azure Portal.
    1. Select **Event Hub** from the list, then follow the instructions to create an Event Hub Namespace.
    1. Navigate to the Event Hub Namespace resource.
    1. Select **Event Hubs** from the **Entities** section of the portal menu.
    1. Create an Event Hub in the Event Hub namespace.
    1. Navigate to the Event Hub resource.
    1. Select **Access control** then **Add**, then **Add role assignment**.
    1. Select the **Azure Event Hubs Data Receiver** then grant this access to yourself.
    1. Select **Access control** then **Add**, then **Add role assignment**.
    1. Select the **Azure Event Hubs Data Sender** then grant this to the Managed Identity created for the Media Services account.
1. Use the Azure Portal to create an Azure Storage account.
    1. After creating the storage account, navigate to the Storage Account resource.
    1. Select **Access control** then **Add**, then **Add role assignment**.
    1. Select the **Storage Blob Data Contributor** then grant this access to yourself.
1. Create an Event Subscription
    1. Navigate to the Media Services account.
    1. Select **Events** from the portal menu.
    1. Select **+ Event Subscription**.
    1. Enter a subscription name and a system topic name.
    1. Set the **Endpoint Type** to `Event Hub`.
    1. Set the Event Hub to the previously created Event Hub and set the Managed Identity to the identity that was previously granted Sender access to the Event Hub
1. Update the `appsetttings.json` file.
    1. Set EVENT_HUB_NAMESPACE to the full name of the namespace. It should be similar to `myeventhub.servicebus.windows.net`.
    1. Set EVENT_HUB_NAME.
    1. Set AZURE_STORAGE_ACCOUNT_NAME.

Run the sample again. With Event Hub integration enabled, the sample will log events when the encoder connects and disconnects from the Live Event. Events
will also be logged for various other events.

After running the sample, delete the Event Hub and storage account if they are no longer needed.

## Clean up resources in your Media Services account

If you're done streaming events and want to clean up the resources provisioned earlier, use the following procedure:

1. Stop streaming from the encoder.
1. Stop the live event. After the live event is stopped, it won't incur any charges. When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.
1. Stop the streaming endpoint, unless you want to continue to provide the archive of your live event as an on-demand stream. If the live event is in a stopped state, it won't incur any charges.

<!-- REPACE SAMPLE CODE: Use region name “Cleanup” -->

[!code-csharp[Main](~/../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#Cleanup)]

## Clean up remaining resources

If you no longer need any of the resources in your resource group, including the Media Services and storage accounts that you created for this tutorial, delete
the resource group that you created earlier.

Run the following CLI command:

```cli

az group delete --name amsResourceGroup

```

[!INCLUDE [media-services-community](includes/media-services-community.md)]
