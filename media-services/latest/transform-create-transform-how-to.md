---
title: Azure CLI Script Example - Create a transform 
description: Transforms describe a simple workflow of tasks for processing your video or audio files (often referred to as a "recipe"). The Azure CLI script in this article shows how to create a transform. 
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 11/18/2020
ms.author: inhenkel
---


# Create a transform

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

The Azure CLI script in this article shows how to create a transform. Transforms describe a simple workflow of tasks for processing your video or audio files (often referred to as a "recipe"). You should always check if a Transform with desired name and "recipe" already exist. If it does, you should reuse it.

## Prerequisites

[Create a Media Services account](./account-create-how-to.md).

## Methods

You can use the following methods to create a transform.

## [Portal](#tab/portal/)

[!INCLUDE [task-create-asset-portal](includes/task-create-transform-portal.md)]

## [CLI](#tab/cli/)

[!INCLUDE [task-create-asset-portal](includes/task-create-transform-cli.md)]

## [REST](#tab/rest/)

See the Media Services [REST API](/rest/api/media/transforms/create-or-update).

---

