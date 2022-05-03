---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Excessive and intermittent 5xx errors.
---

<!-- 2109030040000508 -->

## Excessive and intermittent 5xx errors

### Cause

1. On-premises encoding may have been implemented improperly.
1. The caching ratio between streaming endpoint and CDN may be insufficient.
1. Filter configuration may be incorrect.

### Solution

1. See the [Live streaming best practices guide](../live-event-streaming-best-practices-guide).
1. Use a [tested on-premises encoder](../encode-recommended-on-premises-live-encoders) and check that it is [configured properly](../encode-recommended-on-premises-live-encoders#configuring-on-premises-live-encoder-settings).
1. Adjust the caching ratio so that the CDN is handling more traffic.
1. Adjust the [streaming optimization](/azure/cdn/cdn-media-streaming-optimization) rule for the CDN.
