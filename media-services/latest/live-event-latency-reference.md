---
title: Live Event low latency settings in Azure Media Services
description: This article discusses low latency on a live event. It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 07/05/2022
ms.author: inhenkel
---

# Live event low latency settings

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article discusses the live event stream options that impact the end to end latency of a [live event](/rest/api/media/liveevents). This latency is often measured from the time a scene gets encoded on the contribution encoder to the time a media player displays it on screen for the viewer. It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.


## Standard or premium encoding live event stream options
For *encoding* live events, you can choose between *LowLatency* or *LowLatencyV2* stream options. The *LowLatencyV2* setting is the best option if you wish to go down to 3-7 seconds of end to end latency for your live stream. The supported output formats are DASH CMAF (format=mpd-time-cmaf) and Low Latency HLS (format=m3u8-cmaf). See [dynamic packaging](encode-dynamic-packaging-concept.md) page for streaming URL formats.

Choose the *LowLatency* stream option choose this option if you need Smooth Streaming output, or an archive length (DVR window) longer than 6 hours, or need Fairplay on Apple devices.

## Pass-through live event stream options
For *pass-through* live events, we recommend that you always use the *LowLatency* stream option. The *LowLatencyV2* setting is not available yet for pass-through live events.

## Additional recommendations

In addition to choosing the right stream option for your live event, these are the additional things you can tune to minimize the end to end latency.
For *passthrough* live events, use a key frame interval setting of 1 second on your encoding software.

We using HLS output, choose HLS CMAF (format=m3u8-cmaf) whenever possible. If you must use other streaming formats such as TS outputs with HLS v3 (format=aapl-m3u8-v3) and HLS v4 (format=aapl-m3u8-v4), be sure to set the `LiveOutput.Hls.fragmentsPerTsSegment` setting for your live event to 1 to ensure that Media Services packs only one mp4 fragment into one TS segment.

See the following table for latency numbers when used with the optimal settings and proper player configurations.

## Latency results
### Encoding live events with LowLatencyV2 option

| Format | Latency |
|---|---|
|**DASH**| 4-8 seconds|
|**LL-HLS**| 3-7 seconds|

### Encoding live events with LowLatency stream option

| Format |2 second GOP latency |1 second GOP latency |
|---|---|---|
|**DASH**|14 seconds |10 seconds|
|**HLS**|18 seconds |13 seconds|

### Pass-through live events with LowLatency stream option
| Format | 2 second GOP latency | 1 second GOP latency |
|---|---|---|
|**DASH**|10 seconds|8 seconds|
|**HLS**|14 seconds|10 seconds|

> [!NOTE]
> The end-to-end latency can vary depending on local network conditions or by introducing a CDN caching layer. You should test your exact configurations.

## Supported encryption formats

Media Services can currently only support the following encryption formats for live events with LowLatencyV2 stream option:

[!INCLUDE [low-latency-supported-encryption-types](includes/low-latency-supported-encryption-types.md)]

## Player settings

For all streams, you will need proper settings on your LL-HLS or DASH capable players to see the best latency numbers.

We have tested the LowLatencyV2 options (LL-HLS output) with the following media players:

- Video.js - Choose LL-HLS playback (format=m3u8-cmaf) for best results. Please use the LL-HLS support and buffer level ABR options.
- HLS.js - Choose LL-HLS (format=m3u8-cmaf) playback for best results.
- Shaka player - Use version 4.1.1 and above.
- Azure Media Player - use Low Latency Heuristic Profile. On Safari, it falls back to the native LL-HLS player.  On other platforms, it will choose to play DASH.
- ExoPlayer
- AVPlayer

## How-tos, tutorials and samples

- [Live Event with DVR - .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)
- [Low Latency - Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts)
- [Low Latency - Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event_Low_Latency/720p_low_latency_encoding_live_event.py)
