---
title: Streaming Policies in Azure Media Services
description: This article gives an explanation of what Streaming Policies are, and how they are used by Azure Media Services.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Streaming Policies

In Azure Media Services v3, [Streaming Policies](/rest/api/media/streamingpolicies) enable you to define streaming protocols and encryption options for your [Streaming Locators](stream-streaming-locators-concept.md?stream-streaming-policy-concept). Media Services v3 provides some predefined Streaming Policies so that you can use them directly for trial or production.

The currently available predefined Streaming Policies:

- **Predefined_DownloadOnly**. For allowing downloading only.
- **Predefined_ClearStreamingOnly**. For allowing clear streaming only.
- **Predefined_DownloadAndClearStreaming**. For allowing both downloading and clear streaming.
- **Predefined_ClearKey**. For allowing HLS/DASH/Smooth encrypted with envelopeEncryption with Media Services issuing the content key.
- **Predefined_MultiDrmCencStreaming**. For allowing streaming with DASH/Smooth encrypted with `commonEncryptionCenc` with Media Services issuing the PlayReady and Widevine licenses.
- **Predefined_MultiDrmStreaming**. For allowing streaming with DASH/Smooth encrypted with `commonEncryptionCenc` with Media Services issuing the PlayReady and Widevine licenses, or for allowing streaming with HLS encrypted with `commonEncryptionCbcs` with Media Services issuing the FairPlay license.
- If none of the above meets your needs, create a new streaming policy.

> [!IMPORTANT]
> - Properties of **Streaming Policies** that are of the Datetime type are always in UTC format.
> - You should design a limited set of policies for your Media Service account and reuse them for your Streaming Locators whenever the same options are needed. For more information, see [Quotas and limits](limits-quotas-constraints-reference.md?stream-streaming-policy-concept).

If encrypting your content, you need to create a [Content Key Policy](drm-content-key-policy-concept.md?stream-streaming-policy-concept).

If you have special requirements (for example, if you want to specify different protocols, need to use a custom key delivery service, or need to use an unencrypted audio track), you can [create](/rest/api/media/streamingpolicies/create) a custom Streaming Policy.

## Clear Key Common Encryption (CENC)

A **Content Key Policy** is not needed for unencrypted streaming or downloading. CENC allows you to have common encryption without digital rights management for when you need encryption but your player doesn't support AES envelope encryption.

Players that allow CENC encryption include:

- dash.js from version 4.5.0
- Shaka player from v4.0.0 (2022-04-30)
- Android’s Exoplayer from version r2.18.1
- Bitmovin
- Theo Player

## Filtering, ordering, paging

See [Filtering, ordering, paging of Media Services entities](filter-order-page-entities-how-to.md?stream-streaming-policy-concept).

[!INCLUDE [media-services-community](includes/media-services-community.md)]
