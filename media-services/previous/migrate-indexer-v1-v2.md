---
title: Migrate from Indexer v1 and v2 to Azure Media Services Video Indexer | Microsoft Docs
description: This topic discusses how to migrate from Azure Media Indexer v1 and v2 to Azure Media Services Video Indexer.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/26/2021
ms.author: inhenkel
---
# Migrate from Media Indexer and Media Indexer 2 to Video Analyzer for Media 

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

> [!IMPORTANT]
> It is recommended that customers migrate from Indexer v1 and Indexer v2 to using the [Media Services v3 AudioAnalyzerPreset Basic mode](../latest/analyze-video-audio-files-concept.md). The [Azure Media Indexer](media-services-index-content.md) media processor and [Azure Media Indexer 2 Preview](./legacy-components.md) media processors are being retired. For the retirement dates, see this [legacy components](legacy-components.md) topic.

Azure Video Analyzer for Media is built on Azure Media Analytics, Azure Cognitive Search, Cognitive Services (such as the Face API, Microsoft Translator, the Computer Vision API, and Custom Speech Service). It enables you to extract the insights from your videos using Video Analyzer for Media video and audio models. To see what scenarios Video Analyzer for Media can be used in, and what features it offers, and how to get started, see [Video Analyzer for Media video and audio models](../../azure-video-analyzer/video-analyzer-for-media-docs/video-indexer-overview.md). 

You can extract insights from your video and audio files by using the [Azure Media Services v3 analyzer presets](../latest/analyze-video-audio-files-concept.md) or directly by using the [Video Analyzer for Media APIs](https://api-portal.videoindexer.ai/). Currently, there is an overlap between features offered by the Video Analyzer for Media APIs and the Media Services v3 APIs.

> [!NOTE]
> To understand the differences between the Video Analyzer for Media vs. Media Services analyzer presets, check out the [comparison document](../../azure-video-analyzer/video-analyzer-for-media-docs/compare-video-indexer-with-media-services-presets.md).

This article discusses the steps for migrating from the Azure Media Indexer and Azure Media Indexer 2 to Video Analyzer for Media.  

## Migration options

|If you require  |then |
|---|---|
|a solution that provides a speech-to-text transcription for any media file format in a closed caption file formats: VTT, SRT, or TTML<br/>as well as additional audio insights such as: keywords, topic inferencing, acoustic events, speaker diarization, entities extraction and translation| update your applications to use the Video Analyzer for Media capabilities through the Video Analyzer for Media v2 REST API or the Azure Media Services v3 Audio Analyzer preset.|
|speech-to-text capabilities| use the Cognitive Services Speech API directly.|  

## Getting started with Video Analyzer for Media

The following section points you to relevant links: [How can I get started with Video Analyzer for Media?](../../azure-video-analyzer/video-analyzer-for-media-docs/video-indexer-overview.md#how-can-i-get-started-with-video-analyzer-for-media) 

## Getting started with Media Services v3 APIs

Azure Media Services v3 API enables you to extract insights from your video and audio files through the [Azure Media Services v3 analyzer presets](../latest/analyze-video-audio-files-concept.md).

**AudioAnalyzerPreset** enables you to extract multiple audio insights from an audio or video file. The output includes a VTT or TTML file for the audio transcript and a JSON file (with all the additional audio insights). The audio insights include keywords, speaker indexing, and speech sentiment analysis. AudioAnalyzerPreset also supports language detection for specific languages. For detailed information, see [Transforms](/rest/api/media/transforms/createorupdate#audioanalyzerpreset).

### Get started

To get started see:

* [Tutorial](../latest/analyze-videos-tutorial.md)
* AudioAnalyzerPreset samples: [Java SDK](https://github.com/Azure-Samples/media-services-v3-java/tree/master/AudioAnalytics/AudioAnalyzer) or [.NET SDK](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/master/AudioAnalytics/AudioAnalyzer)
* VideoAnalyzerPreset samples: [Java SDK](https://github.com/Azure-Samples/media-services-v3-java/tree/master/VideoAnalytics/VideoAnalyzer) or [.NET SDK](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/master/VideoAnalytics/VideoAnalyzer)

## Getting started with Cognitive Services Speech Services

[Azure Cognitive Services](../../cognitive-services/index.yml) provides a speech-to-text service that transcribes audio streams to text in real time that your applications, tools, or devices can consume or display. You can  use speech-to-text to [customize your own acoustic model, language model, or pronunciation model](../../cognitive-services/speech-service/how-to-custom-speech-train-model.md). For more information, see [Cognitive Services speech-to-text](../../cognitive-services/speech-service/speech-to-text.md). 

> [!NOTE] 
> The speech-to-text service does not take video file formats and only takes [certain audio formats](../../cognitive-services/speech-service/rest-speech-to-text.md#audio-formats). 

For more information about the text-to-speech service and how to get started, see [What is speech-to-text?](../../cognitive-services/speech-service/speech-to-text.md)

## Known differences from deprecated services

You will find that Video Analyzer for Media, Azure Media Services v3 AudioAnalyzerPreset, and Cognitive Services Speech Services services are more reliable and produces better quality output than the retired Azure Media Indexer 1 and Azure Media Indexer 2 processors.  

Some known differences include:

* Cognitive Services Speech Services does not support keyword extraction. However, Video Analyzer for Media and Media Services v3 AudioAnalyzerPreset both offer a more robust set of keywords in JSON file format.

## Support

You can open a support ticket by navigating to [New support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)

## Next steps

* [Legacy components](legacy-components.md)
* [Pricing page](https://azure.microsoft.com/pricing/details/media-services/#encoding)
