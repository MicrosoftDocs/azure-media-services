---
title: Dynamic encryption and key delivery
description: Learn about content protection with dynamic encryption, streaming protocols, and encryption types in Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 06/22/2022
ms.author: inhenkel
---

# Content protection with dynamic encryption and key delivery

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Use Azure Media Services to help secure your media from the time it leaves your computer all the way through storage, processing, and delivery. With Media Services, you can deliver your live and on-demand content encrypted dynamically with Advanced Encryption Standard (AES-128) or any of the three major digital rights management (DRM) systems: Microsoft PlayReady, Google Widevine, and Apple FairPlay. FairPlay Streaming is an Apple technology that is only available for video transferred over HTTP Live Streaming (HLS) on iOS devices, in Apple TV, and in Safari on macOS. Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses to authorized clients. If content is encrypted with an AES clear key and is sent over HTTPS, it is not in clear until it reaches the client.

In Media Services v3, a content key is associated with Streaming Locator (see [this example](drm-playready-license-template-concept.md)). If using the Media Services key delivery service, you can let Azure Media Services generate the content key for you. The content key should be generated yourself if you're using you own key delivery service, or if you need to handle a high availability scenario where you need to have the same content key in two data centers.

When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES clear key or DRM encryption. To decrypt the stream, the player requests the key from Media Services key delivery service or the key delivery service you specified. To decide if the user is authorized to get the key, the service evaluates the content key policy that you specified for the key.

:::image type="content" source="media/diagrams/content-protection.svg" alt-text="content protection system":::

You can use the REST API, or a Media Services client library to configure authorization and authentication policies for your licenses and keys.

[!INCLUDE [Widevine is not available in the GovCloud region.](./includes/widevine-not-available-govcloud.md)]

## Browsers that support DRM clients

Common browsers support the following DRM clients:

|Browser|Encryption|
|---|---|
|Chrome|Widevine|
|Microsoft Edge, Internet Explorer 11|PlayReady|
|Firefox|Widevine|
|Opera|Widevine|
|Safari|FairPlay|

## Controlling content access

You can control who has access to your content by configuring the content key policy. Media Services supports multiple ways of authorizing users who make key requests. The client (player) must meet the policy before the key can be delivered to the client. The content key policy can have *open* or *token* restriction.

An open-restricted content key policy may be used when you want to issue a license to anyone without authorization. For example, if your revenue is ad-based and not subscription-based.

With a token-restricted content key policy, the content key is sent only to a client that presents a valid JWT token or a simple web token (SWT) in the license/key request. This token must be issued by an STS.

### Using Azure AD as an STS
You can use Azure AD as an STS. It must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration. The Media Services license/key delivery service returns the requested license or key to the client if both of these conditions exist:

* The token is valid.
* The claims in the token match those configured for the license or key.

When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters. The primary verification key contains the key that the token was signed with. The issuer is the STS that issues the token. The audience, sometimes called *scope*, describes the intent of the token or the resource that the token authorizes access to. The Media Services license/key delivery service validates that the values in the token match the values in the template.

### Token replay prevention

The *Token Replay Prevention* feature allows Media Services customers to set a limit on how many times the same token can be used to request a key or a license. The customer can add a claim of type `urn:microsoft:azure:mediaservices:maxuses` in the token, where the value is the number of times the token can be used to acquire a license or key. All subsequent requests with the same token to Key Delivery will return an unauthorized response.

#### Considerations

* You must have control over token generation. The claim needs to be placed in the token itself.
* When using this feature, requests with tokens whose expiry time is more than one hour away from the time the request is received are rejected with an unauthorized response.
* Tokens are uniquely identified by their signature. Any change to the payload (for example, update to the expiry time or the claim) changes the signature of the token and it will count as a new token that Key Delivery hasn't come across before.
* Playback fails if the token has exceeded the `maxuses` value set by the customer.
* It can be used for all existing protected content (only the token issued needs to be changed).
* It works with both JWT and SWT.

## Using a custom STS

You might choose to use a custom STS to provide tokens. Reasons include:

* Your identity provider (IDP) doesn't support STS.
* You might need more flexible or tighter control to integrate the STS with your subscriber billing system.

   For example, an [OTT](https://en.wikipedia.org/wiki/Over-the-top_media_services) service operator might offer multiple subscriber packages, such as premium, basic, and sports. The operator might want to match the claims in a token with a subscriber's package so that only the contents in a specific package are made available. In this case, a custom STS provides the needed flexibility and control.

* To include custom claims in the token to select between different ContentKeyPolicyOptions with different DRM license parameters, for example, a subscription license versus a rental license.
* To include a claim representing the content key identifier of the key that the token grants access to.

When you use a custom STS, two changes must be made:

* When you configure a license delivery service for an asset, you need to specify the security key used for verification by the custom STS instead of the current key from Azure AD.
* When a JTW token is generated, a security key is specified instead of the private key of the current X509 certificate in Azure AD.

There are two types of security keys:

* Symmetric key: The same key is used to generate and to verify a JWT.
* Asymmetric key: A public-private key pair in an X509 certificate is used with a private key to encrypt/generate a JWT and with the public key to verify the token.

> [!NOTE]
> If you use .NET Framework/C# as your development platform, the X509 certificate used for an asymmetric security key must have a key length of at least 2048. This key length is a requirement of the class System.IdentityModel.Tokens.X509AsymmetricSecurityKey in .NET Framework. Otherwise, the following exception is thrown: IDX10630: The 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' for signing can't be smaller than '2048' bits.

## Using a license/key delivery service other than Media Services

You can edit key policy templates if you want to use a different license/key delivery service.

## Test content protection system

Read this [overview of creating a test content protection system](drm-test-system-concept.md), and then try some of the following instructional content.

## How-tos, tutorials and samples

- [Use DRM dynamic encryption and license delivery service tutorial](drm-protect-with-drm-tutorial.md) which uses the following sample.
- The [DRM sample](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/main/AMSV3Tutorials/EncryptWithDRM/Program.cs) shows you how to implement a multi-DRM system with Media Services v3 by using .NET. It also shows you how to use the Media Services license/key delivery service. You can encrypt each asset with multiple encryption types (AES-128, PlayReady, Widevine, FairPlay). The sample shows you how to create and configure a [content key policy](drm-content-key-policy-concept.md), create a [streaming locator](stream-streaming-locators-concept.md) that's configured to stream the encrypted asset, create a test token, and build a streaming URL.
- [Protect content with AES 128](drm-protect-with-aes128-tutorial.md) tutorial.

There are additional content protection samples available for Node.JS and Python:

| **Node.JS** | **Python** | Description |
|---|---| ---|
|[Node.JS Upload and stream HLS and DASH with PlayReady and Widevine DRM](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Streaming/StreamFilesWithDRMSample/index.ts)|[Python Upload and stream HLS and DASH with PlayReady and Widevine DRM](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Streaming/StreamFilesWithDRM/stream-files-with-drm-sample.py)| Demonstrates how to encode and stream using Widevine and PlayReady DRM |
|[Node.JS Basic Playready DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicPlayready/index.ts)|[Python Basic Playready DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicPlayReady/basic-play-ready.py)| Demonstrates how to encode and stream using PlayReady DRM |
|[Node.JS Basic Widevine DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/ContentProtection/BasicWidevine/index.ts)| [Python Basic Widevine DRM content protection and streaming](https://github.com/Azure-Samples/media-services-v3-python/blob/main/ContentProtection/BasicWidevine/basic-widevine.py) | Demonstrates how to encode and stream using Widevine DRM |
