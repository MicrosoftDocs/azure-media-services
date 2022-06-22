---
title: LiveEvent low latency settings in Azure Media Services
description: This article discusses low latency on a live event. It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 05/11/2022
ms.author: inhenkel
---

# Live Event low latency settings

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article discusses low latency on a [live event](/rest/api/media/liveevents). It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.

For *pass-through* live events, we recommend that you always use the `LowLatency` option. It is recommended only if you require the Smooth Streaming output format, or require a DVR window longer than 6 hours.

For *encoding* live events, you can choose between `LowLatency` or `LowLatencyV2`. LowLatencyV2 setting is recommended if you wish to go down to 3-7 seconds of end to end latency for your live stream. This setting is currently only available for DASH or Low Latency HLS outputs. Although it is optimized for CMAF LL-HLS playback (format=aapl-cmaf), the setting still supports all other streaming formats other than smooth. You will see latency improvements regardless of the format used.

When using TS outputs with HLS v3 (format=aapl-m3u8-v3) and HLS v4 (format=aapl-m3u8-v4), be sure to set the `LiveOutput.Hls.fragmentsPerTsSegment` setting to 1 to ensure that Media Services packs only 1 mp4 fragment into one TS segment.

You will need proper settings on your LL-HLS or DASH capable players to see the best latency numbers.

We have tested with the following media players:

- Video.js - Choose CMAF LL-HLS playback for best results. Please use the LL-HLS support and experimental ABR options.
- HLS.js - Choose CMAF LL-HLS playback for best results.
- Shaka player - From version xxxx, which contains fixes for CMAF LL-HLS playback.
- Azure Media Player - Only on native Safari. It falls back to the native LL-HLS player.  On other platforms, it will choose to play DASH with approximately 1 second added latency compared to LL-HLS.  Choose "Low Latency Heuristic Profile".

## Live Events latency

The following tables show typical results for latency in Media Services, measured from the time the contribution feed reaches the service to when a viewer sees the playback on the player. To use low latency optimally, you should tune your encoder settings down to 1 second "Group Of Pictures" (GOP) length. When using a higher GOP length, you minimize bandwidth consumption and reduce bitrate under same frame rate. It is especially beneficial in videos with less motion.

### Pass-through with LowLatency stream option

||2s GOP|1s GOP|
|---|---|---|
|**DASH in AMP**|10s|8s|
|**HLS on native iOS player**|14s|10s|

### Live encoding with LowLatency stream option

||2s GOP |1s GOP |
|---|---|---|
|**DASH in AMP**|14s|10s|
|**HLS on native iOS player**|18s|13s|

### Live encoding with LowLatencyV2 option

GOP size doesn't affect latency with the LowLatencyV2 option.

| | |
|---|---|
|**DASH in AMP**| 4-8 seconds|
|**HLS on native iOS player**| 3-7 seconds|

> [!NOTE]
> The end-to-end latency can vary depending on local network conditions or by introducing a CDN caching layer. You should test your exact configurations.

## Supported encryption formats

Media Services can currently only support the following encryption formats for live events with LowLatencyV2 stream option:

**TO DO  Need encryption formats.**

## How-tos, tutorials and samples

- [Live Event with DVR - .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)
- [Low Latency - Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts)
- [Low Latency - Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event_Low_Latency/720p_low_latency_encoding_live_event.py)