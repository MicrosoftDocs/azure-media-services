---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Source unavailable error
---

<!-- 2201270040004073 -->

## Source unavailable error

"While trying to download the input files, the files were not accessible, please check the availability of the source"

### Cause

If you are using a SAS token to access the file, it may have expired.

### Solution

Adjust your code to check that the token hasn't expired before using it to authenticate.
