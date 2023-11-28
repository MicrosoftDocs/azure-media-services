---
title: Azure Media Services retirement guide
description: Azure Media Services retirement announcement.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 07/24/2023
ms.author: inhenkel
---

# Azure Media Services retirement guide

The Media Services retirement guide presents options available for you to migrate to solutions from the Microsoft partner ecosystem or other Azure services.

> [!Note]
> Migrate to a Microsoft partner solution for your on-demand encoding, live streaming, on-demand streaming, and content protection workflows and to Azure Video Indexer for your audio and video analysis workflows by 30 June 2024. Azure Media Services will be fully retired by this date.  

**Action Required:** To prevent disruptions to your workloads, review this retirement guide for options to transition your workflow before 30 June 2024. After this date, Media Services won’t be supported, and customers won’t have access to their Media Services accounts.

## Migration guidance overview

This section provides links to partner solutions that cover the breadth of Azure Media Services capabilities, except for audio and video analysis workflows, supported by [Azure Video Indexer](/azure/azure-video-indexer/video-indexer-overview). Also included are links to System Integrators (SIs) that can help you with your transition from Azure Media Services.

### Featured partner solutions

Solutions from each of these partners are available in the Azure Marketplace. Each of these partners has migration guides available from the following links to use for transitioning from Media Services to the partner service.

- [Harmonic](https://aka.ms/ams-harmonic)
- [MediaKind](https://aka.ms/ams-mediakind)
- [Bitmovin](https://aka.ms/ams-bitmovin)
- [Ravnur](https://aka.ms/ams-ravnur)

Harmonic and MediaKind are our featured partners, offering solutions that support dynamic packaging of existing Media Services content, eliminating the need for content to be reprocessed. In addition, they possess a wide range of media services capabilities that go beyond what is currently available with Azure Media Services. Ravnur specializes in serving government customers, and their service is available in both Azure (Commercial) and Azure Government regions. For more information, please refer to their individual migration guides, which are available from the links above.

> [!IMPORTANT]
> This doesn't apply to China regions.

### China partner solutions

This section provides links to our partners who offer solutions for migrating media services workflows in Azure China regions. Please refer to the links below for more information on their offerings.

- [bopoda 博普达](https://aka.ms/ams-bopoda)
- [Arcvideo 当虹科技](https://aka.ms/ams-arcvideo)


### System integrators (SIs)

The following SIs all have extensive experience in assisting customers with building media services solutions using both Azure Media Services and partners that are listed above. They can provide guidance or development work needed to facilitate your transition away from Azure Media Services.

- [Eyevinn](https://aka.ms/ams-eyevinn)
- [Southworks](https://aka.ms/ams-southworks)
- [WhDiYo](https://aka.ms/ams-whdiyo)

> [!IMPORTANT]
> This doesn't apply to China regions.

## Video and audio analysis migration

Media Services allows you to extract insights from your video audio files using audio and video analyzer presets. If you're currently using these presets, you'll need to migrate them to [Azure Video Indexer](/azure/azure-video-indexer/video-indexer-overview) Video Indexer provides more advanced capabilities in speech-to-text, translations, speaker identification, and more. Audio and video analysis capabilities from Video Indexer are available in multiple feature bundles; for information on available bundles and pricing, see [Pricing – Azure Video Analyzer](https://azure.microsoft.com/pricing/details/video-indexer/). To learn more about models available in these bundles, see [What is Azure Video Indexer?](/azure/azure-video-indexer/video-indexer-overview).

> [!NOTE]
> The retirement of Media Services Video Analyzer on 14 September 2023 that was previously announced is not changing due to Azure Media Services being fully retired. If you are using Media Services Video Analyzer, you will still need to migrate to Azure Video Indexer by 14 September 2023. See Media Services Video Analyzer retirement and migration for additional information.

> [!IMPORTANT]
> Azure Video Indexer is not available in China Regions. Therefore, any audio and video analyzer preset usage in China regions will either need to migrate to [Azure AI Services](https://azure.microsoft.com/products/cognitive-services/) or to one of the China partners solutions such as [bopoda 博普达](https://aka.ms/ams-bopoda) that has similar capabilities.

### How Can I get started with Azure Video Indexer?

- [Learn how to get started with Azure Video Indexer](/azure/azure-video-indexer/video-indexer-get-started)
- [Learn additional information on impact of Media Services retirement for Video Indexer](https://aka.ms/vi-ams-retirement-announcement)

## Common questions about Azure Media Services retirement

### What are the migration options for existing Media Services content?

Both [MediaKind](https://io.mediakind.com/) and [Harmonic](https://aka.ms/ams-harmonic) offer dynamic packaging of existing AMS content without requiring the content to be reprocessed. If you decide not to use this option, you can convert your Media Services assets to CMAF format with HLS and DASH manifests using the open-source [Azure Media Services Migration Tool](https://github.com/Azure/azure-media-migration). This tool allows you to stream content directly from Azure Storage. See the [tools readme](https://github.com/Azure/azure-media-migration/blob/main/README.md) for additional information.

### Why is Azure Media Services being retired?

This is a result of Microsoft focusing on strategic areas of secular growth and long-term competitiveness for the company. We’re also accelerating media services solutions from the Microsoft partner ecosystem across integrated solution vendors and system integrators to ensure that Azure users have access to a variety of high-quality media services solutions.

### Is Azure Video Indexer being retired?

No, Azure Video Indexer isn't part of the Media Services retirement. Although Video Indexer currently relies on a Media Services account as part of its workflow, this dependency will be eliminated before Media Services is retired on June 30, 2024. See the following for more information: [impact of Media Services retirement for Video Indexer](https://aka.ms/vi-ams-retirement-announcement).

### Do I still need to migrate from Media Services v2 APIs to v3 APIs?

No, you no longer need to migrate from Media Services v2 APIs to v3 APIs. We'll be sending out further communication to all customers who are still using v2 APIs to ensure they're aware of this change. Both v2 and v3 APIs will be retired simultaneously on 30 June 2024.

### What will happen to customer data after the retirement date?

There are two types of data stored in Azure for Media Services: customer videos and associated files (for example, .ism, .ismc, and .mp4 files) that make up a Media Services asset, and Media Services account data. Customer videos and associated files are stored in the customer's Azure Storage account and will remain unaffected by the retirement of Media Services. However, all account data, including streaming endpoints, live events, and asset metadata, will be deleted as part of the retirement process.

### Is Azure Media Player also being retired?

Yes, Azure Media Player will also be retired on 30 June 2024. All partners listed in the Media Services retirement guide have alternative video players available for customers to use. See [Media players for Media Services](player-media-players-concept.md) for other video player options.

### Will partner solutions be available in the same Azure regions as Media Services?

Partner solutions will be available in a more limited set of regions than Media Services. The featured partners, Harmonic and MediaKind, plan to provide coverage across North America, Europe, Asia Pacific, South America, Australia, and India. While they may not have full availability in these regions by June 30, 2023, they're working to expand their coverage in these areas.

### Will partner solutions be available in Azure Government regions?

Partner solutions will be available in Azure Government regions. [Ravnur](https://aka.ms/ams-ravnur) is one partner that specializes in serving government customers.

### Is creation of new Media Services accounts being blocked in all Azure regions?
Currently, the creation of new Media Services accounts is being blocked in a subset of Azure regions where Media Services is available. These regions are listed below:

| Geography            | Region Name                                                         | 
|----------------------|---------------------------------------------------------------------|
| Africa               | South Africa North, South Africa West                               | 
| Azure Government     | US Gov Texas                                                        |
| Canada               | Canada East                                                         | 
| China                | China East, China East 2, China North, China North 2, China North 3 | 
| France               | France South                                                        |
| Germany              | Germany North                                                       |
| India                | South India, West India                                             |
| Korea                | Korea South                                                         |
| Norway               | Norway East                                                         |
| United Arab Emirates | UAE Central, UAE North                                              |
| United Kingdom       | UK West                                                             |
| United States        | North Central US                                                    |

By the end of January 2024, Media Services account creation will be blocked in all regions. If you have an existing Media Services account, you can open a support ticket through the Azure Portal to enable account creation for a specific Azure subscription. Once enabled, you will be able to create new Media Services accounts in any Azure region where Media Services is available.

### How can I get migration help and support?

You can contact Media Services with questions or follow our updates by one of the following methods:

- [Microsoft Q & A](/answers/topics/azure-media-services.html)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-media-services), Tag questions with azure-media-services.
- Open a support ticket through the Azure portal.
