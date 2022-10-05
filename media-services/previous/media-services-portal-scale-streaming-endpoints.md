---
title: Scale streaming endpoints with the Azure portal
description: This tutorial walks you through the steps of scaling streaming endpoints with the Azure portal.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: article
ms.date: 10/05/2022
---

<!-- ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e -->

# Scale streaming endpoints with the Azure portal

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

## Overview

> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).
>
>

**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity. Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU). The streaming endpoint can be scaled by adding SUs. Each SU provides additional bandwidth capacity to the application. For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-streaming-endpoints-overview.md) topic.

This topic shows how to scale a streaming endpoint.

For information about pricing details, see [Media Services Pricing Details](https://azure.microsoft.com/pricing/details/media-services/).

## Scale streaming endpoints

To change the number of streaming units, do the following:

1. In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.
2. In the **Settings** window, select **Streaming endpoints**.
3. Click on the streaming endpoint that you want to scale.
    > [!NOTE]
    > You can only scale **Premium** streaming endpoints.

4. Move the slider to specify the number of streaming units.

    ![Streaming endpoint](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)
