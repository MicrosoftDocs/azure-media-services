---
title: Configure offline PlayReady streaming
description: This article shows how to configure your Azure Media Services v3 account for streaming PlayReady for Windows 10 offline.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 09/29/2022
ms.author: inhenkel
---

<!-- William Zhang -->
<!-- Removed dependencies on external resources 7/13/2022 -IH -->
<!-- Removed .NET code from article, plus editing 9/29/2022 -IH -->

# Offline PlayReady Streaming for Windows 10 with Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Azure Media Services supports offline download and playback with DRM protection. This article describes using offline PlayReady for Windows 10/PlayReady clients. You can read about the offline mode support for iOS/FairPlay and Android/Widevine devices in the following articles:

- [Offline FairPlay Streaming for iOS](drm-offline-fairplay-for-ios-concept.md)
- [Offline Widevine Streaming for Android](drm-offline-widevine-for-android.md)

> [!NOTE]
> Offline DRM is only billed for making a single request for a license when you download the content. Any errors are not billed.

* Your viewers might need to download content onto their phone or tablet for playback when they are disconnected from the Internet.
* In some countries/regions, Internet availability and/or bandwidth is still limited. Users may choose to download content to watch it in higher resolutions.
* Some content providers may disallow DRM license delivery beyond a country/region's border. If a user needs to travel abroad and still wants to watch content, offline download is needed.

The smooth streaming ([PIFF](/iis/media/smooth-streaming/protected-interoperable-file-format)) file format with H264/AAC has a binding with PlayReady (AES-128 CTR). The smooth streaming .ismv file, assuming audio is muxed in video, is itself an fMP4 and can be used for playback. If smooth streaming content goes through PlayReady encryption, each .ismv file becomes a PlayReady protected MP4 fragment. You can choose an .ismv file with the preferred bitrate and rename it as .mp4 for download.

There are two options for hosting the PlayReady protected MP4 for progressive download:

1. You can put the MP4 in the same container/media service asset and use Azure Media Services streaming endpoint for progressive download.
1. You can use the SAS URL for progressive download directly from Azure Storage.

You can use two types of PlayReady license delivery:

1. PlayReady license delivery service in Azure Media Services
1. PlayReady license servers hosted anywhere.

To obtain a PlayReady license with the AMS delivery service, see the [Media Services v3 with PlayReady license template](drm-playready-license-template-concept.md).

For playback testing, you can use a Universal Windows Application on Windows 10. In [Windows 10 Universal samples](https://github.com/Microsoft/Windows-universal-samples), there is a basic player sample called [Adaptive Streaming Sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AdaptiveStreaming). Add the code for choosing the downloaded video and use it as the source, instead of the adaptive streaming source.
