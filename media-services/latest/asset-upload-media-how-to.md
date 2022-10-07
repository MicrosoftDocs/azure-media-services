---
title: Upload media
description: Learn how to upload media for streaming or encoding.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 10/07/2022
ms.author: inhenkel
---

# Upload media for streaming or encoding

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

In Media Services, you upload your digital files (media) into a blob container associated with an asset. The [Asset](/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files). Once the files are uploaded into the asset's container, your content is stored securely in the cloud for further processing  and streaming.

## Collect values

Before you get started, you'll need to collect or think about a few values.

1. The local file path to the file you want to upload
1. The asset ID for the asset (container)
1. The name you want to use for the uploaded file including the extension
1. The name of the storage account you are using
1. The access key for your storage account

## File naming

[!INCLUDE [reserved_characters](./includes/reserved_characters.md)]

[!INCLUDE [Upload files with the portal](./includes/task-upload-file-to-asset-portal.md)]
