---
title: Closed captioning and ad insertion
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 03/22/2022
ms.author: inhenkel
---

## Ad insertion

The following table lists the types of captions supported by Media Services.

| Standard | Notes |
| -------- | ----- |
| SCTE-35 | SCTE-35 is a digital signaling system that's used to cue advertising insertion. Downstream receivers use the signal to splice advertising into the stream for the allotted time. SCTE-35 must be sent as a sparse track in the input stream.<br/><br/>Currently, the only supported input stream format that carries ad signals is fragmented MP4 (Smooth Streaming). The only supported output format is also Smooth Streaming. |

---
