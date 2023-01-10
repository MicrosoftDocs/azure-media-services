---
title: Move a Media Services account to another subscription
description: This article discusses moving a Media Services v3 account to another subscription.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Move a Media Services account to another subscription

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

If you need to move a Media Services account to a new subscription, you need to first move the entire resource group that contains the Media Services account to the new subscription. You must move all attached resources: Azure Storage accounts, Azure CDN profiles, etc. For more information, see [Move resources to new resource group or subscription](/azure/azure-resource-manager/management/move-resource-group-and-subscription). As with any resources in Azure, resource group moves can take some time to complete.

## Considerations

* Create backups of all data in your account before migrating to a different subscription.
* You need to stop all the Streaming Endpoints and live streaming resources. Your users will not be able to access your content for the duration of the resource group move.

> [!IMPORTANT]
> Do not start the Streaming Endpoint until the move completes successfully.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
