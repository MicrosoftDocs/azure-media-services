---
title: How to use WebVTT files with Azure Media Services and Azure Media Player
description: This article describes the steps for using captions and subtitles with Azure Media Services and displaying them with Azure Media Player. In general, text tracks are used for closed captioning that enables viewers who need accessibility features in a video player to understand what is being said and sounds exist in a video. Subtitles, are text tracks that show the speech and sounds in a different language than the source language. For example, if the source language of a video is English, then the text track would be considered a caption. If an additional language text track is provided, it's considered a subtitle.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 09/22/2022
ms.author: inhenkel
---

# Use WebVTT files with Azure Media Services and Azure Media Player

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article describes the steps for using captions and subtitles with Azure Media Services and displaying them with Azure Media Player. You'll be setting up either the dynamic or static [WebVTT player demo](https://amp.azure.net/libs/amp/latest/samples/dynamic_webvtt.html)as seen in the Azure Media Player documentation.

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

## Set up captions and subtitles for the Azure Media Player

Choose which sample code you are going to use for the Azure Media Player.

1. Review the sample code:
    1. For the dynamic version, see [Dynamic WebVTT Azure Media Player](https://github.com/Azure-Samples/azure-media-player-samples/blob/master/html/dynamic_webvtt.html).
    1. For the static version, see [Static WebVTT Azure Media Player](https://github.com/Azure-Samples/azure-media-player-samples/blob/master/html/videotag_webvtt.html).
1. Create a new HTML page and copy and paste the code from either the dynamic or static version of the page into the page.

## Upload the video with the Azure portal

For this exercise, use the Azure portal to upload the video.

[!INCLUDE [task-upload-file-to-asset-portal](includes/task-upload-file-to-asset-portal.md)]

## Create a transform

Videos uploaded to an asset must be encoded in order for them to be streamed. Media Services provides built-in encoders. For this example, use either the *ContentAware* or *AdaptiveStreaming* encoder.

[!INCLUDE [task-create-transform-portal](includes/task-create-transform-portal.md)]

## Create a job

After you've created a transform, create a job that uses the transform to encode the video.  The output asset will be where you upload captions.

[!INCLUDE [task-create-job-portal](includes/task-create-job-portal.md)]

## Upload captions

Once the job is completed, the resulting files from the encoder will be in the output asset.  **You will use this asset going forward.**

1. Navigate to the output asset.
1. Select **Upload captions**.
1. Upload the WebVTT files you create for the source language and Spanish.

## Edit the manifest

Since this example uses the Azure portal, edit the manifest file in the portal as well.

1. You should already be on the output asset screen.
1. Select the **storage container link**.  The storage container name starts with the "asset-" prefix. The storage container screen will appear.
1. Select the `.ism` file from the file list. The blob screen will appear.
1. Select **Edit**.
1. Copy and paste the following XML above the `</switch>` element, changing the VTT file names to the ones you've uploaded.

    ```html
    <textstream src="english.vtt" systemBitrate="0">
        <param name="textDisplayName" value="English" valuetype="data" />
        <param name="outputFlag" value="2" valuetype="data" />
        <param name="armId" value="english.vtt" valuetype="data" />
    </textstream>
    <textstream src="spanish.vtt" systemBitrate="0">
        <param name="systemBitrate" value="0" valuetype="data" />
        <param name="textDisplayName" value="Spanish" valuetype="data" />
        <param name="outputFlag" value="2" valuetype="data" />
        <param name="armId" value="spanish.vtt" valuetype="data" />
    </textstream>
    ```

## Start streaming

So you can complete the rest of the steps, create a streaming locator for the asset.

### Create a streaming locator

1. Navigate to the Media Services account you want to work with.
1. Select **Assets** from the menu. The assets screen will appear.
1. Under Streaming locators, select **+ New streaming locator**. The Add streaming locator screen will appear.
1. Enter a name for the streaming locator in the **Name** field, if you want to change the default name.
1. Select the Predefined_DownloadAndClearStreaming streaming policy from the **Streaming policy** dropdown list.
1. Select **Add**. The video will start playing in the player on the screen, and the **Streaming URL** field will be populated.
1. Select **Show URLs** in the Streaming locator list. The Streaming URLs screen will appear.
1. Copy one of the streaming URLs onto your clipboard.  You'll be using this value to configure the player.

> [!IMPORTANT]
> You must select the Predefined_DownloadAndClearStreaming streaming policy or the text tracks will not be rendered in the player. Also, remember to start the streaming endpoint.  Once the streaming endpoint starts, billing starts.

## Using the manifest and WebVTT URLs

The path for both the manifest and WebVTT URLs should be the same when they're located in the same asset as below:

`https://myamsaccount-usw22.streaming.media.azure.net/5aa2a1ca-6ab2-492a-b881-76ded8c75fac/myvideo.ism/manifest(format=m3u8-cmaf)`

`https://myamsaccount-usw22.streaming.media.azure.net/5aa2a1ca-6ab2-492a-b881-76ded8c75fac/english.vtt`

You'll use these paths to configure the player.

## [Dynamic](#tab/dynamic/)

### Edit the dynamic source code

You'll be editing the following lines:

```html
myPlayer.src(
    [
        { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TearsOfSteel_WAMEH264SmoothStreaming720p.ism/manifest", type: "application/vnd.ms-sstr+xml" },
    ],
    [
        { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TOS-en.vtt", srclang: "en", kind: "subtitles", label: "english" },
        { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TOS-es.vtt", srclang: "es", kind: "subtitles", label: "spanish" },
        { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TOS-fr.vtt", srclang: "fr", kind: "subtitles", label: "french" },
        { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TOS-it.vtt", srclang: "it", kind: "subtitles", label: "italian" }
    ]
);
```

### Get the manifest URL

1. From the streaming locator list in the asset screen, select **Show URLS**. The streaming locator screen will appear.
1. Copy one of the URLs, HLS, DASH, or Smooth streaming onto your clipboard.
1. Paste the URL into the `src` value for the manifest.

    ```html
    { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TearsOfSteel_WAMEH264SmoothStreaming720p.ism/manifest", type: "application/vnd.ms-sstr+xml" }
    ```

### Paste the WebVTT URL

Use the same path for the WebVTT file as you did for the manifest and append it with the VTT file name.

1. Paste the URL for the source language into the `src` value for the first language.
1. Change the `srclang` value to the language designator for your source language.
1. You can change the `kind` value to "caption", leave it as "subtitles" and/or add an additional line and change the value to "caption" to designate the source language as both a caption and subtitles.

   ```html
    { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TOS-en.vtt", srclang: "en-us", kind: "subtitles", label: "english" },
    ```

1. Change the `srclang` value to the language designator for your second language, in this case, Spanish, which is *es-us*.

    ```html
    { src: "//ams-samplescdn.streaming.mediaservices.windows.net/11196e3d-2f40-4835-9a4d-fc52751b0323/TOS-es.vtt", srclang: "es", kind: "subtitles", label: "spanish" },
    ```

1. Delete the rest of the language lines unless you want to use them and have uploaded WebVTT file for them.

## [Static](#tab/static/)

### Edit the static source code

You'll be editing the following lines:

```html
<video id="azuremediaplayer" class="azuremediaplayer amp-default-skin amp-big-play-centered" autoplay controls width="640" height="400" poster="" data-setup='{}' tabindex="0">
            <source src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TearsOfSteel.ism/manifest" type="application/vnd.ms-sstr+xml" />
            <track kind="subtitles" src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TOS-en.vtt" srclang="en" label="English">
            <track kind="subtitles" src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TOS-es.vtt" srclang="es" label="Spanish">
            <track kind="captions" src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TOS-fr.vtt" srclang="fr" label="French">
            <track kind="subtitles" src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TOS-it.vtt" srclang="it" label="Italian">
            <p class="amp-no-js">To view this video please enable JavaScript, and consider upgrading to a web browser that supports HTML5 video</p>
        </video>
```

### Get the manifest URL

1. From the streaming locator list in the asset screen, select **Show URLS**. The streaming locator screen will appear.
1. Copy one of the URLs, HLS, DASH, or Smooth streaming onto your clipboard.
1. Paste the URL into the `src` value for the manifest.

    ```html
    <source src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TearsOfSteel.ism/manifest" type="application/vnd.ms-sstr+xml" />
    ```

### Paste the WebVTT URL

Use the same path for the WebVTT file as you did for the manifest and append it with the VTT file name.

1. Paste the URL for the source language into the `src` value for the first language.
1. Change the `srclang` value to the language designator for your source language.
1. You can change the `kind` value to "caption", leave it as "subtitles" and/or add an additional line and change the value to "caption" to designate the source language as both a caption and subtitles.

   ```html
    <track kind="subtitles" src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TOS-en.vtt" srclang="en-us" label="English">
    ```

1. Paste the URL for the source language into the `src` value for the second language.
1. Change the `srclang` value to the language designator for your second language, in this case, Spanish, which is *es-us*.

    ```html
    <track kind="subtitles" src="//amssamples.streaming.mediaservices.windows.net/bc57e088-27ec-44e0-ac20-a85ccbcd50da/TOS-es.vtt" srclang="es-us" label="Spanish">
    ```

1. Delete the rest of the language lines unless you want to use them and have uploaded WebVTT files for them.

---

## View the video with captions

1. Make sure the the streaming endpoint is started.
1. Open the hosted HTML page in a browser.
1. Select the text track for the language of your choice from the captions or subtitles list.