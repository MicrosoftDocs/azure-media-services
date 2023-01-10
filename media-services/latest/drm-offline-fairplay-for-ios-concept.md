---
title: Media Services v3 offline FairPlay Streaming for iOS
description: This article gives an overview and shows how to use Azure Media Services v3 to dynamically encrypt your HTTP Live Streaming (HLS) content with Apple FairPlay in offline mode.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 01/09/2023
ms.author: inhenkel
ms.custom: engagement-fy23
---

<!-- William Zhang -->

# Offline FairPlay Streaming for iOS with Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

 Azure Media Services provides a set of well-designed [content protection services](https://azure.microsoft.com/services/media-services/content-protection/) for Microsoft PlayReady, Google Widevine<sup>*</sup>, Apple FairPlay Streaming, and AES-128 encryption.

> [!NOTE]
> Offline DRM is only billed for making a single request for a license when you download the content. Any errors are not billed.

## Prerequisites

Before you implement offline DRM for FairPlay on an iOS 10+ device:

- Read [Apple FairPlay license requirements and configuration](drm-fairplay-license-overview.md)
- Obtain the FPS SDK from the Apple Developer Network. The FPS SDK contains two components:
    - The FPS Server SDK, which contains the Key Security Module (KSM), client samples, a specification, and a set of test vectors.
    - The FPS Deployment Pack, which contains the D function specification, along with instructions about how to generate the FPS Certificate customer-specific private key, and Application Secret Key. Apple issues the FPS Deployment Pack only to licensed content providers.
- The .der/.cer certificate files you receive as part of the generation of the FPS certificate contain a public key and can be made available to the client.  The private key (.pfx) should be secured in Azure Key Vault or another secure location.

[!INCLUDE [Store FairPlay Private Key in Azure KeyVault](./includes/task-drm-store-fairplay-key.md)]

## Clone the sample

Clone the Media Services .Net samples.

`git clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git`

## Modify the code

Modify the code in [Encrypt with DRM using .NET](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/main/AMSV3Tutorials/EncryptWithDRM) to add FairPlay configurations.

<sup>*</sup> Widevine is a service provided by Google Inc. and subject to the terms of service and Privacy Policy of Google, Inc.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
