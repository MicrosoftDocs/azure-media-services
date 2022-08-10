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

Media Services offers the Tracks API so you can:

- Deliver text tracks with complete sentences and proper punctuation right after a live event is over.
- Enable accessibility player features for the viewer.
- Allow viewers to select the text and audio tracks of their choice.

## Tracks general workflow

### Text tracks workflow

1. Create a live event with live transcription enabled.
1. When the live event is over, make the output asset available for a VOD application.
1. Download and edit the source language VTT or TTML files for complete sentences and proper punctuation.
1. To present the text track in multiple languages, translate the source text track to those languages and save them as separate files for each language.
1. Upload the edited source language track, and the text tracks for each language.
1. Hide the live transcription text track, and show the text track in the language that is appropriate for the viewer.

### Audio tracks workflow

1. When the live event is over, make the output asset available for a VOD application.
1. Download the source audio track and/or the source text track for audio translation into multiple languages.
1. **ADD METADATA to the local audio tracks?**
1. Upload the additional audio tracks.

### Descriptive or director's commentary audio track workflow

1. Use the method works best for you to product the descriptive audio track or director's commentary audio track. You have the option to download the video from the Azure portal so the narration can be done offline.
1. **ADD METADATA to the local audio tracks?**
1. Upload the audio tracks to the live event asset that is available for your VOD application.

## How-tos, tutorials and quickstarts

**FILES WITH NO LINK ARE YET TO BE WRITTEN**

### Text tracks
- [How to list the audio, video and text tracks in an asset](tracks-list-how-to.md)
- [How to edit and upload VTT files in the Azure portal](tracks-edit-track-portal-how-to.md) produced during a live event after the live event is no longer live and is now available as a VOD asset
- How to hide or show text tracks in the video player
- How to allow viewers to select the right text track to be displayed during playback
- How to hide the live transcription text track produced during a live event

### Audio tracks
- How to upload additional audio tracks to an existing asset.
- How to add accessibility signals to the DASH manifest or HLS playlist.
- How to edit the properties of an audio track such as specifying the name and language of an audio track.