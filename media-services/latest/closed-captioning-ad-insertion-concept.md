---
title: Closed captioning and ad insertion
description: The table in this article lists the types of captions supported by Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 03/22/2022
ms.author: inhenkel
---

# Closed captioning and ad insertion

The following table lists the types of captions supported by Media Services.

| Standard | Notes |
| -------- | ----- |
| CEA-708 and EIA-608 (708/608) | CEA-708 and EIA-608 are closed-captioning standards for the United States and Canada.<br/><br/>Currently, captioning is supported only if carried in the encoded input stream. You need to use a live media encoder that can insert 608 or 708 captions in the encoded stream that's sent to Media Services. Media Services delivers the content with inserted captions to your viewers. |
| TTML inside .ismt (Smooth Streaming text tracks) | Media Services dynamic packaging enables your clients to stream content in any of the following formats: DASH, HLS, or Smooth Streaming. However, if you ingest fragmented MP4 (Smooth Streaming) with captions inside .ismt (Smooth Streaming text tracks), you can deliver the stream to only Smooth Streaming clients. |
| SCTE-35 | SCTE-35 is a digital signaling system that's used to cue advertising insertion. Downstream receivers use the signal to splice advertising into the stream for the allotted time. SCTE-35 must be sent as a sparse track in the input stream.<br/><br/>Currently, the only supported input stream format that carries ad signals is fragmented MP4 (Smooth Streaming). The only supported output format is also Smooth Streaming. |

---
