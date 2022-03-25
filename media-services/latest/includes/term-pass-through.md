---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/25/2022
ms.author: inhenkel
title: Pass through
---

**Pass through** - When using the pass-through Live Event (basic or standard), the on-premises live encoder to generates a multiple bitrate video stream and sends those as the contribution feed to the live event (using RTMP or fragmented-MP4 input protocol). The live event then passes the incoming video streams to the dynamic packager (streaming endpoint) without any further transcoding. A pass-through live event is optimized for long-running live events or 24x365 linear live streaming.
