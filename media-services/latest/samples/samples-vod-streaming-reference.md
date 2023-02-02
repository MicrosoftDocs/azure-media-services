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

[!INCLUDE [net_samples_note](../includes/net_samples_note.md)]

## Upload and stream HLS and DASH

This sample shows you how to upload a local file or encoding from a source URL. It also shows you how to use storage SDK to download content, and stream to a player.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFilesSample/index.ts) |  :small_blue_diamond: |

## Upload a file and stream with Clear Key encryption

This sample shows you how to upload a local file, encode it with Content Aware Encoding, and stream it using AES Clear Key encryption with the Azure Media Player. It also demonstrates how to create a basic JWT token for playback of AES encrypted content in the browser.

| Node.JS | Python |
| ------- | ------ |
| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFileWithAESClearKey/index.ts) |  :small_blue_diamond: |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
