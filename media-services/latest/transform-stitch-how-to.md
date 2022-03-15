---
title: How to stitch two or more video files | Microsoft Docs
description: This article shows how to stitch two or more video files.
services: media-services
author: IngridAtMicrosoft
manager: femila
ms.service: media-services
ms.topic: how-to
ms.date: 03/09/2022
ms.author: inhenkel
---

# How to stitch two or more video files

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Stitch two or more video files

The following example illustrates how you can generate a preset to stitch two or more video files. The most common scenario is when you want to add a header or a trailer to the main video.

> [!NOTE]
> Video files edited together should share properties (video resolution, frame rate, audio track count, etc.). You should take care not to mix videos of different frame rates, or with different number of audio tracks.

## [.NET](#tab/net/)

## Prerequisites

Clone or download the [Media Services .NET samples](https://github.com/Azure-Samples/media-services-v3-dotnet/). 

## Example

Find the code that shows how to stitch video files in [EncodingWithMESCustomStitchTwoAssets folder](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/VideoEncoding/Encoding_StitchTwoAssets/Program.cs).
