---
title: Live Event low latency settings in Azure Media Services
description: Media Services supports Apple's Low Latency HLS (LL-HLS).  Watch Roger Pantos explain the Low Latency HLS specification at WWDC19 to get an understanding of how the specification works and what it can do you for you. This article describes Media Services support for LL-HLS and provides you with implementation guidance.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 01/09/2023
ms.author: inhenkel
---

# Low Latency HLS (LL-HLS)

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Media Services supports Apple's Low Latency HLS (LL-HLS) specification as well as DASH.  [Watch](https://developer.apple.com/videos/play/wwdc2019/502/) Roger Pantos explain the Low Latency HLS specification at WWDC19 to understand how the specification gets your media content to your viewers faster.

This article describes Media Services support for LL-HLS and provides you with implementation guidance.

## LowLatency and LowLatencyV2 options

Media Services provides two options for delivering streaming content with low latency.

- **LowLatencyV2**. Use this option when:
  - You are using Media Services to encode a live event
  - You are using either Low Latency HLS or DASH CMAF
- **LowLatency**. Use this option when:
  - You are using a pass-through live event
  - You need Smooth Streaming output
  - An archive length (DVR window) of more than 6 hours
  - Need to use FairPlay on Apple devices

## LL-HLS URL

This is an example of an HLS URL. The `(format-m3u8-cmaf)` part of the URL is required.

`https://myamsaccount-usw22.streaming.media.azure.net/06c39667-84d8-43ce-9dba-3aee82e35262/output-20221021-193449-manifest.ism/manifest(format=m3u8-cmaf)`

## How to use LL-HLS

### Use LowLatencyV2 in the Azure portal

1. Set up your on-premises stream. Try the [OBS tutorial](live-event-obs-quickstart.md) if you haven't done this before.
1. While creating a live event, select either **Standard encoding (up to 720p)** or **Premium encoding (up to 1080p)** under the live event type.  The Stream latency options will appear.
1. Select the **Low latency** radio button.  *LowLatencyV2* will automatically be selected for the encoding standard you chose.
1. Optionally select the **Start preparing live event for input** checkbox to automatically start the live event. Remember that billing starts as soon as a live event is started.
1. Set any other options you want for the live event then select **Review and create**. The live event screen will appear with a listing of the streaming URLs.
1. Copy the **HLS URL** for use with the player.

### LL-HLS SDK Samples

There are detailed instructions in the comments of the sample code provided for LL-HLS.

- [Live Event with DVR - .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)
- [Low Latency - Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts)
- [Low Latency - Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event_Low_Latency/720p_low_latency_encoding_live_event.py)

See [dynamic packaging](encode-dynamic-packaging-concept.md) page for more information on streaming URL formats.

## Player testing

Use the links below to see the [3rd-party player sample](https://github.com/Azure-Samples/media-services-3rdparty-player-samples) test results.

- Azure Media Player - use Low Latency Heuristic Profile. On Safari, it falls back to the native LL-HLS player. On other platforms, it will choose to play DASH.
- [Shaka ](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/shaka#test-results)
- [Video.js](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/video.js#test-results)
- [hls.js](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/hls.js#test-results)
- [dash.js](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/dash.js#test-results)
- [ExoPlayer](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/exoplayer#test-results)
- [AVPlayer](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/avplayer#test-results)
- [THEOplayer](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/THEOplayer#test-results)
- [NexPlayer](https://github.com/Azure-Samples/media-services-3rdparty-player-samples/blob/master/docs/NexPlayer#test-results)

## Additional recommendations

When using HLS output, choose HLS CMAF (format=m3u8-cmaf) whenever possible. If you must use other streaming formats such as TS outputs with HLS v3 (format=aapl-m3u8-v3) or HLS v4 (format=aapl-m3u8-v4), be sure to set the `LiveOutput.Hls.fragmentsPerTsSegment` setting for your live event to 1 to ensure that Media Services packs only one mp4 fragment into one TS segment.

> [!NOTE]
> The end-to-end latency can vary depending on local network conditions or by introducing a CDN caching layer. You should test your exact configurations.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
