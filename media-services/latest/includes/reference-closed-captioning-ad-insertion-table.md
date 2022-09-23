---
title: Closed captioning and ad insertion
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 03/22/2022
ms.author: inhenkel
---

## Captioning and subtitles

The following table lists the types of captions supported by Media Services:

| Standard | Notes |
| -------- | ----- |
| WebVTT | WebVTT is the W3C standard for displaying timed text for the HTML5 text track element. This is the standard that Media Services uses for live transcirption during live events which is provided by Azure Cognitive Services. You can also use this standard to easily add captions and subtitles to be consumed by a player client such as Azure Media Player.
| TTML inside .ismt (Smooth Streaming text tracks) | Media Services dynamic packaging enables your clients to stream content in any of the following formats: DASH, HLS, or Smooth Streaming. However, if you ingest fragmented MP4 (Smooth Streaming) with captions inside .ismt (Smooth Streaming text tracks), you can deliver the stream to only Smooth Streaming clients. |
| CEA-708 and EIA-608 (708/608) | CEA-708 and EIA-608 are closed-captioning standards for the United States and Canada.<br/><br/>Currently, captioning is supported only if carried in the encoded input stream. You need to use a live media encoder that can insert 608 or 708 captions in the encoded stream that's sent to Media Services. Media Services delivers the content with inserted captions to your viewers. |
