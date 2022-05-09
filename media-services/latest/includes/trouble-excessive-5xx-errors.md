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

| Cause | Solution |
| ----- | -------- |
| On-premises encoding may have been implemented improperly. | Check that your encoder is [configured properly](../encode-recommended-on-premises-live-encoders.md?amspage=troubleshooting#configuring-on-premises-live-encoder-settings). |
| You may be using a non-tested on-premises encoder | Use a [tested on-premises encoder](../encode-recommended-on-premises-live-encoders.md?amspage=troubleshooting) and check that it is [configured properly](../encode-recommended-on-premises-live-encoders.md?amspage=troubleshooting#configuring-on-premises-live-encoder-settings).
| The caching ratio between streaming endpoint and CDN may be insufficient. | 1. Adjust the caching ratio so that the CDN is handling more traffic. <br/> 2. Adjust the [streaming optimization](/azure/cdn/cdn-media-streaming-optimization) rule for the CDN. |
| Filter configuration may be incorrect. | Check that your [filters configured properly](../filters-concept.md?amspage=troubleshooting). |

See the [Live streaming best practices guide](../live-event-streaming-best-practices-guide.md?amspage=troubleshooting).
