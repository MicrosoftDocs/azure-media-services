---
title: How to enable CDN optimizations
description: To get the most of a streaming endpoint CDN, you may want to change the way it behaves based on certain conditions. This article covers how to use the Azure portal and the CDN Rules engine to adjust the behavior of a CDN profile.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# How to enable CDN optimizations

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

To get the best performance from streaming endpoint CDN, you may want to change the way it behaves based on certain conditions. This article covers how to use the Azure portal and the CDN Rules Engine to adjust the behavior of a CDN profile.

## Prerequisites

- Read the article [Scale Streaming with a CDN](stream-scale-streaming-cdn-concept.md) to understand how CDN caching works.
- A Media Services account with at least one streaming endpoint.

## Create a streaming endpoint

If you don't want to use the default streaming endpoint, you can create a new streaming endpoint:

1. Sign in to the Azure portal.
1. Navigate to the Media Services account you want to use.
1. Select **Streaming endpoints**.
1. Select **+ Add a streaming endpoint**. The *Create a streaming endpoint* screen will appear.
1. Enter a name into the **Streaming endpoint name** field.
1. Select either the **Standard** or **Premium** radio button for the streaming endpoint type.
1. Select either the **Yes** or **No** radio button for starting the streaming endpoint after creation.
1. Under the *Content Delivery Network* section, select *Premium Verizon* from the **CDN pricing tier** dropdown menu.
1. Select the **Select existing** radio button to select the CDN profile.
1. For **CDN Profile name**, the *AzureMediaStreamingPlatformCdnProfile-PremiumVerizon* profile should already be selected.
1. Add tags if needed.
1. Select **Create**. Once the streaming endpoint has been created, it will show up on the list of streaming endpoints.

## Add conditional rules for a Premium Verizon CDN

From the streaming endpoint screen:

1. Select the new streaming endpoint from the list.
1. In the CDN card, select the **AzureMediaStreamingPlatformCdnProfile-PremiumVerizon** profile. The *Profile* screen will appear.
1. Select **Manage**. A *CDN origin management* page will open in a new tab or window in your browser.
1. From the menu, select **HTTP Large** > **Rules Engine V4.0**.
1. Select **+ New** to create a new draft.
1. Enter a name into the **Draft Name Required** field.
1. Select **Continue**. The *Rule Builder* screen will appear.
1. Select **+Rule**. *Rule 1* interface will appear.
1. Give the rule a description in the **Rule Description** field (optional).
1. Select **+** > **Match**.
1. Create the conditions of the rule using the drop down menus. For example:
    - If *General* + *Always*
        - *Feature*
            - *Specialty* + *Streaming optimization*
1. Select **yes** to enable the rule.
1. Select **Save**.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
