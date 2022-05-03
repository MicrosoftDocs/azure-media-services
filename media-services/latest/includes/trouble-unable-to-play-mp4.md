---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Unable to download or play an MP4 file
---

<!-- 2201110050000558, multipe -->

## Unable to download or play an MP4 file

### Cause

Azure Media Services is designed to use a manifest file rather than playing full size MP4 streams directly.  The manifest file tells the player which encoded media fragments to play and in what order.

### Solution

Use one of the provided media encoders to create media fragments and manifest file. For more information about encoding see [Content-aware encoding](encode-content-aware-concept) and [Encode with an auto-generated bitrate ladder](encode-autogen-bitrate-ladder) encoding.
