---
title: Azure storage accounts
description: Learn how to create an Azure storage account to use with Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 3/16/2022
ms.author: inhenkel
---

# Azure Storage accounts

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

When you create a Media Services account, a storage account will be attached to it.  When you create a Media Services account in the portal, storage account creation is part of the process.  When you create a Media Services account with other methods, you have to create the storage account seperately, then attach it to the Media Services account.

## Assets in a storage account

In Media Services v3, the Storage APIs are used to upload files into assets. For more information about Assets, see [Assets in Azure Media Services v3](assets-concept.md).

## Required storage account types and limits

You must have one **Primary** storage account and you can have any number of **Secondary** storage accounts associated with your Media Services account. Media Services supports **General-purpose v2** (GPv2) or **General-purpose v1** (GPv1) accounts only. Azure Data Lake Gen2 or blob only accounts aren't allowed to be used as **Primary** or **Secondary**.

We recommend that you use General-purpose v2, so you can take advantage of the latest features and performance. To learn more about storage account types, see [Azure Storage account overview](/azure/storage/common/storage-account-overview).

Azure Data Lake Gen2 storage is not supported by Media Services. To ingest content from a storage account using hierarchical namespace support, you must submit encoding jobs using SAS URLs and the JobInputHttp feature in Media Services.

> [!NOTE]
> It is recommended to use the hot storage tier when streaming assets for live or VOD. Cool storage can be used for encoding jobs and long term storage of assets that are not actively being streamed, but keep in mind the higher costs of reading from cool storage if you plan to do a lot of reads on content. One strategy can be to move your master/mezzanine source assets into a secondary storage account that is configured as cool storage to reduce the long term costs of retention on your source files, and output your encoded files for streaming into a storage account configured for hot storage.

There are different SKUs you can choose for your storage account. If you want to experiment with storage accounts, use `--sku Standard_LRS`. However, when picking a SKU for production, you should consider `--sku Standard_RAGRS`, which provides geographic replication for business continuity.

## Usage of cross-subscription storage accounts

[!INCLUDE [Usage of cross-subscription storage accounts](./includes/note-account-storage-same-subscription.md)]

## How-Tos and Tutorials

- [Create a storage account](storage-create-how-to.md?amspage=storage-account-concept)
- [Add storage to an account](account-add-account-storage-how-to.md?amspage=storage-account-concept)
- [Remove storage from an account](account-remove-account-storage-how-to.md?amspage=storage-account-concept)
- [List assets in an account](account-list-assets-how-to.md?amspage=storage-account-concept)
- [List transforms in an account](account-list-transforms-how-to.md?amspage=storage-account-concept)
- [Set account encryption with customer-managed keys](account-set-account-encryption-customer-managed-key-how-to.md?amspage=storage-account-concept)
- [Set account encryption with system-managed keys](account-set-account-encryption-system-managed-key-how-to.md?amspage=storage-account-concept)
- [Show account encryption](account-show-encryption-how-to.md?amspage=storage-account-concept)
- [Sync storage keys](storage-sync-storage-keys-how-to.md?amspage=storage-account-concept)
- [Manage multiple storage accounts](storage-managing-multiple-storage-accounts-how-to.md?amspage=storage-account-concept)
- [Access storage with a Media Services Managed Identity](security-access-storage-managed-identity-cli-tutorial.md?amspage=storage-account-concept)
- [Media Services trusted storage](security-trusted-storage-rest-tutorial.md?amspage=storage-account-concept)
- [Use the Azure portal to use customer-managed keys or BYOK with Media Services](security-customer-managed-keys-portal-tutorial.md?amspage=storage-account-concept)