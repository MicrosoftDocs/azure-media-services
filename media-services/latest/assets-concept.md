---
title: Assets in Azure Media Services
description: Learn about what assets are and how they're used by Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 3/16/2022
ms.author: inhenkel
---

# Assets in Azure Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

In Azure Media Services, an [Asset](/rest/api/media/assets) is a core concept. It is where you input media (for example, through upload or live ingest), output media (from a job output), and publish media (for streaming).

An Asset is mapped to a blob container in the [Azure Storage account](storage-account-concept.md?amspage=assets-concept) and the files in the Asset are stored as block blobs in that container. Assets contain information about digital files stored in Azure Storage (including video, audio, images, thumbnail collections, text tracks, and closed caption files).

## Storage options

Media Services supports Blob tiers when the account uses General-purpose v2 (GPv2) storage. With GPv2, you can move files to [Cool or Archive storage](/azure/storage/blobs/access-tiers-overview). **Archive** storage is suitable for archiving source files when no longer needed (for example, after they've been encoded).

The **Archive** storage tier is only recommended for very large source files that have already been encoded and the encoding Job output was put in an output blob container. The blobs in the output container that you want to associate with an Asset and use to stream or analyze your content must exist in a **Hot** or **Cool** storage tier.

### Naming files/blobs within an asset

The names of files/blobs within an asset must follow both the [blob name requirements](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata) and the [NTFS name requirements](/windows/win32/fileio/naming-a-file). The reason for these requirements is the files can get copied from blob storage to a local NTFS disk for processing.

## Asset How-Tos and Tutorials

[Upload media for streaming or encoding](asset-upload-media-how-to.md?amspage=assets-concept)
[Create an asset](asset-create-asset-how-to.md?amspage=assets-concept)
