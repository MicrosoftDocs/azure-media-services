---
title: Media Services v3 offline FairPlay Streaming for iOS
description: This article gives an overview and shows how to use Azure Media Services v3 to dynamically encrypt your HTTP Live Streaming (HLS) content with Apple FairPlay in offline mode.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 09/29/2022
ms.author: inhenkel
---

<!-- William Zhang -->

# Offline FairPlay Streaming for iOS with Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

 Azure Media Services provides a set of well-designed [content protection services](https://azure.microsoft.com/services/media-services/content-protection/) that cover:

- Microsoft PlayReady
- Google Widevine

    Widevine is a service provided by Google Inc. and subject to the terms of service and Privacy Policy of Google, Inc.
- Apple FairPlay Streaming - An Apple DRM technology that is only available for video transferred over HTTP Live Streaming (HLS) on iOS devices, in Apple TV, and in Safari on macOS.
- AES-128 encryption

Digital rights management (DRM)/Advanced Encryption Standard (AES) encryption of content is performed dynamically upon request for various streaming protocols. DRM license/AES decryption key delivery services also are provided by Media Services.

Offline-mode support is needed for the following scenarios:

* Playback when internet connection isn't available, such as during travel.
* Some content providers might disallow DRM license delivery beyond a country/region's border. If users want to watch content while traveling outside of the country/region, offline download is needed.
* In some countries/regions, internet availability and/or bandwidth is still limited. Users might choose to download first to be able to watch content in a resolution that is high enough for a satisfactory viewing experience. In this case, the issue typically isn't network availability but limited network bandwidth. Over-the-top (OTT)/online video platform (OVP) providers request offline-mode support.

> [!NOTE]
> Offline DRM is only billed for making a single request for a license when you download the content. Any errors are not billed.

## Prerequisites

Before you implement offline DRM for FairPlay on an iOS 10+ device:

* Review online content protection for FairPlay:

    - [Apple FairPlay license requirements and configuration](drm-fairplay-license-overview.md)
    - A .NET sample that includes configuration of online FPS streaming: [ConfigureFairPlayPolicyOptions](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/main/AMSV3Tutorials/EncryptWithDRM/Program.cs#L493)
* Obtain the FPS SDK from the Apple Developer Network. The FPS SDK contains two components:

    - The FPS Server SDK, which contains the Key Security Module (KSM), client samples, a specification, and a set of test vectors.
    - The FPS Deployment Pack, which contains the D function specification, along with instructions about how to generate the FPS Certificate, customer-specific private key, and Application Secret Key. Apple issues the FPS Deployment Pack only to licensed content providers.
    - The .der/.cer certificate files you receive as part of the generation of the FPS certificate contain a public key and can be made available to the client.  The private key (.pfx) should be secured in Azure Key Vault or another secure location.

### Sample

* Clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git.

    - Modify the code in [Encrypt with DRM using .NET](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/main/AMSV3Tutorials/EncryptWithDRM) to add FairPlay configurations.

![Offline FairPlay iOS App Streams](media/drm-offline-fairplay-for-ios-concept/offline-fairplay-ios-app-streams.png)

## Offline Fairplay questions

See [offline fairplay questions in the FAQ](frequently-asked-questions.yml).

[!INCLUDE [Store FairPlay Private Key in Azure KeyVault](./includes/task-drm-store-fairplay-key.md)]
