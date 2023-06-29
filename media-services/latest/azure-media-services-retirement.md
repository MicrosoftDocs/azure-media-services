---
title: Azure Media Services retirement guide
description: Azure Media Services retirement announcement.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 06/29/2023
ms.author: inhenkel
---

# Azure Media Services retirement guide

The Media Services retirement guide presents options available for you to migrate to solutions from the Microsoft partner ecosystem or other Azure services.

> [!Note]
> Migrate to a Microsoft partner solution for your on-demand encoding, live streaming, on-demand streaming, and content protection workflows and to Azure Video Indexer for your audio and video analysis workflows by 30 June 2024. Azure Media Services will be fully retired by this date.  

**Action Required:** To prevent disruptions to your workloads, review this retirement guide for options to transition your workflow before 30 June 2024. After this date, Media Services won’t be supported, and customers won’t have access to their Media Services accounts.

## Migration guidance overview

This section provides links to partner solutions that will cover the breadth of Azure Media Services capabilities, except for audio and video analysis workflows, which will be supported by [Azure Video Indexer](/azure/azure-video-indexer/video-indexer-overview). Also included are links to Independent Software Vendors (ISVs) that can help you with your transition from Azure Media Services.

### Featured partner solutions

Solutions from each of these partners are available in the Azure Marketplace. Each of these partners has migration guides, available from the following links, to use for transition from Media Services to the partner service

- [Harmonic](https://aka.ms/ams-harmonic)
- [MediaKind](https://io.mediakind.com/)

Both partners will support dynamic packaging of existing Media Services content, eliminating the need for content to be reprocessed. They possess a wide range of media services capabilities beyond what is currently available with Azure Media Services and will continue to add more capabilities and improvements for Azure customers in the future. For more information, please refer to their individual migration guides available from the above links.

### Other partner solutions

This section contains links to partners, who also offer solutions for migrating your media services workflows through the Azure Marketplace, as well as to Independent Software Vendors (ISVs). Refer to the links for their offerings below for further information.
Azure Marketplace offerings:

- [Bitmovin](https://bitmovin.com/azure-marketplace/)
- [Ravnur](https://aka.ms/ams-ravnur)

### ISVs

The following ISVs all have extensive experience in assisting customers with building media services solutions using both Azure Media Services and partners that are listed above. They can provide guidance or development work needed to facilitate your transition away from Azure Media Services.

- [Eyevinn](https://www.eyevinntechnology.se/)
- [Southworks](https://www.southworks.com/)
- [Whdyio](https://whdiyo.com/)

## Video and audio analysis migration

Media Services allows you to extract insights from your video audio files using audio and video analyzer presets. If you're currently using these presets, you'll need to migrate them to [Azure Video Indexer](/azure/azure-video-indexer/video-indexer-overview) Video Indexer provides more advanced capabilities in speech-to-text, translations, speaker identification, and more. Audio and video analysis capabilities from Video Indexer are available in multiple feature bundles; for information on available bundles and pricing, see [Pricing – Azure Video Analyzer](/pricing/details/video-indexer/). To learn more about models available in these bundles, see [What is Azure Video Indexer?](/azure/azure-video-indexer/video-indexer-overview).

> [!Note]
> The retirement of Media Services Video Analyzer on 14 September 2023 that was previously announced is not changing due to Azure Media Services being fully retired. If you are using Media Services Video Analyzer, you will still need to migrate to Azure Video Indexer by 14 September 2023. See Media Services Video Analyzer retirement and migration for additional information.

### How Can I get started with Azure Video Indexer?

- [Learn how to get started with Azure Video Indexer](/azure/azure-video-indexer/video-indexer-get-started)
- [Learn additional information on impact of Media Services retirement for Video Indexer](https://aka.ms/vi-ams-retirement-announcement)

## Common questions about Azure Media Services retirement

### Why is Azure Media Services being retired?

This is a result of Microsoft focusing on strategic areas of secular growth and long-term competitiveness for the company. We’re also accelerating media services solutions from the Microsoft partner ecosystem across integrated solution vendors and system integrators to ensure that Azure users have access to a variety of high-quality media services solutions.

### Is Azure Video Indexer being retired?

No, Azure Video Indexer isn't part of the Media Services retirement. Although Video Indexer currently relies on a Media Services account as part of its workflow, this dependency will be eliminated before Media Services is retired on June 30, 2024. See the following for more information: [impact of Media Services retirement for Video Indexer](https://aka.ms/vi-ams-retirement-announcement).

### Do I still need to migrate from Media Services v2 APIs to V3 APIs?

No, you no longer need to migrate from Media Services V2 APIs to V3 APIs. We'll be sending out further communication to all customers who are still using V2 APIs to ensure they're aware of this change. Both V2 and V3 APIs will be retired simultaneously on 30 June 2024.

### What will happen to customer data after the retirement date?

There are two types of data stored in Azure for Media Services: customer videos and associated files (for example, .ism, .ismc, and .mp4 files) that make up a Media Services asset, and Media Services account data. Customer videos and associated files are stored in the customer's Azure Storage account and will remain unaffected by the retirement of Media Services. However, all account data, including streaming endpoints, live events, and asset metadata, will be deleted as part of the retirement process.

### What migration options will be available for existing Media Services content?

Both [MediaKind](https://io.mediakind.com/) and [Harmonic](https://aka.ms/ams-harmonic) will offer dynamic packaging of existing AMS content without requiring the content to be moved to another location or reprocessed in most cases. If you don’t choose this option, we'll be releasing an open-source tool that will allow you to convert Media Services assets to CMAF format with HLS and DASH manifests, so that content can be directly streamed from Azure Storage. We'll provide an update in the Media Services retirement guide when this tool is available. 

### Is Azure Media Player also being retired?

Yes, Azure Media Player will also be retired on 30 June 2024. All partners listed in the Media Services retirement guide have alternative video players available for customers to use.

### Will partner solutions be available in the same Azure regions as Media Services?

Partner solutions will be available in a more limited set of regions than Media Services. The featured partners, Harmonic and MediaKind, plan to provide coverage across North America, Europe, Asia Pacific, South America, Australia, and India. While they may not have full availability in these regions by June 30, 2023, they're working to expand their coverage in these areas.

### Will partner solutions be available in Azure Government or China regions?

Partner solutions will be available in Azure Government regions. [Ravnur](https://aka.ms/ams-ravnur) is one partner that specializes in serving government customers. However, none of the partners listed in the Media Services retirement guide will have a marketplace offering available in the China region. We're working to provide further information on partner offerings in this region and will update the Media Services retirement guide accordingly.

### How can I get migration help and support?

You can contact Media Services with questions or follow our updates by one of the following methods:

- [Microsoft Q & A](/answers/topics/azure-media-services.html)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-media-services), Tag questions with azure-media-services.
- Open a support ticket through the Azure portal.
