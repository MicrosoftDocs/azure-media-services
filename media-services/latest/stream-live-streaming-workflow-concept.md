---
title: Media Services live streaming workflow
description: To understand the live streaming workflow in Media Services v3, you have to first review and understand the following concepts- Streaming endpoints, live events and live outputs, and streaming locators.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/02/2023
ms.author: inhenkel
---

# Media Services live streaming workflow

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Live streaming workflow

To understand the live streaming workflow in Media Services v3, first review the following concepts:

- [Streaming endpoints](stream-streaming-endpoint-concept.md)
- [Live events and live outputs](live-event-concept.md)
- [Streaming locators](stream-streaming-locators-concept.md)

> [!NOTE]
> This workflow doesn't describe live event encoding. For details on how to achieve low latency with live event encoding see the [Low Latency HLS (LL-HLS) and DASH streaming options](live-event-latency-reference.md) and the [Live streaming best practices guide](live-event-streaming-best-practices-guide.md). See also code sample listed on the [Live Streaming Samples](samples-live-streaming-reference.md) page.

### General steps

1. In your Media Services account, make sure the **streaming endpoint** (origin) is running.
2. Create a [live event](live-event-concept.md). <br/>When creating the event, you can specify to autostart it. Alternatively, you can start the event when you are ready to start streaming.<br/> When autostart is set to true, the Live Event will be started right after creation. The billing starts as soon as the Live Event starts running. You must explicitly call Stop on the live event resource to halt further billing. For more information, see [live event states and billing](live-event-states-billing-concept.md).
3. Get the ingest URL(s) and configure your on-premises encoder to use the URL to send the contribution feed.<br/>See [recommended on-premises live encoders](encode-recommended-on-premises-live-encoders.md).
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

## More information related to live streaming

- [Recommended live encoders](encode-recommended-on-premises-live-encoders.md)
- [Using a cloud DVR](live-event-cloud-dvr-time-how-to.md)
- [Live event types feature comparison](live-event-types-comparison-reference.md)
- [States and billing](live-event-states-billing-concept.md)
- [Latency](live-event-latency-reference.md)
- [Quotas and limits](limits-quotas-constraints-reference.md)

## Live streaming FAQ

See the [live streaming questions in the FAQ](frequently-asked-questions.yml).

[!INCLUDE [media-services-community](includes/media-services-community.md)]
