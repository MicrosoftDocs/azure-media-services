---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/24/2022
ms.author: inhenkel
title: A streaming endpoint with a CDN won't stop.
---

<!-- 2201160050000370 -->

## A streaming endpoint with a CDN won't stop.

### Cause

When you enable the CDN for any streaming endpoint, the CDN endpoint won't be created until you start the streaming endpoint. This reason is that during the start process, our platform will create the CDN endpoints and link them to the streaming endpoint (including configuring the custom hostname).

During the stop process for the streaming endpoint, our platform should delete the CDN endpoint. Therefore, if the streaming endpoint is in stop state, the CDN endpoint will not exist nor point to the streaming endpoint.

However, in some scenarios, when AMS calls the CDN to delete the CDN endpoints, it fails to delete endpoints due to caches on the CDN. This results in a hostname conflict problem if the CDN endpoint is still there and triggers the stop streaming endpoint issue.

### Solution

Manually delete the CDN profile and then delete the streaming endpoint and setup a new one.
