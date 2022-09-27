---
title: Use time-shifting to create live and on-demand video playback
description: This article describes how to use time-shifting and Live Outputs to record Live Streams and create on-demand playback.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 09/08/2022
ms.author: inhenkel
---

# Use time-shifting and Live Outputs to create on-demand video playback

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

In Azure Media Services, a [Live Output](/rest/api/media/liveoutputs) object is like a digital video recorder that will catch and record your live stream into an asset in your Media Services account. The recorded content is persisted into the container defined by the [Asset](/rest/api/media/assets) resource (the container is in the Azure Storage account attached to your account). The Live Output also allows you to control some properties of the outgoing live stream, like how much of the stream is kept in the archive recording (for example, the capacity of the cloud DVR) or when viewers can start watching the live stream. The archive on disk is a circular archive "window" that only holds the amount of content that's specified in the **archiveWindowLength** property of the Live Output. Content that falls outside of this window is automatically discarded from the storage container and isn't recoverable. The archiveWindowLength value represents an ISO-8601 timespan duration (for example, PTHH:MM:SS), which specifies the capacity of the DVR. The value can be set from a minimum of one minute to a maximum of 25 hours.

The relationship between a Live Event and its Live Outputs is similar to traditional TV broadcast, in that a channel (Live Event) represents a constant stream of video and a recording (Live Output) is scoped to a specific time segment (for example, evening news from 6:30PM to 7:00PM). Once you have the stream flowing into the Live Event, you can begin the streaming event by creating an asset, Live Output, and streaming locator. Live Output will archive the stream and make it available to viewers through the [Streaming Endpoint](/rest/api/media/streamingendpoints). You can create multiple Live Outputs (up to three maximum) on a Live Event with different archive lengths and settings. For information about the live streaming workflow, see the [general steps](stream-live-streaming-concept.md#general-steps) section.

## Using a DVR during an event

This section discusses how to use a DVR during an event to control what portions of the stream is available for ‘rewind’.

The `archiveWindowLength` value determines how far back in time a viewer can go from the current live position. The `archiveWindowLength` value also determines how long the client manifests can grow.

Suppose you're streaming a football game, and it has an `ArchiveWindowLength` of only 30 minutes. A viewer who starts watching your event 45 minutes after the game started can seek back to at most the 15-minute mark. Your Live Outputs for the game will continue until the Live Event is stopped. Content that falls outside of archiveWindowLength is continuously discarded from storage and is non-recoverable. In this example, the video between the start of the event and the 15-minute mark would have been purged from your DVR and from the container in blob storage for the asset. The archive isn't recoverable and is removed from the container in Azure blob storage.

A Live Event supports up to three concurrently running Live Outputs (you can create at most 3 recordings/archives from one live stream at the same time). This support allows you to publish and archive different parts of an event as needed. Suppose you need to broadcast a 24x7 live linear feed, and create "recordings" of the different programs throughout the day to offer to customers as on-demand content for catch-up viewing. For this scenario, you first create a primary Live Output with a short archive window of 1 hour or less–this is the primary live stream that your viewers would tune into. You would create a Streaming Locator for this Live Output and publish it to your app or web site as the "Live" feed. While the Live Event is running, you can programmatically create a second concurrent Live Output at the beginning of a program (or 5 minutes early to provide some handles to trim later). This second Live Output can be deleted 5 minutes after the program ends. With this second asset, you can create a new Streaming Locator to publish this program as an on-demand asset in your app's catalog. You can repeat this process multiple times for other program boundaries or highlights that you wish to share as on-demand videos, all while the "Live" feed from the first Live Output continues to broadcast the linear feed.

## Using rewindWindowLength

You can also use the `rewindWindowLength` property for a Live Output to control the amount of time a viewer can seek backward during a Live Event. The setting also helps to reduce the manifest size delivered to the client over the network during live streaming. It may result in a more efficient live streaming experience and reduce memory usage on the client. Once the Live Output stops, the archived video will use the original archive window length described above.

After the stream is complete, you can access the archived file in the asset defined by the **archiveWindowLength** property for the Live Output. This allows you to set a different archive duration from the previous "DVR sliding window" duration that is visible to the player.

This is very useful for when you want to stream with a very small time-shifting window in the player, but want to archive the entire live event to the output asset.

You can set **rewindWindowLength** to a minimum value of 60 seconds.

If you create a live event using LowLatencyV2, the default value is 30 minutes.

When you send a request for a Live Output, include *rewindWindowLength* in the properties. In the REST example below, PT1H30M is used to indicate 1 hour and 30 minutes of rewind window length.

```rest

{
  "properties": {
    "description": "test live output 1",
    "assetName": "6f3264f5-a189-48b4-a29a-a40f22575212",
    "archiveWindowLength": "PT5M",
    "rewindWindowLength": "PT1H30M",
    "manifestName": "testmanifest",
    "hls": {
      "fragmentsPerTsSegment": 5
    }
  }
```

## Creating an archive for on-demand playback

The Live Output asset automatically becomes an on-demand asset when the Live Output is deleted. You must delete all Live Outputs before a Live Event can be stopped. (You can use an optional flag [removeOutputsOnStop](/rest/api/media/liveevents/stop#request-body) to automatically remove Live Outputs on stop.) Users can stream your archived content on-demand, as long as you don't delete the asset.

> [!NOTE]
> When you delete the Live Output, you're not deleting the underlying asset and content in the asset.

If you've published the asset of your Live Output using a streaming locator, the Live Event (up to the DVR window length) will continue to be viewable until the streaming locator’s expiry or deletion, whichever comes first.

For more information, see:

- [Live streaming overview](stream-live-streaming-concept.md)
- [Live streaming tutorial](stream-live-tutorial-with-api.md)
