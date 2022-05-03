---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: The live stream shows a black screen.
---

<!-- 2202110010000084 -->

## The live stream shows a black screen.

### Cause

#### API implementation

1. You may be attempting to use the features of the v3 API with a v2 account or a v2 API implementation.

#### Filters

1. You may be using a 3rd party player and filters.

### Solution

#### API implementation solution

1. Update your code to use the v3 API. For more detailed assistance, see the [Migration guide](../migrate-v-2-v-3-migration-introduction.md).

#### Filters solution

1. Add audio-only=false to the streaming URL like so `https://streamingtest.streaming.media.azure.net/00000000-0000-0000-0000-000000000000/sample.ism/manifest(format-m3u8-aapl,audio-only=false)`
