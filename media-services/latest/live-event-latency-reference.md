---
title: LiveEvent low latency settings in Azure Media Services
description: This topic gives an overview of LiveEvent low latency settings and shows how to set low latency.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 3/16/2022
ms.author: inhenkel
---

# Live Event low latency settings

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows how to set low latency on a [Live Event](/rest/api/media/liveevents). It also discusses typical results that you see when using the low latency settings in various players. The results vary based on CDN and network latency.

To use the new **LowLatency** feature, you set the **StreamOptionsFlag** to **LowLatency** on the **LiveEvent**. When creating [LiveOutput](/rest/api/media/liveoutputs) for HLS playback, set [LiveOutput.Hls.fragmentsPerTsSegment](/rest/api/media/liveoutputs/create#hls) to 1. Once the stream is up and running, you can use the [Azure Media Player](https://ampdemo.azureedge.net/) (AMP demo page), and set the playback options to use the "Low Latency Heuristics Profile".

> [!NOTE]
> Currently, the LowLatency HeuristicProfile in Azure Media Player is designed for playing back streams in MPEG-DASH protocol, with either CSF or CMAF format (for example, `format=mdp-time-csf` or `format=mdp-time-cmaf`).

## Live Events latency

The following tables show typical results for latency (when the LowLatency flag is enabled) in Media Services, measured from the time the contribution feed reaches the service to when a viewer sees the playback on the player. To use low latency optimally, you should tune your encoder settings down to 1 second "Group Of Pictures" (GOP) length. When using a higher GOP length, you minimize bandwidth consumption and reduce bitrate under same frame rate. It is especially beneficial in videos with less motion.

### Pass-through

||2s GOP low latency enabled|1s GOP low latency enabled|
|---|---|---|
|**DASH in AMP**|10s|8s|
|**HLS on native iOS player**|14s|10s|

### Live encoding

||2s GOP low latency enabled|1s GOP low latency enabled|
|---|---|---|
|**DASH in AMP**|14s|10s|
|**HLS on native iOS player**|18s|13s|

> [!NOTE]
> The end-to-end latency can vary depending on local network conditions or by introducing a CDN caching layer. You should test your exact configurations.

## Low Latency How-tos and Tutorials

- [Live Event with DVR - .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)
- [Low Latency - Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts)