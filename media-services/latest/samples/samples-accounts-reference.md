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

This sample shows how to create a Media Services account and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, Managed Identity, storage auth, and bring your own encryption key.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Account/create-account.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Account/create-account.py) |

## Create an account with user assigned managed identity

This sample shows how to create a Media Services account with a managed identity and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, user or system assigned Managed Identity, storage auth, and bring your own encryption key.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Account/create-account_with_managed_identity.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Account/create-account-with-managed-identity.py) |
