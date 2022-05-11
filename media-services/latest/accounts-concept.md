---
title: Azure Media Services v3 accounts
description: To start managing, encrypting, encoding, analyzing, and streaming media content in Azure, you need to create a Media Services account. This article talks about Azure Media Services v3 accounts.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 05/11/2022
ms.author: inhenkel
---

# Azure Media Services v3 accounts

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

To start managing, encrypting, encoding, analyzing, and streaming media content in Azure, you need to create a Media Services account. A Media Services account is the foundation of everything you do with Media Services. It is the parent account for:

- Video On Demand (VOD) applications
- Live streaming applications
- Encoding and delivering videos
- Content protection, etc
- The storage of media assets to use with all of the above.

[!INCLUDE [account creation note](./includes/note-2020-05-01-account-creation.md)]

## Create a Media Services account

There are multiple ways to create a Media Services account.  See [Create a Media Services account](account-create-how-to.md?amspage=accounts-concept).

## Associated storage

When creating a Media Services account, you attach an Azure Storage account to the Media Services account. The Media Services account and all associated storage accounts must be in the same Azure subscription. For more information about storage accounts, see [Storage accounts](storage-account-concept.md?amspage=accounts-concept).

## Associate streaming endpoint

If you create an account using the Azure portal, a streaming endpoint is also created.  The name of the streaming endpoint is *default*.  You can [create additional streaming endpoints](streaming-endpoint-create-how-to.md?amspage=accounts-concept) for your account if you don't want to use the default streaming endpoint.

## How-tos and Tutorials

- [Create a storage account](storage-create-how-to.md?amspage=accounts-concept)
- [Add storage to an account](account-add-account-storage-how-to.md?amspage=accounts-concept)
- [Remove storage from an account](account-remove-account-storage-how-to.md?amspage=accounts-concept)
- [List assets in an account](account-list-assets-how-to.md?amspage=accounts-concept)
- [List transforms in an account](account-list-transforms-how-to.md?amspage=accounts-concept)
- [Set account encryption with customer-managed keys](account-set-account-encryption-customer-managed-key-how-to.md?amspage=accounts-concept)
- [Set account encryption with system-managed keys](account-set-account-encryption-system-managed-key-how-to.md?amspage=accounts-concept)
- [Show account encryption](account-show-encryption-how-to.md?amspage=accounts-concept)
- [Sync storage keys](storage-sync-storage-keys-how-to.md?amspage=accounts-concept)