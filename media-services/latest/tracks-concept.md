---
title: Media Services asset tracks
description: Media Services offers the Tracks API so you can deliver text tracks with complete sentences and proper punctuation right after a live event is over, enable accessibility player features for the viewer, allow viewers to select the text and audio tracks of their choice.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 01/17/2023
ms.author: inhenkel
---

# Media Services Tracks API

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

A Media Services asset contains media files in the associated Azure storage account. These files contain the data for audio, video and text tracks. The Tracks API allows you to understand and manage the tracks that are in the asset. The tracks are used by a DASH or HLS video player to present the audio, video and subtitles or captions (text) to the audience. A Media Services streaming endpoint communicates information about the tracks to a player via DASH manifests or HLS playlists when requested.

With the Tracks API you can:

- Get the list of audio, video and text tracks in an asset.
- Add or remove text tracks.
- Add or remove audio tracks.
- Specify accessibility attributes of the text or audio tracks.
- Get the download URL a text track so you can edit it, and then upload it back into the asset.
- Show or hide a text track in a video player with settings in the HLS playlist or DASH manifest.

> [!NOTE]
> You can only add or update a text track on a video-on-demand (VOD) asset. Additionally, audio late binding isn’t supported for live streaming assets.

## Text tracks

### Using text tracks with locally produced media

After you've produced a video locally and exported captions, you can upload those captions to the asset that contains your on-demand media.

General workflow for using text tracks with locally produced text:

1. Create a video and export captions to a file that is in VTT or TTML format.
1. Translate or otherwise edit the VTT or TTML file, and save copies for:
    1. A track for an additional language with descriptive text to meet accessibility requirements.
    1. A track for additional text for director's commentary.
1. IMPORTANT: You must add the language designator to the VTT header for the correct language to be displayed in the client player. For example:
    ```
    WEBVTT
    Language: en-us
    ```
1. Upload the video to Media Services
1. Create a transform and job to encode the video.
1. Upload the additional text tracks.
1. Edit (or update) the .ism file to tell the player which text tracks to use as well as their labeling and visibility by:
    1. Manually editing it in the portal, or
    1. Using the Tracks API to update the manifest programmatically.

### Using text tracks with live transcription

When live transcription is turned on for a live event, an additional WebVTT text track is created in addition to the real-time live transcription track that viewers see on the live video player. This WebVTT file contains the best version of the live transcript that contains full sentences instead of the partial, real-time results. You can download the .vtt file after the entire transcript is available and the live output is deleted.

> [!WARNING]
> The final auto generated live transcription VTT files are delayed for processing. Unless you wait for several minutes before deleting a live output, the content in the file will be truncated.  Additionally, live transcription is not available for use with multiple input streams for a live event.

General workflow for using live transcription text tracks:

1. Create a live event with live transcription enabled and with the source language selected.
1. When the live event is over, wait for several minutes, and then delete the live output.  The archived asset will be available for on-demand streaming.  Valid streaming URLs will still be accessible to your viewers.
1. List the tracks in the archived asset or view them in the portal. There will be a WebVTT file that contains the NBest transcription. It will have a .vtt extension. The file is named `auto-generated-best_XXX.vtt`.
1. Download and edit the WebVTT file.
1. To present the text track in multiple languages, translate the source text track to those languages and save them as separate files for each language using the .vtt extension.
1. Upload the source language track, and the text tracks for each language.
1. Edit (or update) the .ism file to tell the player which text tracks to use as well as their labeling and visibility by:
    1. [Manually editing it in the portal](tracks-edit-track-portal-how-to.md), or
    1. Using the [Tracks API](/rest/api/media/tracks/update-track-data?tabs=HTTP) to update the manifest programmatically using one of the SDKs or the CLI:
        1. [Node.JS](/javascript/api/@azure/arm-mediaservices/tracks?view=azure-node-latest#@azure-arm-mediaservices-tracks-beginupdatetrackdataandwait&preserve-view=true)
        1. [Python](/python/api/azure-mgmt-media/azure.mgmt.media.operations.tracksoperations?view=azure-python#azure-mgmt-media-operations-tracksoperations-begin-update-track-data&preserve-view=true)
        1. [.Net](/dotnet/api/microsoft.azure.management.media.tracksoperationsextensions.beginupdatetrackdata?view=azure-dotnet#microsoft-azure-management-media-tracksoperationsextensions-beginupdatetrackdata(microsoft-azure-management-media-itracksoperations-system-string-system-string-system-string-system-string)&preserve-view=true)
        1. [CLI](/cli/azure/ams/asset-track?view=azure-cli-latest#az-ams-asset-track-update-data&preserve-view=true)

> [!IMPORTANT]
> When updating the .ism file, make sure you hide the live transcription text track, and show the text track in the language that is appropriate for the viewer.

## Audio tracks

You can add additional audio tracks to an asset to provide your viewers with audio in different languages, add descriptive audio for accessibility, or add director's commentary.

### General workflow for audio tracks

1. Create additional audio tracks for the live event.  They can be audio in different languages or descriptive audio that is used for accessibility. You can also use an audio track for director's commentary.
1. Upload the audio tracks to the archived asset.
1. Update the track data by editing the manifest file in the portal or by updating the track data using REST, or an SDK.

> [!NOTE]
> When an audio or text track is removed, the underlying file is not removed from the storage container. Media Services sets the dynamic packager (streaming endpoint) to not show the the information about the track in the manifest or playlist requested by the video player.

For detailed Tracks API steps, see the Samples below.

## Samples

- [Node.JS List tracks in an asset](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-tracks-in-asset.ts)
- [Node.JS Add WebVTT files to an asset](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/add-WebVTT-tracks.ts)

## How-tos, tutorials and quickstarts

- [How to edit and upload VTT files in the Azure portal](tracks-edit-track-portal-how-to.md) produced during a live event. You can upload additional WebVTT tracks using the same method.
- [Use WebVTT files with Azure Media Services and Azure Media Player](amp-captions-tutorial.md)

[!INCLUDE [media-services-community](includes/media-services-community.md)]
