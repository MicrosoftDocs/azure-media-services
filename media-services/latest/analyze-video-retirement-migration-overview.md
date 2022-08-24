---
title: Media Services Video Analyzer migration
description: As Microsoft’s Responsible AI Standards outlines, Microsoft is committed to fairness, privacy, security, and
transparency with respect to AI systems. To align with these standards, Azure Media Services is retiring the Video Analyzer preset Analyze video and audiofiles on September 14, 2023. This preset currently allows you to extract multiple video and audio insights from a video file. Customers can replace their current workflows using the more advanced feature set offered by Azure Video Indexer.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 08/24/2022
ms.author: inhenkel
---

# Media Services Video Analyzern retirement and migration

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Executive summary

As Microsoft’s [Responsible AI Standards](https://blogs.microsoft.com/on-the-issues/2022/06/21/microsofts-framework-for-building-ai-systems-responsibly/) outlines, Microsoft is committed to fairness, privacy, security, and
transparency with respect to AI systems. To align with these standards, Azure Media Services is retiring the [Video Analyzer preset](analyze-video-audio-files-concept.md) on September 14, 2023. This preset currently allows you to extract multiple video and audio insights from a video file. Customers can replace their current workflows using the more advanced feature set offered by [Azure Video Indexer](/azure/azure-video-indexer/concepts-overview).

## Comparison between current vs new replacement

Video Indexer provides an enhanced list of supported features that the Media Services preset does not support. The following table details the differences. For more information, see [Comparison of Azure Video Indexer and Azure Media Services v3 presets](/azure/azure-video-indexer/compare-video-indexer-with-media-services-presets).

| **Feature** | **Azure Video Indexer APIs** | **Video Analyzer Preset in Media Services v3 APIs** |
|-------------|------------------------------|-----------------------------------------------------|
| **Media Insights** | [Enhanced](/azure/azure-video-indexer/video-indexer-output-json-v2) | [Fundamentals](/azure/media-services/latest/analyze-video-audio-files-concept) |
| **Experiences**    | See the full list of supported features: [Overview](/azure/azure-video-indexer/video-indexer-overview) | Returns video insights only |
| **Billing** | [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/#analytics) is the same  | [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/#analytics) is the same |
| **Compliance**          | For the most current compliance updates, see [Azure Compliance Offerings.pdf](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942/file/178110/23/Microsoft%20Azure%20Compliance%20Offerings.pdf) and search for "Azure Video Indexer" to determine if it complies with a certificate of interest. | For the most current compliance updates, see [Azure Compliance Offerings.pdf](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942/file/178110/23/Microsoft%20Azure%20Compliance%20Offerings.pdf) and search for "Media Services" to determine if it complies with a certificate of interest. |
| **Free Trial** | East US | Not available |
| **Region availability** | See [Cognitive Services availability by region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services) Note that this is fewer regions than AMS, so this is a region reduction currently | See [Media Services availability by region](https://azure.microsoft.com/global-infrastructure/services/?products=media-services). |

## Migration steps

Refer to the following documents by Video Indexer on how to index videos:

- [Upload and index videos with Azure Video Indexer](/azure/azure-video-indexer/upload-index-videos?tabs=With-classic-account)
- [Use the Azure Video Indexer API](/azure/azure-video-indexer/video-indexer-use-apis)
- [Examine the Azure Video Indexer output](/azure/azure-video-indexer/video-indexer-output-json-v2)

## Microsoft Q&A

If you have further questions, please go to [Microsoft Q&A](https://aka.ms/azureqa), the community support channel to get
answers to technical questions.
