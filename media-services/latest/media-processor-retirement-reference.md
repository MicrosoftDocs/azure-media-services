---
title: Retired media processors
description: Over time, we enhance Media Service components and retire legacy components. This article helps you migrate your application from a legacy component to a current component.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 03/01/2023
ms.author: inhenkel
---

# Media processor retirement

![migration guide logo](./media/migration-guide/azure-media-services-logo-migration-guide.svg)

<hr color="#5ea0ef" size="10">

Over time, we enhance Media Service components and retire legacy components. This article helps you migrate your application from a legacy component to a current component.

> [!IMPORTANT]
> Although Azure Media Services is being retiree, there is no change to the media processor retirement timeline.

## Media processor retirement timeline

| **Media processor name** | **Retirement date** | **Status** | **Additional notes** |
| --- | --- | --- | --- |
| Azure Media Indexer 2 | January 1, 2020 | Retired | This media processor will be replaced by the [Media Services v3 AudioAnalyzerPreset Basic mode](analyze-video-audio-files-concept.md). For more information, see [Migrate from Azure Media Indexer 2 to Azure Video Indexer](../previous/migrate-indexer-v1-v2.md) (formerly Video Indexer). |
| Motion Detection | June 1, 2020| Retired | No replacement plans at this time. |
| Video Summarization |June 1, 2020| Retired | No replacement plans at this time.|
| Video Optical Character Recognition | June 1, 2020 | Retired | This media processor was replaced by Azure Video Indexer. Also, consider using [Azure Media Services v3 API](../latest/analyze-video-audio-files-concept.md). <br/>See [Compare Azure Media Services v3 presets and Video Indexer](/azure/azure-video-analyzer/video-analyzer-for-media-docs/compare-video-indexer-with-media-services-presets). |
| Face Detector | June 1, 2020 | Retired | This media processor was replaced by Azure Video Indexer. Also, consider using [Azure Media Services v3 API](analyze-video-audio-files-concept.md). <br/>See [Compare Azure Media Services v3 presets and Video Indexer](/azure/azure-video-analyzer/video-analyzer-for-media-docs/compare-video-indexer-with-media-services-presets). |
| Content Moderator | June 1, 2020 | Retired | This media processor was replaced by Azure Video Indexer. Also, consider using [Azure Media Services v3 API](analyze-video-audio-files-concept.md). <br/>See [Compare Azure Media Services v3 presets and Video Indexer](/azure/azure-video-analyzer/video-analyzer-for-media-docs/compare-video-indexer-with-media-services-presets). |
| Azure Media Indexer | March 1, 2023 | Retired | This media processor is replaced by the [Media Services v3 AudioAnalyzerPreset Basic mode](analyze-video-audio-files-concept.md). For more information, see [Migrate from Azure Media Indexer 2 to Azure Video Indexer](../previous/migrate-indexer-v1-v2.md) (formerly Video Indexer). |
| Video Analyzer preset (in v3 API) | Sept 14, 2023 | Planned |  As Microsoft’s [Responsible AI Standards](https://blogs.microsoft.com/on-the-issues/2022/06/21/microsofts-framework-for-building-ai-systems-responsibly/) outlines, Microsoft is committed to fairness, privacy, security, and transparency with respect to AI systems. To align with these standards, **Azure Media Services is retiring the [Video Analyzer preset](./analyze-video-audio-files-concept.md) on September 14, 2023**. This preset currently allows you to extract multiple video and audio insights from a video file. Customers can replace their current workflows using the more advanced feature set offered by [Azure Video Indexer](/azure/azure-video-indexer/concepts-overview)
|
| Media Encoder Premium Workflow | February 29, 2024 | Planned | The AMS v2 API no longer supports the Premium Encoder. If you previously used the workflow-based Premium Encoder for HEVC encoding, you should migrate to the [new v3 Standard Encoder](encode-media-encoder-standard-formats-reference.md) with HEVC encoding support. <br/> If you require advanced workflow features of the Premium Encoder, you're encouraged to start using an Azure advanced encoding partner from [Imagine Communications](https://imaginecommunications.com/), [Telestream](https://telestream.net), or [Bitmovin](https://bitmovin.com). |

## Migration guide

[Migration Guide introduction](migrate-v-2-v-3-migration-introduction.md)

[!INCLUDE [media-services-community](includes/media-services-community.md)]
