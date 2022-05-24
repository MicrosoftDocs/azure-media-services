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

| Cause | Solution |
| ----- | -------- |
| Video packets are being delivered late. | Possible solutions: <br/><br/> 1. You may have implemented a storage versioning policy that was turned on automatically which causes buffering and disconnects. Remove the policy and turn off automatic storage versioning. <br/> 2. Enable a CDN. <br/> 3. Use a Premium streaming endpoint with enough reserved units.  |