---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 06/24/2022
ms.author: inhenkel
title: Reserved characters
---

### Reserved characters

- Media Services uses the value of the asset file name when building URLs for streaming content. For this reason, percent-encoding is not allowed. The value of the name property cannot have any of the following percent-encoding-reserved characters: !*'();:@&=+$,/?%#[]". Also, there can only be one '.' for the file name extension.
- The length of the name should not be greater than 260 characters.