---
title: Live transcription
description: When you publish a live stream using MPEG-DASH or HLS/CMAF, transcribed text in IMSC1.1 compatible TTML is created along with video and audio. It is packaged into MPEG-4 Part 30 (ISO/IEC 14496-30) fragments. If you use HLS/TS, text is delivered as chunked VTT. This article describes how to enable live transcription when streaming a Live Event with Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 07/25/2022
ms.author: inhenkel
---

# How to use live transcription

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Transcription delivery and playback

When you publish a live stream using MPEG-DASH or HLS/CMAF, transcribed text in IMSC1.1 compatible TTML is created along with video and audio. It is packaged into MPEG-4 Part 30 (ISO/IEC 14496-30) fragments. If you use HLS/TS, text is delivered as chunked VTT.

If you are using the Azure Media Player, use the [Azure Media Player version 2.3.3 or later](player-use-azure-media-player-how-to.md).

> [!NOTE]
> Additional charges apply when live transcription is turned on. Please review the pricing information in the Live Video section of the [Media Services pricing page](https://azure.microsoft.com/pricing/details/media-services/).

[!INCLUDE [live-transcription-gop-size](includes/live-transcription-gop-size.md)]

## Live transcription auto generated VTT file

When you enable live transcription for a live event, a WebVTT file is generated and is located in the root of the archived asset. As this file is delayed until after all speech has been broadcast, you should not delete the live output for several minutes after the broadcast has ended. You can then download the VTT file and edit it or use it for translation to other languages for subtitles. The files is named `auto-generated-best_XXX.vtt`.

> [!WARNING]
> The final auto generated live transcription VTT files are delayed for processing. Unless you wait for several minutes before deleting a live output, the content in the file will be truncated.  Additionally, live transcription is not available for use with multiple input streams for a live event.

For more information about how to use the Tracks API with the generated WebVTT file, see the [Tracks](tracks-concept.md) article.

## Create a live event with live transcription

You can create a live event with live transcription using the Azure portal, with the REST API or with any of the SDKs.

The language code must match the spoken language of the video. See the [language code table](#live-transcription-regions-and-languages) at the end of this article.

## [Portal](#tab/portal/)

[!INCLUDE [task-create-live-event-portal](includes/task-create-live-event-portal.md)]

## [REST](#tab/rest/)

To create a live event with the transcription turned on, set the 'transcriptions' property with the desired language code when creating the [live event](/rest/api/media/live-events/create).

## [CLI](#tab/cli/)

[!INCLUDE [task-create-live-event-cli](includes/task-create-live-event-cli.md)]

## [Python](#tab/python/)

[!INCLUDE [task-create-live-event-python](includes/task-create-live-event-python.md)]

---

## Start or stop transcription after the live event has started

You can start and stop, or change the language of live transcription while the live event is in running, standby or stopped state.

> [!IMPORTANT]
> Turning live transcription on or off must be done before any data is written to the output asset - this is usually when a live output is created, or when the incoming input stream arrives at the live event.

To turn on live transcriptions or to update the transcription language, patch the live event to include a “[transcriptions](/rest/api/media/live-events/create#liveeventtranscription)” property with the correct language code on the 'language' property. See the list above to supported language codes.

To turn off live transcriptions, remove the “transcriptions” property from the live event object.

## Live transcription regions and languages

Live transcription is available in the regions as documented [here](azure-clouds-regions.md).

This is the list of available languages that can be transcribed, use the language code in the API.

| Language                          | Locale (BCP-47) |
|-----------------------------------|-----------------|
| Afrikaans (South Africa)          | `af-ZA`         |
| Amharic (Ethiopia)                | `am-ET`         |
| Arabic (Algeria)                  | `ar-DZ`         |
| Arabic (Bahrain), modern standard | `ar-BH`         |
| Arabic (Egypt)                    | `ar-EG`         |
| Arabic (Iraq)                     | `ar-IQ`         |
| Arabic (Israel)                   | `ar-IL`         |
| Arabic (Jordan)                   | `ar-JO`         |
| Arabic (Kuwait)                   | `ar-KW`         |
| Arabic (Lebanon)                  | `ar-LB`         |
| Arabic (Libya)                    | `ar-LY`         |
| Arabic (Morocco)                  | `ar-MA`         |
| Arabic (Oman)                     | `ar-OM`         |
| Arabic (Palestinian Authority)    | `ar-PS`         |
| Arabic (Qatar)                    | `ar-QA`         |
| Arabic (Saudi Arabia)             | `ar-SA`         |
| Arabic (Syria)                    | `ar-SY`         |
| Arabic (Tunisia)                  | `ar-TN`         |
| Arabic (United Arab Emirates)     | `ar-AE`         |
| Arabic (Yemen)                    | `ar-YE`         |
| Bengali (India)                   | `bn-IN`         |
| Bulgarian (Bulgaria)              | `bg-BG`         |
| Burmese (Myanmar)                 | `my-MM`         |
| Catalan (Spain)                   | `ca-ES`         |
| Chinese (Cantonese, Traditional)  | `zh-HK`         |
| Chinese (Mandarin, Simplified)    | `zh-CN`         |
| Chinese (Taiwanese Mandarin)      | `zh-TW`         |
| Croatian (Croatia)                | `hr-HR`         |
| Czech (Czech)                     | `cs-CZ`         |
| Danish (Denmark)                  | `da-DK`         |
| Dutch (Belgium)                   | `nl-BE`         |
| Dutch (Netherlands)               | `nl-NL`         |
| English (Australia)               | `en-AU`         |
| English (Canada)                  | `en-CA`         |
| English (Ghana)                   | `en-GH`         |
| English (Hong Kong)               | `en-HK`         |
| English (India)                   | `en-IN`         |
| English (Ireland)                 | `en-IE`         |
| English (Kenya)                   | `en-KE`         |
| English (New Zealand)             | `en-NZ`         |
| English (Nigeria)                 | `en-NG`         |
| English (Philippines)             | `en-PH`         |
| English (Singapore)               | `en-SG`         |
| English (South Africa)            | `en-ZA`         |
| English (Tanzania)                | `en-TZ`         |
| English (United Kingdom)          | `en-GB`         |
| English (United States)           | `en-US`         |
| Estonian (Estonia)                | `et-EE`         |
| Filipino (Philippines)            | `fil-PH`        |
| Finnish (Finland)                 | `fi-FI`         |
| French (Belgium)                  | `fr-BE`         |
| French (Canada)                   | `fr-CA`         |
| French (France)                   | `fr-FR`         |
| French (Switzerland)              | `fr-CH`         |
| German (Austria)                  | `de-AT`         |
| German (Germany)                  | `de-DE`         |
| German (Switzerland)              | `de-CH`         |
| Greek (Greece)                    | `el-GR`         |
| Gujarati (Indian)                 | `gu-IN`         |
| Hebrew (Israel)                   | `he-IL`         |
| Hindi (India)                     | `hi-IN`         |
| Hungarian (Hungary)               | `hu-HU`         |
| Icelandic (Iceland)               | `is-IS`         |
| Indonesian (Indonesia)            | `id-ID`         |
| Irish (Ireland)                   | `ga-IE`         |
| Italian (Italy)                   | `it-IT`         |
| Japanese (Japan)                  | `ja-JP`         |
| Javanese (Indonesia)              | `jv-ID`         |
| Kannada (India)                   | `kn-IN`         |
| Khmer (Cambodia)                  | `km-KH`         |
| Korean (Korea)                    | `ko-KR`         |
| Lao (Laos)                        | `lo-LA`         |
| Latvian (Latvia)                  | `lv-LV`         |
| Lithuanian (Lithuania)            | `lt-LT`         |
| Macedonian (North Macedonia)      | `mk-MK`         |
| Malay (Malaysia)                  | `ms-MY`         |
| Maltese (Malta)                   | `mt-MT`         |
| Marathi (India)                   | `mr-IN`         |
| Norwegian (Bokmål, Norway)        | `nb-NO`         |
| Persian (Iran)                    | `fa-IR`         |
| Polish (Poland)                   | `pl-PL`         |
| Portuguese (Brazil)               | `pt-BR`         |
| Portuguese (Portugal)             | `pt-PT`         |
| Romanian (Romania)                | `ro-RO`         |
| Russian (Russia)                  | `ru-RU`         |
| Serbian (Serbia)                  | `sr-RS`         |
| Sinhala (Sri Lanka)               | `si-LK`         |
| Slovak (Slovakia)                 | `sk-SK`         |
| Slovenian (Slovenia)              | `sl-SI`         |
| Spanish (Argentina)               | `es-AR`         |
| Spanish (Bolivia)                 | `es-BO`         |
| Spanish (Chile)                   | `es-CL`         |
| Spanish (Colombia)                | `es-CO`         |
| Spanish (Costa Rica)              | `es-CR`         |
| Spanish (Cuba)                    | `es-CU`         |
| Spanish (Dominican Republic)      | `es-DO`         |
| Spanish (Ecuador)                 | `es-EC`         |
| Spanish (El Salvador)             | `es-SV`         |
| Spanish (Equatorial Guinea)       | `es-GQ`         |
| Spanish (Guatemala)               | `es-GT`         |
| Spanish (Honduras)                | `es-HN`         |
| Spanish (Mexico)                  | `es-MX`         |
| Spanish (Nicaragua)               | `es-NI`         |
| Spanish (Panama)                  | `es-PA`         |
| Spanish (Paraguay)                | `es-PY`         |
| Spanish (Peru)                    | `es-PE`         |
| Spanish (Puerto Rico)             | `es-PR`         |
| Spanish (Spain)                   | `es-ES`         |
| Spanish (Uruguay)                 | `es-UY`         |
| Spanish (USA)                     | `es-US`         |
| Spanish (Venezuela)               | `es-VE`         |
| Swahili (Kenya)                   | `sw-KE`         |
| Swahili (Tanzania)                | `sw-TZ`         |
| Swedish (Sweden)                  | `sv-SE`         |
| Tamil (India)                     | `ta-IN`         |
| Telugu (India)                    | `te-IN`         |
| Thai (Thailand)                   | `th-TH`         |
| Turkish (Turkey)                  | `tr-TR`         |
| Ukrainian (Ukraine)               | `uk-UA`         |
| Uzbek (Uzbekistan)                | `uz-UZ`         |
| Vietnamese (Vietnam)              | `vi-VN`         |
| Zulu (South Africa)               | `zu-ZA`         |
