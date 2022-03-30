---
title: Upload content to an asset CLI
description: The Azure CLI script in this topic shows how to create a Media Services Asset to upload content to.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 3/16/2022
ms.author: inhenkel
---

# Create an Asset

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows how to create a Media Services Asset.  You will use an asset to hold media content for encoding and streaming.  To learn more about Media Services assets, read [Assets in Azure Media Services v3](assets-concept.md)

## Prerequisites

Follow the steps in [Create a Media Services account](./account-create-how-to.md) to create the needed Media Services account and resource group to create an asset.

## Methods

Use the following methods to create a Media Services asset.

## [Portal](#tab/portal/)

Creating assets in the portal is as simple as uploading a file.

[!INCLUDE [task-create-asset-portal.md](includes/task-create-asset-portal.md)]

## [CLI](#tab/cli/)

[!INCLUDE [task-create-asset-cli.md](./includes/task-create-asset-cli.md)]

## [REST](#tab/rest/)

### Using REST

[!INCLUDE [task-create-asset-rest.md](./includes/task-create-asset-rest.md)]

### Using cURL

[!INCLUDE [task-create-asset-curl.md](./includes/task-create-asset-curl.md)]

## [.NET](#tab/net/)

[!INCLUDE [task-create-asset-dotnet.md](./includes/task-create-asset-dotnet.md)]

## [Python](#tab/python/)

[!INCLUDE [task-python-setup.md](./includes/task-python-setup.md)]

[!INCLUDE [task-create-asset-python.md](./includes/task-create-asset-python.md)]

---
