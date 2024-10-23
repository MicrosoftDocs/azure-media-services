---
title: Storage side encryption for Media Services storage accounts
description: To protect your assets at rest, the assets should be encrypted by the storage side encryption.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Storage side encryption for Media Services storage accounts

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Storage side encryption

To protect your assets at rest, the assets should be encrypted by the storage side encryption. The following table shows how the storage side encryption works in Media Services v3:

|Encryption option|Description|Media Services v3|
|---|---|---|
|Media Services storage encryption| AES-256 encryption, key managed by Media Services. |Not supported.<sup>1</sup>|
|[Storage service encryption for data at rest](/azure/storage/common/storage-service-encryption)|Server-side encryption offered by Azure Storage, key managed by Azure or by customer.|Supported.|
|[Storage client-side encryption](/azure/storage/common/storage-client-side-encryption)|Client-side encryption offered by Azure storage, key managed by customer in Key Vault.|Not supported.|

<sup>1</sup> In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your assets were created with Media Services v2, which means v3 works with existing storage encrypted assets but won't allow creation of new ones.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
