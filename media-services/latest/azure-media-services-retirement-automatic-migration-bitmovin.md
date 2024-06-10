---
title: Automatic migration to Bitmovin
description: One of our Azure partners, Bitmovin, allows you to stream AMS content without changing the streaming URLs until June 30, 2025. To automatically migration to Bitmovin, subscribe to the Bitmovin product from the Azure Marketplace and then follow the instructions provided in the Bitmovin portal.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 06/10/2024
ms.author: inhenkel
---

# Automatic migration to Bitmovin

> [!IMPORTANT]
> This doesn't apply to China regions.

One of our Azure partners, Bitmovin, allows you to stream AMS content without changing the streaming URLs until June 30, 2025. To automatically migration to Bitmovin, subscribe to the Bitmovin product from the Azure Marketplace and then follow the instructions provided in the Bitmovin portal.

## Prerequisites

To successfully migrate AMS content streaming to Bitmovin, ensure the following requirements are met:

1. Digital Rights Management (DRM) protection for streaming (FairPlay, PlayReady, or Widevine) isn't being used.
1. Content Distribution Network (CDN) is enabled for your streaming endpoints.

## Details

After you grant the necessary permissions to Bitmovin, the migration process will copy information about AMS assets using the AMS APIs. Bitmovin then provisions resources that provide the equivalent functionality as your AMS streaming endpoint.

You can verify that Bitmovin can stream your content by loading Bitmovin's streaming URLs in your existing media player. To construct these URLs, replace the hostname portion of your AMS streaming URLs with Bitmovin's origin hostname.

Once you verify that streaming works as expected, you can update the CDN endpoint's origin in the Azure portal. This change requests data from Bitmovin's origin instead of the AMS streaming endpoint. Once complete, all exsiting streaming URLs are preserved. These URLs will continue to work until June 30, 2025.

For more information, see [Bitmovin's migration guide](https://developer.bitmovin.com/streams/docs/azure-media-services-migration-guide).
