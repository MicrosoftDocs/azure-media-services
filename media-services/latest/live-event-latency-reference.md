---
title: Live Event low latency settings in Azure Media Services
description: Media Services supports Apple's Low Latency HLS (LL-HLS) specification.  This article describes Media Services support for LL-HLS and provides you with implementation guidance.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: reference
ms.date: 6/29/2023
ms.author: inhenkel
---

# Low Latency HLS (LL-HLS)

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Media Services support Apple's Low Latency HLS (LL-HLS) specification. This article describes Media Services support for LL-HLS and provides you with implementation guidance.

> [!NOTE]
> At this time, we do not support LL-DASH.

## LowLatency and LowLatencyV2 options

Media Services support low latency live streaming using LL-HLS for Standard Encoding Live Events and Premium Encoding Live Events. When creating a new encoding live event, you must choose StreamOptions.LowLatencyV2 when using the API, or the "Low latency" option using the Azure portal. With this option, you have certain limitations compared to the other stream options.

- Only RTMP input is supported at this time.
- Smooth output is not supported.
- You can still use DASH output and gain benefits of a much lower latency compared to other stream options. However LL-DASH is not supported.
- A smaller seekback window during live playback is recommended. By default we set a 30 minute seekback window.
- We can only archive up to 6 hours of live content.
- Fairplay support is limited.


## How to use LL-HLS

### Use LowLatencyV2 in the Azure portal

1. Set up your on-premises stream. Try the [OBS tutorial](live-event-obs-quickstart.md) if you haven't done this before.
1. While creating a live event, select either **Standard encoding (up to 720p)** or **Premium encoding (up to 1080p)** under the live event type.  The Stream latency options will appear.
1. Select the **Low latency** radio button.  *LowLatencyV2* will automatically be selected for the encoding standard you chose.
1. Optionally select the **Start preparing live event for input** checkbox to automatically start the live event. Remember that billing starts as soon as a live event is started.
1. Set any other options you want for the live event then select **Review and create**. The live event screen will appear with a listing of the streaming URLs.
1. Copy the **HLS URL** for use with the player.

### LL-HLS SDK Samples

There are detailed instructions in the comments of the sample code provided for LL-HLS.

- [Live Event with DVR - .NET](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)
- [Low Latency - Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Live/720P_Low_Latency_Encoding_Live_Event/index.ts)
- [Low Latency - Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Live/720p_Encoding_Live_Event_Low_Latency/720p_low_latency_encoding_live_event.py)

See [dynamic packaging](encode-dynamic-packaging-concept.md) page for more information on streaming URL formats.

## Player testing

We recommend that you use players that support LL-HLS and configure the players appropriately for best results.

We have tested with the latest version of the following players:

- Shaka 4.3.2
- Video.JS 7.21.1 with support for LL-HLS
- ExoPlayer

When using DASH output with Azure Media Player, configure the player with the following option: `heuristicprofile: LowLatency`.

## Output formats

For LL-HLS outputs use the format string: (format=m3u8-cmaf). For example:

`https://accountName-region.streaming.media.azure.net/11111111-1111-43ce-9dba-3aee82e35262/output.ism/manifest(format=m3u8-cmaf).m3u8`

When using DASH output use the format string: (format=mpd-time-cmaf)

> [!NOTE]
> The end-to-end latency can vary depending on local network conditions or by introducing a CDN caching layer. You should test your exact configurations.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
