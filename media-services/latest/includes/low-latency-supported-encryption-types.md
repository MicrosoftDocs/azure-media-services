---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 06/22/2022
ms.author: inhenkel
title: low latency supported encryption types
---

## HLS and DASH

The following container formats and encryption schemes are supported.

| Packaging format | Container format | Condition | Encryption scheme | Format string |
| ---------------- | ---------------- | -------------------- | ----------------- | ------------- |
| HLS v3           | MPG2-TS          | Requires playlist proxy for HLS when token auth is used | AES             | (format=m3u8-aapl-v3,encryption=cbc) |
|                  |                  |                                                         | CBCS (FairPlay) | (format=m3u8-aapl-v3,encryption=cbcs-aapl) |
| HLS v4           | MPG2-TS          | Requires playlist proxy for HLS when token auth is used | AES             | (format=m3u8-aapl-v4,encryption=cbc) |
|                  |                  | Non LL-HLS scenario                                     | CBCS (FairPlay) | (format=m3u8-aapl-v4,encryption=cbcs-aapl) |
| HLS v7 and above | CMAF             | Requires playlist proxy for HLS                         | AES             | (format=m3u8-cmaf,encryption=cbc) |
|                  |                  | Does not work with LL-HLS output                        | CBCS (FairPlay) | (format=m3u8-cmaf,encryption=cbcs-aapl) |
| Dash             | CMAF             |                                                         | AES             | (format=mpd-time-cmaf,encryption=cbc) |
|                  |                  |                                                         | CENC (PlayReady or Widevine)	(format=mpd-time-cmaf,encryption=cenc)

HLS/CMAF + FairPlay (including HEVC/H.265) is supported on the following devices:

- iOS 11 or later.
- iPhone 8 or later.
- macOS High Sierra with Intel 7th Generation CPU.

[!INCLUDE [Widevine is not available in the GovCloud region.](./includes/widevine-not-available-govcloud.md)]

## Smooth Streaming

The Smooth Streaming protocol supports the following container formats and encryption schemes.

|Protocol|Container format|Encryption scheme|
|---|---|---|
|fMP4|AES|`https://amsv3account-usw22.streaming.media.azure.net/00000000-0000-0000-0000-000000000000/ignite.ism/manifest(encryption=cbc)`|
|fMP4 | CENC (PlayReady) |`https://amsv3account-usw22.streaming.media.azure.net/00000000-0000-0000-0000-000000000000/ignite.ism/manifest(encryption=cenc)`|
|fMP4 | PIFF 1.1 (PlayReady) |`https://amsv3account-usw22.streaming.media.azure.net/00000000-0000-0000-0000-000000000000/ignite.ism/manifest(encryption=piff)`|

> [!NOTE]
> PIFF 1.1 support is provided as a backwards compatible solution for Smart TV (Samsung, LG) that implemented the early "Silverlight" version of Common Encryption. It is recommended to only use the PIFF format where needed for support of legacey Samsung or LG Smart TVs shipped between 2009-2015 that supported the PIFF 1.1 version of PlayReady encryption.