---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Video playback issues
---

<!-- 2112130040007664, 2201210050001913 -->

## Common video playback issues

- Videos take a long time to start playing.
- Videos are blurry when they start playing.
- Video quality is low.
- Video doesn't play at all or shows a black screen.


| Cause | Solution |
| ----- | -------- |
| You may be attempting to reach a large audience without using a CDN which is causing latency issues. | Add a CDN to your streaming locator. For more information about using a CDN, see [Stream content with CDN integration](../stream-scale-streaming-cdn-concept.md?amspage=troubleshooting). |
| You may not have implemented dynamic packaging. |  For more information on implementing dynamic packaging, see [Dynamic packaging in Media Services v3](../encode-dynamic-packaging-concept.md?amspage=troubleshooting). |
| You may have what is known as "noisy neighbors", which means that you are sharing compute resources with other customers. | To avoid "noisy neighbors" upgrade from a standard streaming endpoint to a premium streaming endpoint with dedicated streaming units. |
| You may be using an older browser to view videos. | Upgrade your browser. |
| You may be using a 3rd party player and filters. | Add `audio-only=false` to the streaming URL like so `https://streamingtest.streaming.media.azure.net/00000000-0000-0000-0000-000000000000/sample.ism/manifest(format-m3u8-aapl,audio-only=false)` |

## You can't play an MP4 file from the asset

| Cause | Solution |
| ----- | -------- |
| Azure Media Services is designed to use a manifest file rather than playing full size MP4 streams directly.  The manifest file tells the player which encoded media fragments to play and in what order. | Use one of the provided media encoders to create media fragments and manifest file. For more information about encoding see [Content-aware encoding](../encode-content-aware-concept.md?amspage=troubleshooting) and [Encode with an auto-generated bitrate ladder](../encode-autogen-bitrate-ladder.md?amspage=troubleshooting) encoding. |
| The file name contains reserved characters. | Remove the reserved characters from the file name. |

[!INCLUDE [reserved_characters](../includes/reserved_characters.md)]
