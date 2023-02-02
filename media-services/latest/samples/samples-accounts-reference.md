---
title: Azure Media Services Accounts code samples
description: This article is a listing of code samples for Accounts.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/02/2023
ms.author: inhenkel
---

# Azure Media Services Accounts code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Accounts.

[!INCLUDE [net_samples_note](../includes/net_samples_note.md)]

## Create an account

The sample shows how to create a Media Services account and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, Managed Identity, storage auth, and bring your own encryption key.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Account/create-account.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Account/create-account.py) |

## Create an account with user assigned managed identity

The sample shows how to create a Media Services account and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, user or system assigned Managed Identity, storage auth, and bring your own encryption key.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Account/create-account_with_managed_identity.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Account/create-account-with-managed-identity.py) |

## List assets

This is a basic example of how to connect and list assets.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/HelloWorld-ListAssets/list-assets.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/list-assets-filtered.py) |

## Get the storage container from an asset

This sample demonstrates how to find the Azure storage account container used to store the contents of this asset. This can be used to then edit sources, modify, or copy contents using the Azure storage SDK library.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/get-container-from-asset.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/get-container-from-asset.py) |

## List assets using filters

This sample shows you how to use filters in your list assets calls to find assets by date and order them.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-assets-filtered.ts) |  :small_blue_diamond: |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
