---
title: Content Key Policies in Media Services - Azure
description: This article gives an explanation of what Content Key Policies are, and how they are used by Azure Media Services.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Content Key Policies

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

With Media Services, you can deliver your live and on-demand content encrypted dynamically with Advanced Encryption Standard (AES-128) or any of the three major digital rights management (DRM) systems: Microsoft PlayReady, Google Widevine, and Apple FairPlay. Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses to authorized clients. FairPlay Streaming is an Apple technology that is only available for video transferred over HTTP Live Streaming (HLS) on iOS devices, in Apple TV, and in Safari on macOS.

To specify encryption options on your stream, you need to create a [Streaming Policy](stream-streaming-policy-concept.md) and associate it with your [Streaming Locator](stream-streaming-locators-concept.md). You create the [Content Key Policy](/rest/api/media/contentkeypolicies) to configure how the content key (that provides secure access to your [Assets](assets-concept.md)) is delivered to end clients. You need to set the requirements (restrictions) on the Content Key Policy that must be met in order for keys with the specified configuration to be delivered to clients. The content key policy is not needed for clear streaming or downloading.

In most cases, the content key policy is associated with a [Streaming Locator](stream-streaming-locators-concept.md). When creating a custom streaming policy for advanced scenarios, you can specify the content key policy inside of a [Streaming Policy](stream-streaming-policy-concept.md).

## Best practices and considerations

> [!IMPORTANT]
> Please review the following recommendations.

* You should design a limited set of policies for your Media Service account and reuse them for streaming locators whenever the same options are needed. For more information, see [Quotas and limits](limits-quotas-constraints-reference.md).
* Content key policies are updatable. It can take up to 15 minutes for the key delivery caches to update.

   By updating the policy, you are overwriting your existing CDN cache which could cause playback issue for customers that are using cached content.
* Don't create a new content key policy for each asset. The main benefits of sharing the same content key policy between assets that need the same policy options are:

   * It's easier to manage a small number of policies.
   * If you need to make updates to the content key policy, the changes go into effect on all new license requests almost right away.
* If you do need to create a new policy, you have to create a new streaming locator for the asset.
* It's recommended to let Media Services autogenerate the content key.

   Typically, you would use a long-lived key and check for the existence of the content key policy with [Get](/rest/api/media/contentkeypolicies/get). To get the key, call a separate action method to get secrets or credentials.

## Filtering, ordering, paging

See [Filtering, ordering, paging of Media Services entities](filter-order-page-entities-how-to.md).

Widevine is a service provided by Google Inc. and subject to the terms of service and Privacy Policy of Google, Inc.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
