---
title: Azure Media Services Content Protection code samples
description: This article is a listing of code samples for Content Protection.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/17/2023
ms.author: inhenkel
---

# Azure Media Services Content Protection code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Content Protection.

## Upload and stream HLS and DASH with PlayReady and Widevine DRM

This sample demonstrates how to encode and stream using Widevine and PlayReady DRM.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFilesWithDRMSample/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFilesWithDRM/stream-files-with-drm-sample.py) |

## Deliver basic Playready DRM content protection and streaming

This sample demonstrates how to encode and stream using PlayReady DRM.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
|[.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/BasicPlayReady) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicPlayReady/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicPlayReady/basic-play-ready-helper.py) |

## Deliver basic Widevine DRM content protection and streaming

This sample demonstrates how to encode and stream using Widevine DRM.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/BasicWidevine) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicWidevine/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicWidevine/basic-widevine-helper.py) |

## Deliver basic AESClearKey content protection and streaming

This sample demonstrates how to dynamically encrypt your content with AES-128.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/BasicAESClearKey) | [NodeJS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFileWithAESClearKey/index.ts) | :small_blue_diamond: |

## Deliver offline Fairplay

This sample demonstrates how to dynamically encrypt your content with FairPlay DRM and play the content without requesting a license from license service.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/OfflineFairPlay) | :small_blue_diamond: | :small_blue_diamond: |

## Deliver offline PlayReady and Widevine

This sample demonstrates how to dynamically encrypt your content with PlayReady and Widevine DRM and play the content without requesting a license from license service.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/ContentProtection/OfflinePlayReadyAndWidevine) | :small_blue_diamond: | :small_blue_diamond: |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
