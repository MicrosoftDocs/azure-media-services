---
title: Azure Media Services Accounts code samples
description: This article is a listing of code samples for Accounts.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 02/24/2023
ms.author: inhenkel
---

# Azure Media Services Accounts code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Accounts.

## Create an account

This sample shows how to create a Media Services account and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, Managed Identity, storage auth, and bring your own encryption key.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Account/create-account.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Account/create-account.py) |

## Create an account with user assigned managed identity

This sample shows how to create a Media Services account with a managed identity and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, user or system assigned Managed Identity, storage auth, and bring your own encryption key.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Account/create-account_with_managed_identity.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Account/create-account-with-managed-identity.py) |

## Account management with .NET

The sample shows how to create a Media Services account and set the primary storage account, in addition to advanced configuration settings including Key Delivery IP allowlist, Managed Identity, storage auth, and bring your own encryption key.

[Create Account](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Account/CreateAccount)

This sample shows how to list all Media Services accounts in a resource group and select one by its name.

[Get Accounts](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Account/GetAccounts)

This sample shows how to use the metrics API to retrieve account quotas.

[Quotas](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Account/Quotas)
