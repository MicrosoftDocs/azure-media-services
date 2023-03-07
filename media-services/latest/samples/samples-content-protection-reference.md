---
title: Azure Media Services Content Protection code samples
description: This article is a listing of code samples for Content Protection.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 03/07/2023
ms.author: inhenkel
---

# Azure Media Services Content Protection code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Content Protection.

## Basic content protection

### Deliver basic AESClearKey content protection and streaming

This sample demonstrates how to dynamically encrypt your content with AES-128.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/BasicAESClearKey) | [NodeJS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFileWithAESClearKey/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFileWithAESClearKey/stream-files-with-aes-clear-key-helper.py) |

### Deliver basic Playready DRM content protection and streaming

This sample demonstrates how to encode and stream using PlayReady DRM.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
|[.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/BasicPlayReady) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicPlayReady/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicPlayReady/basic-play-ready-helper.py) |

### Deliver basic Widevine DRM content protection and streaming

This sample demonstrates how to encode and stream using Widevine DRM.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/BasicWidevine) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicWidevine/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicWidevine/basic-widevine-helper.py) |

## Combined content protection

### Upload and stream HLS and DASH with PlayReady and Widevine DRM

This sample demonstrates how to encode and stream using Widevine and PlayReady DRM.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
| not yet available | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFilesWithDRMSample/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFilesWithDRM/stream-files-with-drm-sample.py) |

## Offline content protection

### Deliver offline Fairplay

This sample demonstrates how to dynamically encrypt your content with FairPlay DRM and play the content without requesting a license from license service.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/OfflineFairPlay) | Node.JS not yet available | Python not yet available |

### Deliver offline PlayReady and Widevine

This sample demonstrates how to dynamically encrypt your content with PlayReady and Widevine DRM and play the content without requesting a license from license service.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/OfflinePlayReadyAndWidevine) | Node.JS not yet available | Python not yet available |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
