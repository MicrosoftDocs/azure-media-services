---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Video playback issues
---

<!-- 2112130040007664, 2201210050001913 -->

## Video playback issues

- Videos take a long time to start playing.
- Videos are blurry when they start playing.
- Video quality is low.

### Cause

1. You may be attempting to reach a large audience without using a CDN which is causing latency issues.
1. You may not have implemented dynamic packaging.
1. You may have what is known as "noisy neighbors", which means that you are sharing compute resources with other customers.

### Solution

1. Add a CDN to your streaming locator. For more information about using a CDN, see [Stream content with CDN integration](../stream-scale-streaming-cdn-concept.md).
1. For more information on implementing dynamic packaging, see [Dynamic packaging in Media Services v3](../encode-dynamic-packaging-concept.md).
1. To avoid "noisy neighbors" upgrade from a standard streaming endpoint to a premium streaming endpoint with dedicated streaming units.
