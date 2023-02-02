---
title: Azure Media Services Live Streaming code samples
description: This article is a listing of code samples for Live Streaming.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/02/2023
ms.author: inhenkel
---

# Azure Media Services Live Streaming code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Live Streaming.

[!INCLUDE [net_samples_note](../includes/net_samples_note.md)]

## Live stream with standard passthrough

This sample shows you how to use standard passthrough live streaming.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/Standard_Passthrough_Live_Event/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/Standard_Passthrough_Live_Event/standard_passthrough_live_event.py) |

## Live stream with standard passthrough with Event Hubs

This sample demonstrates how to use Event Hubs to subscribe to events on the live streaming channel. Events include encoder connections, disconnections, heartbeat, latency, discontinuity, and drift issues.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/Standard_Passthrough_Live_Event_with_EventHub/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/Standard_Passthrough_Live_Event_Event_Hub/standard_passthrough_live_event_with_eventhub.py) |

## Live stream with basic passthrough

This sample shows you how to set up the basic passthrough live event if you only need to broadcast a low-cost UGC channel.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/Basic_Passthrough_Live_Event/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/Basic_Passthrough_Live_Event/basic_passthrough_live_event.py) |

## Live stream with low Latency (LL-HLS) with 720P standard encoding

This sample shows you how to enable low latency live streaming with Apple's LL-HLS protocol and encode with the new 3-layer 720P HD adaptive bitrate encoding preset.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event_Low_Latency/720p_low_latency_encoding_live_event.py) |

## Live stream with 720P standard encoding

This sample shows you how to use live encoding in the cloud with the 720P HD adaptive bitrate encoding preset.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Encoding_Live_Event/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event/720p_encoding_live_event.py) |

## Live stream with 1080P encoding

This sample shows you how to use live encoding in the cloud with the 1080P HD adaptive bitrate encoding preset.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Encoding_Live_Event/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/1080p_Encoding_Live_Event/1080p_encoding_live_event.py) |

## FFmpeg command line samples for RTMP and Smooth

This sample shows you how to use FFmpeg command lines locally to stream over RTMP or Smooth streaming. It demonstrates various scenarios including audio only, multi-audio, and screen recording.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/FFmpeg/ffmpeg_commands.md) |  :small_blue_diamond: |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]