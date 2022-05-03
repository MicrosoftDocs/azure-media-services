---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: The audio is out of sync
---

<!-- 2106210040004186 -->

## The audio is out of sync.

### Cause

You may have implemented a storage versioning policy that was turned on automatically which causes buffering and disconnects.

### Solution

Remove the policy and turn off automatic storage versioning.