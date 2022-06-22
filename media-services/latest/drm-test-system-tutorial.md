---
title: Create a test content protection system
description: This article shows you how to create a content protection system for testing digital rights management.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 06/22/2022
ms.author: inhenkel
---

# Create a test content protection system

This article shows you how to create a content protection system for testing digital rights management (DRM).

## Main components of a content protection system

To successfully complete your content protection system, fully understand the scope of the effort by testing a proof of concept content protection system.

There are three parts to implement for your testing system:

1. Application code
1. A player with an AES or DRM client
1. A security token service

### Application code

The [DRM sample](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/main/AMSV3Tutorials/EncryptWithDRM/Program.cs) shows you how to implement a multi-DRM system with Media Services v3 by using .NET. It also shows you how to use the Media Services license/key delivery service.

You can encrypt each asset with multiple encryption types (AES-128, PlayReady, Widevine, FairPlay).

The sample shows you how to create and configure a [content key policy](drm-content-key-policy-concept.md), create a [streaming locator](stream-streaming-locators-concept.md) that's configured to stream the encrypted asset, create a test token, and build a streaming URL.

There are additional content protection samples available for Node.JS and Python:

| **Node.JS** | **Python** | Description |
|---|---| ---|
|[Node.JS Upload and stream HLS and DASH with PlayReady and Widevine DRM](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFilesWithDRMSample/index.ts)|[Python Upload and stream HLS and DASH with PlayReady and Widevine DRM](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFilesWithDRM/stream-files-with-drm-sample.py)| Demonstrates how to encode and stream using Widevine and PlayReady DRM |
|[Node.JS Basic Playready DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicPlayready/index.ts)|[Python Basic Playready DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicPlayReady/basic-play-ready.py)| Demonstrates how to encode and stream using PlayReady DRM |
|[Node.JS Basic Widevine DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicWidevine/index.ts)| [Python Basic Widevine DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicWidevine/basic-widevine.py) | Demonstrates how to encode and stream using Widevine DRM |

### Player with an AES or DRM client

A video player application based on a player SDK (either native or browser-based) that meets the following requirements:

* The player SDK supports the needed DRM clients.
* The player SDK supports the required streaming protocols: Smooth, DASH, and/or HTTP Live Streaming (HLS).
* The player SDK can handle passing a JWT token in a license acquisition request.

You can use the [Azure Media Player](https://aka.ms/azuremediaplayer) or use the [Azure Media Player API](https://amp.azure.net/libs/amp/latest/docs/) to create a player for testing. Use the [Azure Media Player ProtectionInfo API](https://amp.azure.net/libs/amp/latest/docs/) to specify which DRM technology to use on different DRM platforms.

To test AES or CENC (Widevine and/or PlayReady) encrypted content with the Azure Media Player, make sure that you select **Advanced options** and check your encryption options.

If you want to test FairPlay encrypted content, use [this test player](https://aka.ms/amtest). The player supports Widevine, PlayReady, and FairPlay DRMs, along with AES-128 clear key encryption.

Choose the correct browser to test each:

* Chrome, Opera, or Firefox for Widevine.
* Microsoft Edge for PlayReady.
* Safari on macOS for FairPlay.

### Security token service

A security token service (STS) issues JWT as the access token for back-end resource access. You can use the Azure Media Services license/key delivery service. An STS has to define the following things:

* Issuer and audience (or scope).
* Claims, which are dependent on business requirements in content protection.
* Symmetric or asymmetric verification for signature verification.
* Key rollover support (if necessary).

You can use [this STS tool](https://openidconnectweb.azurewebsites.net/DRMTool/Jwt) to test the STS. It supports all three types of verification keys: symmetric, asymmetric, or Azure Active Directory (Azure AD) with key rollover.

## Custom key and license acquisition URL

Use the following templates if you want to specify a different license/key delivery service (not Media Services). The two replaceable fields in the templates are there so that you can share your streaming policy across many assets instead of creating a streaming policy per asset.

* `EnvelopeEncryption.CustomKeyAcquisitionUrlTemplate`: Template for the URL of the custom service that delivers keys to end-user players. It isn't required when you're using Azure Media Services for issuing keys.

   The template supports replaceable tokens that the service will update at runtime with the value specific to the request.  The currently supported token values are:
   * `{AlternativeMediaId}`, which is replaced with the value of StreamingLocatorId.AlternativeMediaId.
   * `{ContentKeyId}`, which is replaced with the value of the identifier of the requested key.
* `StreamingPolicyPlayReadyConfiguration.CustomLicenseAcquisitionUrlTemplate`: Template for the URL of the custom service that delivers licenses to end-user players. It isn't required when you're using Azure Media Services for issuing licenses.

   The template supports replaceable tokens that the service will update at runtime with the value specific to the request. The currently supported token values are:
   * `{AlternativeMediaId}`, which is replaced with the value of StreamingLocatorId.AlternativeMediaId.
   * `{ContentKeyId}`, which is replaced with the value of the identifier of the requested key.
* `StreamingPolicyWidevineConfiguration.CustomLicenseAcquisitionUrlTemplate`: Same as the previous template, only for Widevine.
* `StreamingPolicyFairPlayConfiguration.CustomLicenseAcquisitionUrlTemplate`: Same as the previous template, only for FairPlay.

For example:

```csharp
streamingPolicy.EnvelopEncryption.customKeyAcquisitionUrlTemplate = "https://mykeyserver.hostname.com/envelopekey/{AlternativeMediaId}/{ContentKeyId}";
```

`ContentKeyId` has a value of the requested key. You can use `AlternativeMediaId` if you want to map the request to an entity on your side. For example, `AlternativeMediaId` can be used to help you look up permissions.

For REST examples that use custom license/key acquisition URLs, see [Streaming Policies - Create](/rest/api/media/streamingpolicies/create).

> [!NOTE]
> Widevine is a service provided by Google Inc. and subject to the terms of service and Privacy Policy of Google, Inc.

[!INCLUDE [Warning on captions and encryption](./includes/warning-captions-encryption.md)]

## Troubleshoot

If you get the `MPE_ENC_ENCRYPTION_NOT_SET_IN_DELIVERY_POLICY` error, make sure that you specify the appropriate streaming policy.

If you get errors that end with `_NOT_SPECIFIED_IN_URL`, make sure that you specify the encryption format in the URL. An example is `…/manifest(format=m3u8-cmaf,encryption=cbcs-aapl)`. See [Streaming protocols and encryption types](drm-streaming-protocol-encryption-types-reference.md).