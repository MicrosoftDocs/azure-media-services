---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Video playback issues
---

<!-- 2112130040007664 -->

## Video playback issues

- Videos take a long time to start playing.
- Videos are blurry when they start playing.

### Cause

You may be attempting to reach a large audience without using a CDN which is causing latency issues.
You may not have implemented dynamic packaging.

### Solution

Add a CDN to your streaming locator. For more information about using a CDN, see [Stream content with CDN integration](../stream-scale-streaming-cdn-concept.md)
For more information on implementing dynamic packaging, see [Dynamic packaging in Media Services v3](../encode-dynamic-packaging-concept.md)