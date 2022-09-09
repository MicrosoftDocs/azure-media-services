---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 09/09/2022
ms.author: inhenkel
title: GOP sizes important
---

> [!IMPORTANT]
> You *should* use GOP sizes of 2 seconds for live events. You **must** use GOP sizes of 4 seconds or below for passthrough live events with live transcriptions in order to get correct transcription data. If you choose to use higher GOP size, the transcription data might have defects, e.g. missing content.
