---
title: Captions, subtitles and text tracks
description: You can provide captions, subtitles and other text tracks to the client player. This article discusses captions and subtitle formats.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 09/22/2022
ms.author: inhenkel
---

# Captions, subtitles and text tracks

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

You can provide captions, subtitles and other text tracks to the client player. This article discusses captions and subtitle formats.

[!INCLUDE [captions-subtitles-text-track-description](includes/captions-subtitles-text-track-description.md)]

The following caption/subtitle formats are supported by Media Services

<!-- captions -->

[!INCLUDE [reference-closed-captioning-ad-insertion-table](includes/reference-closed-captioning-ad-insertion-table.md)]

[!INCLUDE [warning-captions-encryption](includes/warning-captions-encryption.md)]

## Text tracks

Media Services allows you to provide text tracks in WebVTT or TTML format. You can update the manifest file to [tell the player about the text tracks with the portal](amp-captions-tutorial.md) or with the Tracks API available as REST or with the SDKs.

See the [Tracks API article](tracks-concept.md) for more information about updating asset tracks programmatically.

## How-tos, tutorials and quickstarts

[Use WebVTT files with Azure Media Services and Azure Media Player](amp-captions-tutorial.md) with the portal.
