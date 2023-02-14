---
title: How to use WebVTT files with Azure Media Services
description: This article describes the steps for using captions and subtitles with Azure Media Services and displaying them with Azure Media Player. In general, text tracks are used for closed captioning that enables viewers who need accessibility features in a video player to understand what is being said and sounds exist in a video. Subtitles, are text tracks that show the speech and sounds in a different language than the source language. For example, if the source language of a video is English, then the text track would be considered a caption. If an additional language text track is provided, it's considered a subtitle.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 02/14/2023
ms.author: inhenkel
---

# Use WebVTT files with Azure Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article describes the steps for using captions and subtitles with Azure Media Services in the Azure portal.

> [!NOTE]
> This article does **not** discuss using Media Services live transcription or the Tracks API.

## Captions vs subtitles

In general, *captions* are text tracks that are used for closed captioning that enables viewers who need accessibility features in a video player to understand what is being said and the sounds that exist in a video. *Subtitles*, are text tracks that show the speech and sounds in a different language than the source language.

For example, if the source language of a video is English, then the text track would be considered a *caption*. If an additional language text track is provided, it's considered a *subtitle*. You can use one text track for both a caption and subtitles, but implementation varies between video player clients.

## Prerequisites

- An Azure subscription.
- A Media Services account.
- Follow the steps in the [Azure Media Player Full Setup](/azure/media-services/azure-media-player/azure-media-player-full-setup) article. Use either the static or dynamic version.
- Create a video with audio.
- Export captions using your favorite video editing software in WebVTT format. If your editing software doesn't export captions to this format, there are many online conversion tools you can use to covert the file.
- Translate the captions from the source language to another language and save the file with a different name than the source language.

For example, save the source language file in your native language, then use an online tool to translate the text in the file to Spanish.

> [!WARNING]
> Be careful not to edit the timestamps!

The resulting files should look like this:

| English VTT file | Spanish VTT file |
| ---------------- | ---------------- |
| WEBVTT<br/><br/>00:05.400 --> 00:10.833<br/>Hi. In this video we are going to learn how to use<br/><br/>00:10.833 --> 00:16.266<br/>captions and subtitles with Azure Media Services<br/><br/>00:16.266 --> 00:23.532<br/>and Azure Media Player.|WEBVTT<br/><br/>00:05.400 --> 00:10.833<br/>Hola. En este video vamos a aprender a usar<br/><br/>00:10.833 --> 00:16.266<br/>leyendas y subtítulos con Azure Media Services<br/><br/>00:16.266 --> 00:23.532<br/>y Azure Media Player.|

## Filenames

It is recommended that you name the files using language designators. For this example, the English file would be named *en-us.vtt*.  The Spanish file would be named *es-es.vtt*.

## Upload the video with the Azure portal

For this exercise, use the Azure portal to upload the video.

[!INCLUDE [task-upload-file-to-asset-portal](includes/task-upload-file-to-asset-portal.md)]

## Create a transform

Videos uploaded to an asset must be encoded in order for them to be streamed. Media Services provides built-in encoders. For this example, use the *ContentAwareEncoding* encoder.

[!INCLUDE [task-create-transform-portal](includes/task-create-transform-portal.md)]

## Create a job

After you've created a transform, create a job that uses the transform to encode the video.  The output asset will be where you upload captions.

[!INCLUDE [task-create-job-portal](includes/task-create-job-portal.md)]

Once the job is completed, the resulting files from the encoder will be in the output asset.  **You will use this asset going forward.**

[!INCLUDE [task-upload-captions](includes/task-upload-captions.md)]

## Repeat steps

Repeat these steps for Spanish, except don't select **Set as default track** as you have already set English as the default track.

[!INCLUDE [task-view-captions-ism](includes/task-view-captions-ism.md)]

## Start streaming

So you can complete the rest of the steps, create a streaming locator for the asset.

### Create a streaming locator

1. Navigate to the Media Services account you want to work with.
1. Select **Assets** from the menu. The assets screen will appear.
1. Under Streaming locators, select **+ New streaming locator**. The Add streaming locator screen will appear.
1. Enter a name for the streaming locator in the **Name** field if you want to change the default name.
1. Select the *Predefined_DownloadAndClearStreaming* streaming policy from the **Streaming policy** dropdown list.
1. Select **Add**. If the streaming endpoint is running, the video will start playing in the player on the screen, and the **Playback URL** field will be populated.
1. If the streaming endpoint isn't running, select **Start streaming endpoint**.
1. Copy the Playback URL onto your clipboard.  You'll be using this value to configure the player.

> [!IMPORTANT]
> You must select the Predefined_DownloadAndClearStreaming streaming policy or the text tracks will not be rendered in the player. Also, remember to start the streaming endpoint.  Once the streaming endpoint starts, billing starts. Remember to turn it off when you are finished with this tutorial.

### Get the manifest URL

1. From the streaming locator list in the asset screen, select **Show URLS**. The streaming locator screen will appear.
1. Copy one of the URLs, HLS, DASH, or Smooth streaming onto your clipboard.
1. Use the URL as your player source value.

## View the video with captions

1. Make sure the the streaming endpoint is started.
1. Open the hosted HTML page in a browser.
1. Select the text track for the language of your choice from the captions or subtitles list.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
