---
title: Scale media processing using the Azure portal
description: This tutorial walks you through the steps of scaling media processing using the Azure portal.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: article
ms.date: 10/05/2022
---

<!-- ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da -->

# Change the reserved unit type

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

## Overview

By default, Media Reserve Units are no longer needed to be used and are not supported by Azure Media Services. For compatibility purposes, the current Azure portal has an option for you to manage and scale MRUs. However, by default, none of the MRU configurations that you set will be used to control encoding concurrency or performance.

> [!IMPORTANT]
> Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.

## Scale media processing

>[!NOTE]
>Selecting MRUs will not affect concurrency or performance in Azure Media Services V3.

To change the reserved unit type and the number of reserved units, do the following:

1. In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.
2. In the **Settings** window, select **Media reserved units**.

    To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider at the top of the screen.

    To change the **RESERVED UNIT TYPE**, click on the **Speed of reserved processing units** bar. Then, select the pricing tier you need: S1, S2, or S3.

3. Press the SAVE button to save your changes.

    The new reserved units are allocated when you press SAVE.
