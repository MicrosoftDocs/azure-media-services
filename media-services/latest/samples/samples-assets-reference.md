---
title: Azure Media Services Assets code samples
description: This article is a listing of code samples for Assets.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/24/2023
ms.author: inhenkel
---

# Azure Media Services Assets code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Assets.

## List assets

This is a basic example of how to connect and list assets.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/HelloWorld-ListAssets/list-assets.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/list-assets-filtered.py) |

## Get the storage container from an asset

This sample demonstrates how to find the Azure storage account container used to store the contents of this asset. This can be used to then edit sources, modify, or copy contents using the Azure storage SDK library.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/get-container-from-asset.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/get-container-from-asset.py) |

## List assets using filters

This sample shows you how to use filters in your list assets calls to find assets by date and order them.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-assets-filtered.ts) |  [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/list-assets-filtered.py) |

## List the streaming locators on an asset using filters

This sample shows you how to use filters to list the streaming locators attached to your assets.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-assets-filtered.ts) |  Python not yet available |

## List tracks in an asset

This sample shows you how to use the tracks collection to list all of the track names and track types (audio, video, or text) available on an asset

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-tracks-in-asset.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/list-tracks-in-asset-helper.py) |

## Add a WebVTT/IMSC1/TTML subtitle or caption to an existing asset

This sample shows you how to use the Tracks API on an Asset to add a new WebVTT or TTML/IMSC1 text profile caption or subtitle to an existing asset.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/add-WebVTT-tracks.ts) |  Python not yet available |

## Add an additional audio track to an existing asset using the tracks API

This sample shows you how to use the Tracks API on an Asset to add an additional audio language or descriptive audio track to an existing asset. This sample demonstrates how to upload, encode using content aware encoding, and then late bind an additional audio track for a new language to the asset.

| &#32; | &#32; |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/add-audio-language-track.ts) |  [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/add-audio-language-track-helper.py) |

## Asset management with .NET

The sample for .NET contains the methods listed above in one script.

[Asset Management with .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Assets/AssetManagement)

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
