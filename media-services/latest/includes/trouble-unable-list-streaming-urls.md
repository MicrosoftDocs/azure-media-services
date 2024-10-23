---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 05/02/2022
ms.author: inhenkel
title: Unable to list streaming URLs.
---

<!-- 2203160050001645 -->

## Unable to list streaming URLs.

| Cause | Solution |
| ----- | -------- |
| An account may have been moved between subscriptions and the new managed identity doesn't have assigned roles for the storage account. | Assign the missing *Reader* and *Storage Blog Data Contributor* roles to the managed identity. |
