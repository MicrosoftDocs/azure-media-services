---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 03/25/2020
ms.author: inhenkel
---

> [!NOTE]
> When Media Services is configured to use Managed Identity to access storage, Media Services can use any storage account that the Managed Identity can access.
>
> When using System authentication to storage, the storage account must be in the same subscription as the Media Services account.
> It's recommended to use storage accounts in the same region as the Media Services account to avoid additional data egress costs.
>
> **Future requirement**: For both authentication types, the principal that creates or updates the Media Services account must have the 'Microsoft.Storage/storageAccounts/listkeys/action' permission over the storage account.
