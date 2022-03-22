---
title: Live transcription
description: Learn about Azure Media Services live transcription.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 3/16/2022
ms.author: inhenkel
---

# Live transcription

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Azure Media Service delivers video, audio, and text in different protocols. When you publish your live stream using MPEG-DASH or HLS/CMAF, then along with video and audio, our service delivers the transcribed text in IMSC1.1 compatible TTML. The delivery is packaged into MPEG-4 Part 30 (ISO/IEC 14496-30) fragments. If using delivery via HLS/TS, then text is delivered as chunked VTT.

Additional charges apply when live transcription is turned on. Please review the pricing information in the Live Video section of the [Media Services pricing page](https://azure.microsoft.com/pricing/details/media-services/).

This article describes how to enable live transcription when streaming a Live Event with Azure Media Services. Before you continue, make sure you are familiar with the [live streaming](stream-live-streaming-concept.md) concept. It's recommended to complete the [Stream live with Media Services](stream-live-tutorial-with-api.md) tutorial.

## Live transcription preview regions and languages

Live transcription is available in the regions as documented [here](azure-clouds-regions.md).

This is the list of available languages that can be transcribed, use the language code in the API.

| Language | Language code |
| -------- | ------------- |
| Catalan  | ca-ES |
| Danish (Denmark) | da-DK |
| German (Germany) | de-DE |
| English (Australia) | en-AU |
| English (Canada) | en-CA |
| English (United Kingdom) | en-GB |
| English (India) | en-IN |
| English (New Zealand) | en-NZ |
| English (United States) | en-US |
| Spanish (Spain) | es-ES |
| Spanish (Mexico) | es-MX |
| Finnish (Finland) | fi-FI |
| French (Canada) | fr-CA |
| French (France) | fr-FR |
| Italian (Italy) | it-IT |
| Dutch (Netherlands) | nl-NL |
| Portuguese (Brazil) | pt-BR |
| Portuguese (Portugal) | pt-PT |
| Swedish (Sweden) | sv-SE |

## Create the live event with live transcription

To create a live event with the transcription turned on, set the 'transcriptions' property with the desired language code when creating the [live event](/rest/api/media/live-events/create). The language code must match the spoken language of the video.


## Start or stop transcription after the live event has started

You can start and stop, or change the language of live transcription while the live event is in running, standby or stopped state.

To turn on live transcriptions or to update the transcription language, patch the live event to include a “[transcriptions](/rest/api/media/live-events/create#liveeventtranscription)” property with the correct language code on the 'language' property. See the list above to supported language codes.

To turn off live transcriptions, remove the “transcriptions” property from the live event object.

> [!NOTE]
> Turning live transcription on or off must be done before any data is written to the output asset - this is usually when a live output is created, or when the incoming input stream arrives at the live event.


## Transcription delivery and playback

Review the [Dynamic packaging overview](encode-dynamic-packaging-concept.md#to-prepare-your-source-files-for-delivery) article of how our service uses dynamic packaging to deliver video, audio, and text in different protocols. When you publish your live stream using MPEG-DASH or HLS/CMAF, then along with video and audio, our service delivers the transcribed text in IMSC1.1 compatible TTML. This delivery is packaged into MPEG-4 Part 30 (ISO/IEC 14496-30) fragments. If using delivery via HLS/TS, then the text is delivered as chunked VTT. You can use a web player such as the [Azure Media Player](player-use-azure-media-player-how-to.md) to play the stream.

> [!NOTE]
> If using Azure Media Player, use version 2.3.3 or later.


## Next steps

* [Media Services overview](media-services-overview.md)
