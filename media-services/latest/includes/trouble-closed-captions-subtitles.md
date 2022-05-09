---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Closed caption and subtitles issues
---

<!-- 2204220040000581 -->

## The player request for the VTT file caused CORS errors.

| Cause | Solution |
| ----- | -------- |
| CORS rules setup | Set up [CORS rules](/rest/api/storageservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) for your storage account or [CDN](/azure/cdn/cdn-cors). |

Yuu can also get the download URL of the VTT file from the asset.
