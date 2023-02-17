---
title: Azure Media Services Encoding code samples
description: This article is a listing of code samples for Encoding.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/16/2023
ms.author: inhenkel
---

# Azure Media Services Encoding code samples

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

This article is a listing of code samples for Encoding.

## Create a transform and use job preset overrides (v2-to-v3 API migration)

If you need a workflow where you desire to submit custom preset jobs to a single queue, you can use this base sample that shows how to create a (mostly) empty Transform, and then use the preset override property on the Job to submit custom presets to the same transform. This allows you to treat the v3 AMS API a lot more like the legacy v2 API Job queue if you desire.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/CreateTransform_Job_PresetOverride/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/CreateTransform_Job_PresetOverride/create-transform-job-preset-override-helper.py) |

## Copy Audio and Video to MP4 without re-encoding

This sample uses the built-in preset that rapidly copies the source video and audio into a new MP4 file that is ready to be streamed on-demand. This is an extremely useful preset for pre-encoded content or externally encoded content to be quickly readied for streaming in AMS.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_BuiltIn_CopyCodec/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_BuiltIn_CopyCodec/encoding-builtin-copycodec-helper.py) |

## Copy Audio and Video to MP4 without re-encoding and create a low bitrate proxy

This sample adds an additional fast-encoded proxy resolution to the Copy Audio and Video to MP4 sample. It is very useful when creating a CMS or preview of an Asset.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_BuiltIn_CopyCodecWithProxy/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_BuiltIn_CopyCodecWithProxy/encoding-builtin-copycodecwithproxy-helper.py) |

## Copy Audio and Video to MP4 without re-encoding and create a low bitrate proxy and VTT sprite thumbnail

This sample adds a VTT sprite thumbnail to the Copy Audio and Video to MP4 sample for building a web page, CMS, or custom asset management application.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_Custom_CopyCodec_Sprite+Proxy/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_Custom_CopyCodec_Sprite_Proxy/encoding-custom-copycodec-sprite-proxy-helper.py) |

## Encode with H264

This sample shows how to use the standard encoder to encode a source file into H264 format with AAC audio and PNG thumbnails.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_H264) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264/encoding-h264-helper.py) |

## Encode with H264 with Event Hubs/Event Grid

This sample shows how to use the standard encoder and receive and process Event Grid events from Media Services through an Event Hubs. First, set up an Event Grid subscription that pushes events into an Event Hubs using the Azure portal or CLI to use this sample.

|.NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264_with_EventHub/index.ts) |
[Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264_with_EventHub/encoding-h264-with-eventhub-helper.py) |

## Create a thumbnail sprite

This samples shows how to encode with a custom Transform to create a thumbnail sprite.

| .NET | Node.JS | Python |
| ---- | ------- | ------- |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_SpriteThumbnail) | :small_blue_diamond: | [Python](https://github.com/IngridAtMicrosoft/media-services-v3-python/blob/main/VideoEncoding/Encoding_Sprite_Thumbnail/encoding-sprite-thumbnail-helper.py) |

## Create a thumbnail sprite (VTT) in JPG format

This sample shows how to generate a VTT Sprite Thumbnail in JPG format and how to set the columns and number of images. It also shows a speed encoding mode in H264 for a 720P layer.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_Sprite_Thumbnail/index.ts) |  :small_blue_diamond: |

## Use content aware encoding with H264

This sample is an example of using the standard encoder with Content Aware encoding to automatically generate the best quality adaptive bitrate streaming set based on an analysis of the source files contents.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
|[.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_H264_ContentAware) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264_ContentAware/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264_ContentAware/encoding-h264-contentaware-helper.py) |

## Use content aware encoding constrained with H264

This sample demonstrates how to control the output settings of the Content Aware encoding H264 preset to make the outputs more deterministic to your encoding needs and costs. This will still auto generate the best quality adaptive bitrate streaming set based on an analysis of the source files contents, but constrain the output to your desired ranges.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
|[.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_H264_ContentAware_Constrained) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264_ContentAware_Constrained/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264_ContentAware_Constrained/encoding-h264-contentaware-constrained-helper.py) |

## Use an overlay image

This sample shows you how to upload an image file and overlay on top of video with output to MP4 container.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_OverlayImage) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264_OverlayImage/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264_OverlayImage/encoding-h264-overlayimage-helper.py) |

## Rotate a video

This sample shows how to use the rotation filter to rotate a video by 90 degrees.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264_Rotate90degrees/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264_Rotate90degrees/encoding-h264-rotate90degrees-helper.py) |

## Output to MPEG transport stream format

This sample shows how to use the standard encoder to encode a source file and output to MPEG Transport Stream format using H264 format with AAC audio and PNG thumbnail.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_H264_To_TransportStream/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_H264_To_TransportStream/encoding-h264-to-transportstream-helper.py) |

## Encode with HEVC

This sample shows how to use the standard encoder to encode a source file into HEVC format with AAC audio and PNG thumbnails.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_HEVC) | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_HEVC/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_HEVC/encoding-hevc-helper.py) |

## Use content aware encoding with HEVC

This sample is an example of using the standard encoder with Content Aware encoding to automatically generate the best quality HEVC (H.265) adaptive bitrate streaming set based on an analysis of the source files contents.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_HEVC_ContentAware)| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_HEVC_ContentAware/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_HEVC_ContentAware/encoding-hevc-contentaware-helper.py) |

## Use content aware encoding constrained with HEVC

This sample demonstrates how to control the output settings of the Content Aware HEVC encoding preset to make the outputs more deterministic to your encoding needs and costs. This will still auto generate the best quality adaptive bitrate streaming set based on an analysis of the source files contents, but constrain the output to your desired ranges.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_HEVC_ContentAware_Constrained/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_HEVC_ContentAware_Constrained/encoding-hevc-contentaware-constrained-helper.py) |

## Bulk encode from a remote Azure storage account using SAS URLs

This samples shows how you can point to a remote Azure Storage account using a SAS URL and submit batches of encoding jobs to your account, monitor progress, and continue. You can modify the file extension types to scan for (e.g - .mp4, .mov) and control the batch size submitted. You can also modify the Transform used in the batch operation. This sample demonstrates the use of SAS URLs as ingest sources to a Job input. Make sure to configure the `REMOTESTORAGEACCOUNTSAS` environment variable in the .env file for this sample to work.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_Bulk_Remote_Storage_Account_SAS/index.ts) |  :small_blue_diamond: |

## Copy live archive to MP4 file format for export or use with Video Indexer

This sample demonstrates how to use the archived output from a live event and extract only the top highest bitrate video track to be packaged into an MP4 file for export to social media platforms, or for use with Video Indexer. The key concept in this sample is the use of an input definition on the Job InputAsset to specify a VideoTrackDescriptor. The SelectVideoTrackByAttribute allows you to select a single track from the live archive by using the bitrate attribute, and filtering by the "Top" video bitrate track in the live archive.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| :small_blue_diamond: | [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_Live_Archive_To_MP4/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/EncodingLiveArchiveMP4/encoding-live-archive-to-mp4-helper.py) |

## Encode a multi-channel audio source file

This sample demonstrates how to create an encoding Transform that uses channel mappings and audio track selection from the input source to output two new AAC audio tracks. The standard encoder is limited to outputting 1 Stereo track, followed by a 5.1 surround sound audio track in AAC format.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_MultiChannel_Audio)| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_MultiChannel_Audio/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_MultiChannel_Audio/encoding-multichannel-audio-helper.py) |

## Stitch and edit two assets together

This sample demonstrates how to stitch and edit together two or more assets into a single MP4 file using the JobInputSequence as part of a job submission.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_StitchTwoAssets)| [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/VideoEncoding/Encoding_Stitch_Two_Assets/index.ts) | [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/VideoEncoding/Encoding_Stitch_Two_Assets/encoding-stitch-two-assets-helper.py) |

## Encode with Constant Rate Factor Preset for H.264

This sample shows how to create a custom encoding Transform using custom H.264 Constant Rate Factor (CRF) encoding settings.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_H264_ConstantRateFactor) | :small_blue_diamond: | :small_blue_diamond: |

## Encode with MES adaptive bitrate predefined preset from an HTTP source URL

This sample demonstrates how to create an encoding Transform that uses a built-in preset for adaptive bitrate encoding and ingests a file directly from an HTTPs source URL, publish output asset for streaming, and download results for verification.

| .NET | Node.JS | Python |
| ---- | ------- | ------ |
| [.NET](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/main/VideoEncoding/Encoding_PredefinedPreset) | :small_blue_diamond: | :small_blue_diamond: |

[!INCLUDE [media-services-community](../includes/media-services-community.md)]
