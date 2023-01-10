---
title: Media Services v3 offline streaming
description: This article covers offline streaming with Fairplay, Widevine and Playready
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 01/09/2023
ms.author: inhenkel
ms.custom: engagement-fy23
---

<!-- William Zhang -->
<!-- Removed dependencies on external resources 7/13/2022 -IH -->
<!-- Removed .NET code from article, plus editing 9/29/2022 -IH -->
<!-- Consolidated all offline streaming from individual articles to this one for article performance reasons. 1/2/2023 -->

# Media Services offline streaming

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

- Your viewers might need to download content onto their phone or tablet for playback when they are disconnected from the Internet.
- In some countries/regions, Internet availability and/or bandwidth is still limited. Users may choose to download content to watch it in higher resolutions.
- Some content providers may disallow DRM license delivery beyond a country/region's border. If a user needs to travel abroad and still wants to watch content, offline download is needed.

Azure Media Services provides a set of well-designed [content protection services](https://azure.microsoft.com/services/media-services/content-protection/) for Microsoft PlayReady, Google Widevine<sup>*</sup>, Apple FairPlay Streaming, and AES-128 encryption.

> [!NOTE]
> Offline DRM is only billed for making a single request for a license when you download the content. Any errors are not billed.

## [Fairlplay](#tab/fairplay/)

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

## [Widevine](#tab/widevine/)



[!INCLUDE [Widevine is not available in the GovCloud region.](./includes/widevine-not-available-govcloud.md)]

This article gives you an overview of implementing offline mode playback for DASH content protected by Widevine on Android devices. It also answers some common questions related to offline streaming of Widevine protected content.

> [!NOTE]
> Offline DRM is only billed for making a single request for a license when you download the content. Any errors are not billed.

## Prerequisites

Before implementing offline DRM for Widevine on Android devices, you should first:

- Become familiar with the concepts introduced for online content protection using Widevine DRM.
- Clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git.
    - You will need to modify the code in [Encrypt with DRM using .NET](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/main/AMSV3Tutorials/EncryptWithDRM) to add Widevine configurations.
- Become familiar with the Google ExoPlayer SDK for Android, an open-source video player SDK capable of supporting offline Widevine DRM playback.
    - [ExoPlayer SDK](https://github.com/google/ExoPlayer)
    - [ExoPlayer Developer Guide](https://google.github.io/ExoPlayer/guide.html)
    - [EoPlayer Developer Blog](https://medium.com/google-exoplayer)

## Enable offline mode

To enable **offline** mode for Widevine licenses, configure the [Widevine license template](drm-widevine-license-template-concept.md). In the **policy_overrides** object, set the **can_persist** property to **true**, as shown in [ConfigureWidevineLicenseTemplate](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/main/AMSV3Tutorials/EncryptWithDRM/Program.cs#L452).

## Configure the Android player for offline playback

The easiest way to develop a native player app for Android devices is to use the [Google ExoPlayer SDK](https://github.com/google/ExoPlayer), an open-source video player SDK. ExoPlayer supports features not currently supported by Android's native MediaPlayer API, including MPEG-DASH and Microsoft Smooth Streaming delivery protocols.

ExoPlayer version 2.6 and higher includes many classes that support offline Widevine DRM playback. In particular, the `OfflineLicenseHelper` class provides utility functions to facilitate the use of the DefaultDrmSessionManager for downloading, renewing, and releasing offline licenses. The classes provided in the SDK folder `library/core/src/main/java/com/google/android/exoplayer2/offline/` support offline video content downloading.

The following list of classes facilitates offline mode in the ExoPlayer SDK for Android:

- `library/core/src/main/java/com/google/android/exoplayer2/drm/OfflineLicenseHelper.java`
- `library/core/src/main/java/com/google/android/exoplayer2/drm/DefaultDrmSession.java`
- `library/core/src/main/java/com/google/android/exoplayer2/drm/DefaultDrmSessionManager.java`
- `library/core/src/main/java/com/google/android/exoplayer2/drm/DrmSession.java`
- `library/core/src/main/java/com/google/android/exoplayer2/drm/ErrorStateDrmSession.java`
- `library/core/src/main/java/com/google/android/exoplayer2/drm/ExoMediaDrm.java`
- `library/core/src/main/java/com/google/android/exoplayer2/offline/SegmentDownloader.java`
- `library/core/src/main/java/com/google/android/exoplayer2/offline/DownloaderConstructorHelper.java`
- `library/core/src/main/java/com/google/android/exoplayer2/offline/Downloader.java`
- `library/dash/src/main/java/com/google/android/exoplayer2/source/dash/offline/DashDownloader.java`

Developers should reference the [ExoPlayer Developer Guide](https://google.github.io/ExoPlayer/guide.html) and the corresponding [Developer Blog](https://medium.com/google-exoplayer) during development of an application.

### Working with older Android devices

For some older Android devices, you must set values for the following **policy_overrides** properties (defined in [Widevine license template](drm-widevine-license-template-concept.md): **rental_duration_seconds**, **playback_duration_seconds**, and **license_duration_seconds**. Alternatively, you can set them to `0`, which means there is no time restriction.

> [!WARNING]
> The values must be set to avoid an integer overflow bug. For more explanation about the issue, see https://github.com/google/ExoPlayer/issues/3150 and https://github.com/google/ExoPlayer/issues/3112. <br/>If you do not set the values explicitly, very large values for  **PlaybackDurationRemaining** and **LicenseDurationRemaining** will be assigned, (for example, 9223372036854775807, which is the maximum positive value for a 64-bit integer). As a result, the Widevine license appears expired and hence the decryption will not happen.<br/><br/>This issue does not occur on Android 5.0 Lollipop or later since Android 5.0 is the first Android version, which has been designed to fully support ARMv8 ([Advanced RISC Machine](https://en.wikipedia.org/wiki/ARM_architecture)) and 64-bit platforms, while Android 4.4 KitKat was originally designed to support  ARMv7 and 32-bit platforms as with other older Android versions.

## Use Xamarin to build an Android playback app

You can find Xamarin bindings for ExoPlayer using the following links:

- [Xamarin bindings library for the Google ExoPlayer library](https://github.com/martijn00/ExoPlayerXamarin)
- [Xamarin bindings for ExoPlayer NuGet](https://www.nuget.org/packages/Xam.Plugins.Android.ExoPlayer/)

Also, see the following thread: [Xamarin binding](https://github.com/martijn00/ExoPlayerXamarin/pull/57).

## Chrome player apps for Android

Starting with the release of [Chrome for Android v. 62](https://developers.google.com/web/updates/2017/09/chrome-62-media-updates), persistent license in EME is supported. [Widevine L1](https://developers.google.com/web/updates/2017/09/chrome-62-media-updates#widevine_l1) is now also supported in Chrome for Android. This allows you to create offline playback applications in Chrome if your end users have this (or higher) version of Chrome.

In addition, Google has produced a Progressive Web App (PWA) sample:

- [Source code](https://github.com/GoogleChromeLabs/sample-media-pwa)
- [Google hosted version](https://biograf-155113.appspot.com/ttt/episode-2/) (only works in Chrome v 62 and higher on Android devices)

If you upgrade your mobile Chrome browser to v62 (or higher) on an Android phone and test the above hosted sample app, you will see that both online streaming and offline playback work.

The above open-source PWA app is authored in Node.js. If you want to host your own version on an Ubuntu server, keep in mind the following common encountered issues that can prevent playback:

1. CORS issue: The sample video in the sample app is hosted in https://storage.googleapis.com/biograf-video-files/videos/. Google has set up CORS for all their test samples hosted in Google Cloud Storage bucket. They are served with CORS headers, specifying explicitly the CORS entry: `https://biograf-155113.appspot.com` (the domain in which google hosts their sample) preventing access by any other sites. If you try, you will see the following HTTP error: `Failed to load https://storage.googleapis.com/biograf-video-files/videos/poly-sizzle-2015/mp4/dash.mpd: No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'https:\//13.85.80.81:8080' is therefore not allowed access. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.`
2. Certificate issue: Starting from Chrome v 58, EME for Widevine requires HTTPS. Therefore, you need to host the sample app over HTTPS with an X509 certificate. A usual test certificate does not work due to the following requirements: You need to obtain a certificate meeting the following minimum requirements:
    - Chrome and Firefox require SAN-Subject Alternative Name setting to exist in the certificate
    - The certificate must have trusted CA and a self-signed development certificate does not work
    - The certificate must have a CN matching the DNS name of the web server or gateway

## [PlayReady](#tab/playready/)

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

---

## More information

For more information, see [Content Protection in the FAQ](frequently-asked-questions.yml).

Widevine is a service provided by Google Inc. and subject to the terms of service and Privacy Policy of Google, Inc.


[!INCLUDE [media-services-community](includes/media-services-community.md)]
