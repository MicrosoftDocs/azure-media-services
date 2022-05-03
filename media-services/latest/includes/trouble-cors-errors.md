---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: CORS issues
---

<!-- 2201060050001871 -->

## CORS issues

### Cause

If you are attempting to use preflight requests containing traceparent headers, you will receive CORS errors.  At this time, Media Services doesn't support preflight requests.

### Solution

We are aware that preflight requests are of value to our customers.  Don't use preflight requests until the feature is available.
