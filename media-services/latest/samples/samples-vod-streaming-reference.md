---
title: Azure Media Services VOD Streaming code samples
description: This article is a listing of code samples for VOD Streaming.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/02/2023
ms.author: inhenkel
---

# Azure Media Services VOD Streaming code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for VOD Streaming.

## Upload and stream HLS and DASH

This sample shows you how to upload a local file or encoding from a source URL. It also shows you how to use storage SDK to download content, and stream to a player.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Streaming/StreamHLSAndDASH) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFilesSample/index.ts) |  [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFilesSample/stream-files-helper.py) |

## Upload a file and stream with Clear Key encryption

This sample shows you how to upload a local file, encode it with Content Aware Encoding, and stream it using AES Clear Key encryption with the Azure Media Player. It also demonstrates how to create a basic JWT token for playback of AES encrypted content in the browser.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFileWithAESClearKey/index.ts) |  [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFilesWithDRM/stream-files-with-drm-helper.py) |

## Stream an existing single bitrate MP4 files with HLS or DASH

This sample demonstrates how to dynamically package VOD content from an existing pre-encoded MP4 file (or set of ABR encoded Mp4s) and stream with HLS/DASH.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Streaming/StreamExistingMp4) | :small_blue_diamond: | :small_blue_diamond: |

## Use dynamic packaging for VOD content with filters

This sample demonstrates how to filter content using asset and account filters.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/Streaming/AssetFilters) | :small_blue_diamond: | :small_blue_diamond: |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
