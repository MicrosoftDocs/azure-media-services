---
title: Azure Media Services Analytics code samples
description: This article is a listing of code samples for Analytics.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/24/2023
ms.author: inhenkel
---

# Azure Media Services Analytics code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Analytics.

For more video analytics, try Azure Video Indexer. Azure Video Indexer is a cloud application, part of Azure Applied AI Services, built on Azure Media Services and Azure Cognitive Services (such as the Face, Translator, Computer Vision, and Speech). It enables you to extract the insights from your videos using Azure Video Indexer video and audio models. For more information about using Azure Video Indexer, see the [Azure Video Indexer](/azure/azure-video-indexer/video-indexer-overview) documentation.

## Use basic Audio Analytics with per-job language override

This sample illustrates how to create a audio analyzer transform using the basic mode. It also shows how you can override the preset language on a per-job basis to avoid creating a transform for every language. It also shows how to upload a media file to an input asset, submit a job with the transform and download the results for verification.

| &#32; | &#32; | &#32; |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/AudioAnalytics/AudioAnalyzer) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/AudioAnalytics/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/AudioAnalytics/audio-analytics-helper.py) |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
