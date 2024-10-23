---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Encoding seems to be too slow
---

<!-- 2112020040001414 -->

## Encoding seems to be taking a long time.

Most encoding duration issues can be resolved by configuring the encoder settings to control the balance between speed and quality. For faster encoding, set it to *speed* mode.

| Cause | Solution |
| ----- | -------- |
| The mezzanine file may be very large. File size is equal to the bitrate multiplied by duration. | None |
| There are a high number of output layers. | Reduce the number of output layers. |
| Output layers have high resolution. | Reduce the resolution of the output layer to the bitrate you intend to stream media. |
| The mezzanine file may be complex, especially if you are encoding a 4k resolution file. | None |
