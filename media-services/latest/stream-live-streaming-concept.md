---
title: Overview of Live streaming
description: This article gives an overview of live streaming using Azure Media Services v3.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---
# Live streaming with Azure Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Azure Media Services enables you to deliver live events to your customers on the Azure cloud. To stream your live events with Media Services, you'll need to set up a live video encoder that converts signals from a camera (or another device, like a laptop) into a contribution feed that is sent to Media Services. The contribution feed can include signals related to advertising, such as SCTE-35 markers. For a list of recommended live streaming encoders, see [live streaming encoders](encode-recommended-on-premises-live-encoders.md).

If you haven't used an on-premises encoder before, try the [Create an Azure Media Services live stream with OBS](live-event-obs-quickstart.md) quickstart.

## Dynamic packaging and delivery

With Media Services, you can take advantage of [dynamic packaging](encode-dynamic-packaging-concept.md), which allows you to preview and broadcast your live streams in [MPEG DASH, HLS, and Smooth Streaming formats](https://en.wikipedia.org/wiki/Adaptive_bitrate_streaming) from the contribution feed. Your viewers can play back the live stream with any HLS, DASH, or Smooth Streaming compatible players. See the [list of tested players](player-media-players-concept.md) and try the [Media Services 3rd-party player samples](https://github.com/Azure-Samples/media-services-3rdparty-player-samples).

## Live event types

[Live events](/rest/api/media/liveevents) are ingest and process live video feeds. A live event can be set to either:

- *pass-through* when an on-premises live encoder sends a multiple bitrate stream, or
- *live encoding* when an on-premises live encoder sends a single bitrate stream. For details about live outputs, see [Live events and live outputs](live-event-concept.md).

### Pass-through

When using the pass-through **Live Event** (basic or standard), you rely on your on-premises live encoder to generate a multiple bitrate video stream and send that as the contribution feed to the Live Event (using RTMP or fragmented-MP4 input protocol). The Live Event then passes the incoming video stream to the dynamic packager (Streaming Endpoint) without any further processing. A pass-through Live Event is optimized for long-running live events or 24x365 linear live streaming.

:::image type="content" source="media/diagrams/pass-through.svg" alt-text="pass through streaming":::

### Live encoding

To use live encoding, configure your on-premises live encoder to send a single bitrate video (up to 32Mbps aggregate) to the Live Event (using RTMP or fragmented-MP4 input protocol). The Live Event transcodes the incoming single bitrate stream into multiple bitrate video streams at varying resolutions. This improves delivery for playback devices with industry standard protocols like MPEG-DASH, Apple HTTP Live Streaming (HLS), and Microsoft Smooth Streaming.

:::image type="content" source="media/diagrams/live-encoding.svg" alt-text="live encoding streaming":::

## Live event options

### Dynamic encryption

Dynamic encryption enables you to dynamically encrypt your live or on-demand content with AES-128 or any of the three major digital rights management (DRM) systems: Microsoft PlayReady, Google Widevine, and Apple FairPlay. Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses to authorized clients. For more information, see [dynamic encryption](drm-content-protection-concept.md).

Widevine is a service provided by Google Inc. and subject to the terms of service and Privacy Policy of Google, Inc.

### Dynamic filtering

Dynamic filtering is used to control the number of tracks, formats, bitrates, and presentation time windows that are sent out to the players. For more information, see [filters and dynamic manifests](filters-dynamic-manifest-concept.md).

### Live transcription

Live transcription is a feature you can use with live events that are either pass-through or live encoding. For more information, see [live transcription](live-event-live-transcription-how-to.md). When this feature is enabled, the service uses the [Speech-To-Text](/azure/cognitive-services/speech-service/speech-to-text) feature of Cognitive Services to transcribe the spoken words in the incoming audio into text. This text is then made available for delivery along with video and audio in MPEG-DASH and HLS protocols.

[!INCLUDE [live-transcription-gop-size](includes/live-transcription-gop-size.md)]

[!INCLUDE [Warning on captions and encryption](./includes/warning-captions-encryption.md)]

## Live streaming workflow

To understand the live streaming workflow in Media Services v3, you have to first review and understand the following concepts:

- [Streaming endpoints](stream-streaming-endpoint-concept.md)
- [Live events and live outputs](live-event-concept.md)
- [Streaming locators](stream-streaming-locators-concept.md)

### General steps

1. In your Media Services account, make sure the **streaming endpoint** (origin) is running.
2. Create a [live event](live-event-concept.md). <br/>When creating the event, you can specify to autostart it. Alternatively, you can start the event when you are ready to start streaming.<br/> When autostart is set to true, the Live Event will be started right after creation. The billing starts as soon as the Live Event starts running. You must explicitly call Stop on the live event resource to halt further billing. For more information, see [live event states and billing](live-event-states-billing-concept.md).
3. Get the ingest URL(s) and configure your on-premises encoder to use the URL to send the contribution feed.<br/>See [recommended live encoders](encode-recommended-on-premises-live-encoders.md).
4. Get the preview URL and use it to verify that the input from the encoder is actually being received.
5. Create a new **asset** object.

    Each live output is associated with an asset, which it uses to record the video into the associated Azure blob storage container.
6. Create a **live output** and use the asset name that you created so that the stream can be archived into the asset.

    Live Outputs start on creation and stop when deleted. When you delete the Live Output, you are not deleting the underlying asset and content in the asset.
7. Create a **streaming locator** with the [built-in streaming policy types](stream-streaming-policy-concept.md).

    To publish the live output, you must create a streaming locator for the associated asset.
8. List the paths on the **streaming locator** to get back the URLs to use (these are deterministic).
9. Get the hostname for the **streaming endpoint** (Origin) you wish to stream from.
10. Combine the URL from step 8 with the hostname in step 9 to get the full URL.
11. If you wish to stop making your **live event** viewable, you need to stop streaming the event and delete the **streaming locator**.
12. If you are done streaming events and want to clean up the resources provisioned earlier, follow the following procedure.

    * Stop pushing the stream from the encoder.
    * Stop the live event. Once the live event is stopped, it will not incur any charges. When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.
    * You can stop your streaming endpoint, unless you want to continue to provide the archive of your live event as an on-demand stream. If the live event is in stopped state, it will not incur any charges. However, if the streaming endpoint is still running, it will incur charges.

The asset that the live output is archiving to, automatically becomes an on-demand asset when the live output is deleted. You must delete all live outputs before a live event can be stopped. You can use an optional flag [removeOutputsOnStop](/rest/api/media/liveevents/stop#request-body) to automatically remove live outputs on stop.

> [!TIP]
> See [Live streaming tutorial](stream-live-tutorial-with-api.md), the article examines the code that implements the steps described above.

## Other important articles

- [Recommended live encoders](encode-recommended-on-premises-live-encoders.md)
- [Using a cloud DVR](live-event-cloud-dvr-time-how-to.md)
- [Live event types feature comparison](live-event-types-comparison-reference.md)
- [States and billing](live-event-states-billing-concept.md)
- [Latency](live-event-latency-reference.md)
- [Quotas and limits](limits-quotas-constraints-reference.md)

## Live streaming FAQ

See the [live streaming questions in the FAQ](frequently-asked-questions.yml).

[!INCLUDE [media-services-community](includes/media-services-community.md)]
