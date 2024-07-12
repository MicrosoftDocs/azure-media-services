---
title: Azure Media Services retirement guide
description: Azure Media Services retirement announcement.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 06/18/2024
ms.author: inhenkel
---

# Azure Media Services retirement guide

Azure Media Service announced its retirement on June 30, 2024 in June 2023. The Media Services retirement guide presents options available for you to migrate to solutions from the Microsoft partner ecosystem or other Azure services.

> [!Note]
> Migrate to a Microsoft partner solution for your on-demand encoding, live streaming, on-demand streaming, and content protection by 30 June 2024.  

**Action Required:** To prevent disruptions to your workloads, review this retirement guide for options to transition your workflow before 30 June 2024. After this date, Media Services will stop streaming on all your Azure Media Services accounts and your accounts will become read-only for approximately 90 days until they are automatically deleted.

A one-time 30-day extension until early August is offered on the Azure portal. Extend your account before your account becomes read-only to avoid interruptions. No further extension is possible.

Go to the Azure portal to check your account's expiration date and request the one-time extension.

## Migration guidance overview

Migrate your media workflows to one of the partner solutions listed below. Also included are links to System Integrators (SIs) that can help you with your transition from Azure Media Services. Partners and SI's are listed in alphabetical order.

### Partner solutions

Solutions from each of these partners are available in the Azure Marketplace. Each of these partners has migration guides available from the following links to use for transitioning from Media Services to the partner service.

- [Bitmovin](https://aka.ms/ams-bitmovin)
- [MediaKind](https://aka.ms/ams-mediakind)
- [Ravnur](https://aka.ms/ams-ravnur)

MediaKind and Bitmovin are available to our public cloud customers. Ravnur specializes in serving government customers. Their service is available in both Azure (Commercial) and Azure Government regions. For more information, please refer to their individual migration guides, which are available from the links above.

### China partner solutions

Use the links following links to learn more about our partner solutions in Azure China regions. 

- [Arcvideo 当虹科技](https://aka.ms/ams-arcvideo)
- [bopoda 博普达](https://aka.ms/ams-bopoda)

### System integrators (SIs)

The following SIs all have extensive experience in assisting customers with building media services solutions using both Azure Media Services and partners that are listed above. They can provide guidance or development work needed to facilitate your transition away from Azure Media Services.

- [Eyevinn](https://aka.ms/ams-eyevinn)
- [Southworks](https://aka.ms/ams-southworks)
- [WhDiYo](https://aka.ms/ams-whdiyo)

> [!IMPORTANT]
> This doesn't apply to China regions.

## Data migration options

Your existing Azure Media Services assets will remain in your Azure Storage containers even after your AMS account is deleted. Any Media Services metadata associated with these assets will become read-only for approximately 90 days after your account is deactivated. Be sure to export any necessary data before this time.

For customers in the public Azure regions, these are the data migration options available to you:

- **Bitmovin automatic migration**<br/>
    Bitmovin's solution enables customers to retain their existing non-DRM streaming URLs until June 30, 2025. The migration process involves transferring the metadata associated with your assets to Bitmovin, allowing them to continue streaming your content. No play update is required. For more details, refer to [Automatic migration to Bitmovin](azure-media-services-retirement-automatic-migration-bitmovin.md).
- **MediaKind**<br/>
    For regions where MediaKind is available. MediaKind can continue to stream your existing content in HLS/DASH with AES and DRM support (PlayReady, Widevine and FairPlay). Follow the [MediaKind migration guide](https://docs.mk.io/docs/migrate-your-ams-assets).
- **Ravnur**<br/>
    Ravnur's solution can be hosted in you Azure subscription to continue streaming existing AMS content in HLS/DASH. Follow the [Ravnur migration guide](https://docs.ravnur.com/hc/en-us/articles/19218387054994-RMS-Deployment-Guide).
- **Azure Media Services static migration**<br/>
    The AMS static migration tool allows you to transform your existing assets to stream directly from the storage location of you choosing using HLS/DASH. We recommend that you turn on CDN on the storage account to scale this solution. You will need to provision your own compute resources in the same region as your storage account for this migration.

    However, all existing URLs must be updated after this migration. Azure Media Player no longer supports this new format, so a player update will be required if you are using Azure Media Player.

    The AMS migration tool is available [here](https://github.com/Azure/azure-media-migration).

This table can help you determine the most suitable option.

| Option | Availability | Preserves existing URLs | Data move required | Streaming format | AES/DRM support | Player update required |
| --- | -------- | ----------------------- | ------------------ | ---------------- | --------------- | ---------------------- |
| Bitmovin<br/>Automatic Migration | All regions | Yes<br/>until June 30, 2025 | Not until<br/>June 30, 2025 | All supported by AMS | AES,<br/>DRM not supported | No |  
| Bitmovin<br/>Streams, VOD | 20+ regions | No | Yes | DASH/HLS | AES,<br/>Widevine<br/>FairPlay<br/>PlayReady | Yes | 
| MediaKind | 8 regions | URL structure maintained,<br/>host name must be updated | No | DASH/HLS<br/>Filter support | AES,<br/>Widevine<br/>FairPlay<br/>PlayReady | Yes |
| Ravnur | Everywhere<br/>Runs on your subscription | URL structure maintained,<br/>host name must be updated | No | DASH/HLS<br/>Filter support | AES,<br/>Widevine<br/>FairPlay<br/>PlayReady | Yes |
| AMS Static Migration | Everywhere | No | Yes | DASH/HLS | AES<br/>(You must run your own key delivery service) | Yes |

## Video and audio analysis migration

Media Services allows you to extract insights from your video audio files using audio and video analyzer presets. If you're currently using these presets, you'll need to migrate them to [Azure Video Indexer](/azure/azure-video-indexer/video-indexer-overview). Video Indexer provides more advanced capabilities in speech-to-text, translations, speaker identification, and more. Audio and video analysis capabilities from Video Indexer are available in multiple feature bundles; for information on available bundles and pricing, see [Pricing – Azure Video Analyzer](https://azure.microsoft.com/pricing/details/video-indexer/). To learn more about models available in these bundles, see [What is Azure Video Indexer?](/azure/azure-video-indexer/video-indexer-overview).

> [!IMPORTANT]
> Azure Video Indexer is not available in China Regions. Therefore, any audio analyzer preset usage in China regions will either need to migrate to [Azure AI Services](https://azure.microsoft.com/products/cognitive-services/) or to one of the China partners solutions such as [bopoda 博普达](https://aka.ms/ams-bopoda) that has similar capabilities.

### How Can I get started with Azure Video Indexer?

- [Learn how to get started with Azure Video Indexer](/azure/azure-video-indexer/video-indexer-get-started)
- [Learn additional information on impact of Media Services retirement for Video Indexer](https://aka.ms/vi-ams-retirement-announcement)

## Common questions about Azure Media Services retirement

### Why is Azure Media Services being retired?

This is a result of Microsoft focusing on strategic areas of secular growth and long-term competitiveness for the company. We’re also accelerating media services solutions from the Microsoft partner ecosystem across integrated solution vendors and system integrators to ensure that Azure users have access to a variety of high-quality media services solutions.

### What happens when my AMS account expires? 

On the Azure portal you will find your AMS account’s expiration date and time. Within approximately one of hour of the expiration time all running live events and streaming endpoints will be stopped. The AMS API allows all GET operations and will reject all PATCH, PUT or POST operations. The only exception is that we allow customers to update the CDN settings on streaming endpoints. Enabling CDN for streaming endpoints migrated to Bitmovin allows customers to preserve existing streaming URLs until June 30th, 2025.  

Approximately 90 days after the expiration time, your AMS account will be deleted. Remember to copy out any AMS data prior to that time. Bitmovin, MediaKind and other migration tools work best when asset information can still be queried. The AMS migration tool can work after account deletion, but you will lose all information about existing URLs.   

### Is Azure Video Indexer being retired?

No, Azure Video Indexer isn't part of the Media Services retirement. Although Video Indexer currently relies on a Media Services account as part of its workflow, this dependency will be eliminated before Media Services is retired on June 30, 2024. See the following for more information: [impact of Media Services retirement for Video Indexer](https://aka.ms/vi-ams-retirement-announcement).

### Do I still need to migrate from Media Services v2 APIs to v3 APIs?

No, you no longer need to migrate from Media Services v2 APIs to v3 APIs. Both v2 and v3 APIs will be retired simultaneously on 30 June 2024. The v2 APIs are not expected to work after your account expires.

### What will happen to customer data after the retirement date?

There are two types of data stored in Azure for Media Services: customer videos and associated files (for example, .ism, .ismc, and .mp4 files) that make up a Media Services asset, and Media Services account data. Customer videos and associated files are stored in the customer's Azure Storage account and will remain unaffected by the retirement of Media Services. However, all account data, including streaming endpoints, live events, and asset metadata, will be deleted as part of the retirement process, approximately 90 days after accounts are deactivated in July.

### Is Azure Media Player also being retired?

Yes, Azure Media Player will also be retired on 30 June 2024. All partners listed in the Media Services retirement guide have alternative video players available for customers to use. See [Media players for Media Services](player-media-players-concept.md) for other video player options.

### Will partner solutions be available in the same Azure regions as Media Services?

Partner solutions will be available in a more limited set of regions than Media Services. Refer to each partner's documentation pages for covered regions.

### Will partner solutions be available in Azure Government regions?

[Ravnur](https://aka.ms/ams-ravnur) is one partner that specializes in serving government customers and can support customers in any Azure Government region.

### Is creation of new Media Services accounts being blocked in all Azure regions?

Yes, the creation of new Media Services accounts is blocked in all Azure regions.

### How can I get migration help and support?

You can contact Media Services with questions or follow our updates by one of the following methods:

- [Microsoft Q & A](/answers/topics/azure-media-services.html)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-media-services), Tag questions with azure-media-services.
- Open a support ticket through the Azure portal.
