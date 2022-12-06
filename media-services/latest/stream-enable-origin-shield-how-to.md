---
title: How to enable origin shield
description: It is best to use a Content Delivery Network (CDN) with a shielded origin to ensure that traffic for your media content is delivered efficiently. This article walks you through the steps in the Azure portal.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 12/05/2022
ms.author: inhenkel
---

# How to enable a CDN origin shield

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

It is best to use a Content Delivery Network (CDN) with a shielded origin to ensure that traffic for your media content is delivered efficiently. This article walks you through the steps in the Azure portal.

> [!NOTE]
> Origin Shield is only available in the CDN Supplemental Portal for *Azure CDN from Verizon Premium*. To use Origin Shield for *Azure CDN from Verizon Standard* open a support ticket in the Azure portal.
>
> Origin Shield configuration may not be available for older CDN profiles. If Origin Shield is not available in the portal UI, you will need to create a support ticket to have it enabled.

## Prerequisites

- Read the article [Scale Streaming with a CDN](stream-scale-streaming-cdn-concept.md) to understand how CDN caching works.
- Read [How to enable CDN optimizations](stream-set-cdn-profile-rules-how-to.md).
- A Media Services account with at least one streaming endpoint.

## Determine the closest POP location

You will need to know the geographic location of the origin as you should select the closest POP location in the below configuration steps. You can look up the datacenter. For example, if you chose Central US for the region of your origin, the datacenter is located in the state of Iowa, in the US. You would pick the POP location that is geographically closest to Iowa.


## Enable the origin shield

The streaming endpoint must be started in order to complete the following steps.

From the streaming endpoint screen:

1. Select the new streaming endpoint from the list.
1. In the CDN card, select the CDN profile. The Profile screen will appear.
1. Select **Manage**. A CDN origin management page will open in a new tab or window in your browser.
1. Expand the list of origins using the down arrow to the right of the trash can icon.
1. Find the *HTTPS – Edge Protocol CDN* and select the right arrow to expand the origin settings
1. Select the right arrow next to the origin you want to work with. The origin editing screen will appear.
1. In Group Settings, select **Origin Shield**.
1. Select the **Origin Shield** toggle to enable the origin shield settings.
1. Select the **Single POP** radio button.
1. From the **ALL POPs** dropdown list, select a POP location near the Streaming Endpoint. For example, if the streaming endpoint is in US West 2, choose one of the Seattle POPs from the dropdown list.
1. Select **Save**.
1. Verify that the **Origin Shield** checkbox is ticked in the list of origins for both origins.
