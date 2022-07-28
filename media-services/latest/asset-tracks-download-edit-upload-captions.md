---
title: Download, edit and upload a captions file
description: This topic shows how to use the tracks API to download, edit and upload a captions file for a asset.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 07/27/2022
ms.author: inhenkel
---

# Download, edit and upload a captions file

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

The tracks API enables you to download, edit and upload a captions file. You can make a text track visible or invisible to the player, add or delete a text track, or “update” contents of a text track. Media Services then converts the track into CMFT format after you have called `UpdateTrackData`.

## Sample workflow

1. Call tracks API to list all tracks available
2. Find the name and file name of the text track.
3. Download the text track from the asset using Azure Storage APIs.
4. Edit the text track
5. Call UpdateTrackData
6. Use PUT/PATCH to make the old text track invisible, and make the new text track visible.

## Sample code

### List tracks in an Asset

See the sample code for listing tracks in an asset in [Javascript](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-tracks-in-asset.ts) and [Python](https://github.com/Azure-Samples/media-services-v3-python/blob/main/Assets/list-tracks-in-asset.py).

List the audio, video and text tracks that will show up on a video player.
Add additional WebVTT or TTML files to a VOD asset, so that your content viewers can select the right text track to be displayed during playback.
Decide which text tracks will be shown or hidden in the video player.
Decide that my viewers will not see the live transcription track that was produced during live, and instead see the version that has complete sentences with proper punctuations that was automatically made available right after live event is over.
Edit the .webvtt file that was produced during live and made available right after it is no longer live. The edited version can be selected by my viewers on the player.