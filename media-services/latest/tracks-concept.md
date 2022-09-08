---
title: Media Services asset tracks
description: Media Services offers the Tracks API so you can deliver text tracks with complete sentences and proper punctuation right after a live event is over, enable accessibility player features for the viewer, allow viewers to select the text and audio tracks of their choice.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 08/10/2022
ms.author: inhenkel
---

# Media Services Tracks API

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

A video asset usually contains audio and video tracks. Sometimes it also contains text tracks for captions or subtitles.  The Tracks API gives you information about the tracks that are in an asset. It also allows you to edit a text track and let the player know they are available.

With the Tracks API you can:

- Get the list of audio, video and text tracks in an asset.
- Add or remove text tracks from an asset.
- Specify accessibility attributes of an asset.
- Get the download URL a text track so you can edit it, and then upload it back into the asset.
- Show or hide a text track in a video player with settings in the HLS playlist or DASH manifest.

The last two features are especially useful for live events. We produce two text tracks during a live event when live transcription is turned on. The real-time transcript contains partial sentences. The slightly delayed second track has better punctuations and complete sentences. The first transcript is available as fragmented text files. The second one is available as a single WebVTT file that can be downloaded and edited.

## General workflow for text tracks

1. Create a live event with live transcription enabled.
1. When the live event is over, make the output asset available for a VOD application.
1. Download and edit the source language VTT or TTML files for complete sentences and proper punctuation.
1. To present the text track in multiple languages, translate the source text track to those languages and save them as separate files for each language.
1. Upload the edited source language track, and the text tracks for each language.
1. Hide the live transcription text track, and show the text track in the language that is appropriate for the viewer.

## How-tos, tutorials and quickstarts

- [How to list the audio, video and text tracks in an asset](tracks-list-how-to.md)
- [How to edit and upload VTT files in the Azure portal](tracks-edit-track-portal-how-to.md) produced during a live event after the live event is no longer live and is now available as a VOD asset. You can upload additional WebVTT tracks using the same method.

## Samples

- [Node.JS List tracks in an asset](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/list-tracks-in-asset.ts)
- [Node.JS Add WebVTT files to an asset](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/main/Assets/add-WebVTT-tracks.ts)
