---
title: Live Event low latency settings in Azure Media Services
description: This article discusses low latency on a live event. It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 07/05/2022
ms.author: inhenkel
---

# Live Event low latency settings

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article discusses low latency on a [live event](/rest/api/media/liveevents). It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.

For *pass-through* live events, we recommend that you always use the *LowLatency* stream option.

For *encoding* live events, you can choose between *LowLatency* or *LowLatencyV2* stream options. The *LowLatencyV2* setting is the best option if you wish to go down to 3-7 seconds of end to end latency for your live stream. The supported output formats are DASH CMAF (format=mpd-time-cmaf) or Low Latency HLS (format=m3u8-cmaf). See [dynamic packaging](encode-dynamic-packaging-concept.md) page for streaming URL formats.

## When to choose the LowLatency option

The *LowLatencyV2* option is currently only available for encoding live events. Choose the *LowLatency* stream option if you are using *passthrough* live events. For encoding live events, choose this option if you need Smooth Streaming output, or an archive length (DVR window) longer than 6 hours, or need Fairplay on Apple devices.

## Live Events latency

Latency is measured between the time the video is encoded on your encoding software, to the time when your viewers can view the content on a player. Many parts contribute to this latency. Add together the time the video spends being encoded and buffered in your encoder, the time it spends in Media Services, and the time it spends enroute via the streaming endpoint and CDN, to the buffering time the video player requires. You can control the encoder settings and the player settings.

For the lowest latency possible with a *passthrough* live event, use a key frame interval setting of 1 second on your encoding software and the *LowLatency* streaming option.

For the lowest latency possible with an encoding live event, use the *LowLatencyV2* streaming option and choose HLS CMAF (format=m3u8-cmaf) output. We support delivery in Low Latency HLS.

If you must use other streaming formats such as TS outputs with HLS v3 (format=aapl-m3u8-v3) and HLS v4 (format=aapl-m3u8-v4), be sure to set the LiveOutput.Hls.fragmentsPerTsSegment setting for your live event to 1 to ensure that Media Services packs only one mp4 fragment into one TS segment.

See the following table for latency numbers when used with the optimal settings and proper player configurations.

### Pass-through with LowLatency stream option

| Format | 2 second GOP latency | 1 second GOP latency |
|---|---|---|
|**DASH in AMP**|10 seconds|8 seconds|
|**HLS on native iOS player**|14 seconds|10 seconds|

### Live encoding with LowLatency stream option

| Format |2 second GOP latency |1 second GOP latency |
|---|---|---|
|**DASH in AMP**|14 seconds |10 seconds|
|**HLS on native iOS player**|18 seconds |13 seconds|

### Live encoding with LowLatencyV2 option

GOP size doesn't affect latency with the LowLatencyV2 option.

| Format | Latency |
|---|---|
|**DASH in AMP**| 4-8 seconds|
|**HLS on native iOS player**| 3-7 seconds|

> [!NOTE]
> The end-to-end latency can vary depending on local network conditions or by introducing a CDN caching layer. You should test your exact configurations.

## Supported encryption formats

Media Services can currently only support the following encryption formats for live events with LowLatencyV2 stream option:

[!INCLUDE [low-latency-supported-encryption-types](includes/low-latency-supported-encryption-types.md)]

## Player settings

For all streams, you will need proper settings on your LL-HLS or DASH capable players to see the best latency numbers.

We have tested the LowLatencyV2 options with the following media players:

- Video.js - Choose CMAF LL-HLS playback for best results. Please use the LL-HLS support and buffer level ABR options.
- HLS.js - Choose CMAF LL-HLS playback for best results.
- Shaka player - Use version 4.1.1 and above.
- Azure Media Player - Only on native Safari. It falls back to the native LL-HLS player.  On other platforms, it will choose to play DASH with approximately 1 second added latency compared to LL-HLS.  Choose "Low Latency Heuristic Profile".

## How-tos, tutorials and samples

- [Live Event with DVR - .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)
- [Low Latency - Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts)
- [Low Latency - Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event_Low_Latency/720p_low_latency_encoding_live_event.py)