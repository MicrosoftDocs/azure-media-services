---
title: Packaging and delivery migration guidance
description: This article is gives you scenario based guidance for packaging and delivery that will assist you in migrating from Azure Media Services v2 to v3.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 06/29/2023
ms.author: inhenkel
---

# Packaging and delivery scenario-based migration guidance

![migration guide logo](./media/migration-guide/azure-media-services-logo-migration-guide.svg)

<hr color="#5ea0ef" size="10">

![migration steps 2](./media/migration-guide/steps-4.svg)

[!INCLUDE [migration-no-longer-necessary](includes/migration-no-longer-necessary.md)]

This article gives you scenario-based guidance for packaging and delivery that will assist you in migrating from Azure Media Services v2 to v3.

Major changes to the way content is published in v3 API. The new publishing model is simplified and uses fewer entities to create a Streaming Locator. The API reduced down to just two entities vs. the four entities previously required. Content Key Policies and Streaming Locators now replace the need for `ContentKeyAuthorizationPolicy`, `AssetDeliveryPolicy`, `ContentKey`, and `AccessPolicy`.

## Packaging and delivery in v3

1. Create [content key policies](drm-content-key-policy-concept.md).
1. Create [streaming locators](stream-streaming-locators-concept.md) and get the streaming paths.
    1. Configure the streaming locator for a [DASH](encode-dynamic-packaging-concept.md#deliver-dash) or [HLS](encode-dynamic-packaging-concept.md#deliver-hls) player.

See publishing concepts, tutorials and how to guides below for specific steps.

## Will v2 streaming locators continue to work after February 2024?

Streaming locators created with v2 API will continue to work after our v2 API is turned off. Once the Streaming Locator data is created in the Media Services backend database, there is no dependency on the v2 REST API for streaming. We will not remove v2 specific records from the database when v2 is turned off in February 2024.

There are some properties of assets and locators created with v2 that cannot be accessed or updated using the new v3 API. For example, v2 exposes an **Asset Files** API that does not have an equivalent feature in the v3 API. Often this is not a problem for most of our customers, since it is not a widely used feature and you can still stream old locators and delete them when they are no longer needed.

After migration, you should avoid making any calls to the v2 API to modify streaming locators or assets.

## Publishing concepts, tutorials and how to guides

### Concepts

- [Dynamic packaging in Media Services v3](encode-dynamic-packaging-concept.md)
- [Filters](filters-concept.md)
- [Filter your manifests using Dynamic Packager](filters-dynamic-manifest-concept.md)
- [Streaming Endpoints (Origin) in Azure Media Services](stream-streaming-endpoint-concept.md)
- [Stream content with CDN integration](stream-scale-streaming-cdn-concept.md)
- [Streaming Locators](stream-streaming-locators-concept.md)

[!INCLUDE [media-services-community](includes/media-services-community.md)]
