---
title: Streaming Policies in Azure Media Services
description: This article gives an explanation of what Streaming Policies are, and how they are used by Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 3/16/2022
ms.author: inhenkel
---

# Streaming Policies

In Azure Media Services v3, [Streaming Policies](/rest/api/media/streamingpolicies) enable you to define streaming protocols and encryption options for your [Streaming Locators](stream-streaming-locators-concept.md). Media Services v3 provides some predefined Streaming Policies so that you can use them directly for trial or production.

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
> - You should design a limited set of policies for your Media Service account and reuse them for your Streaming Locators whenever the same options are needed. For more information, see [Quotas and limits](limits-quotas-constraints-reference.md).


If encrypting your content, you need to create a [Content Key Policy](drm-content-key-policy-concept.md), the **Content Key Policy** is not needed for clear streaming or downloading.

If you have special requirements (for example, if you want to specify different protocols, need to use a custom key delivery service, or need to use a clear audio track), you can [create](/rest/api/media/streamingpolicies/create) a custom Streaming Policy.

## Get a Streaming Policy definition

If you want to see the definition of a Streaming Policy, use [Get](/rest/api/media/streamingpolicies/get) and specify the policy name. For example:

### REST

Request:

```
GET https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contoso/providers/Microsoft.Media/mediaServices/contosomedia/streamingPolicies/clearStreamingPolicy?api-version=2018-07-01
```

Response:

```
{
  "name": "clearStreamingPolicy",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contoso/providers/Microsoft.Media/mediaservices/contosomedia/streamingPolicies/clearStreamingPolicy",
  "type": "Microsoft.Media/mediaservices/streamingPolicies",
  "properties": {
    "created": "2018-08-08T18:29:30.8501486Z",
    "noEncryption": {
      "enabledProtocols": {
        "download": true,
        "dash": true,
        "hls": true,
        "smoothStreaming": true
      }
    }
  }
}
```

## Filtering, ordering, paging

See [Filtering, ordering, paging of Media Services entities](filter-order-page-entities-how-to.md).
