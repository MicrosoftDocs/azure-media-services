---
title: How to edit a text track in the Azure portal
description: Your live event is over and you have used live transcription to create a VTT or TTML file for use with captions and trancripts for the captured video.  However, the live transcription will likely need some editing.  You may later want to deliver the text in multiple languages and allow your viewers to choose which to use in the player.  This article covers how to edit the source VTT file in the Azure portal.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 09/08/2022
ms.author: inhenkel
---

# How to edit a text track in the Azure portal

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

When your live event has used live transcription to create a VTT or TTML file for use with captions and transcripts for the captured video, it is likely that the live transcription will need some editing.  You may also want to deliver the text in multiple languages and allow your viewers to choose which to use in the player.  This article covers how to edit the source VTT file in the Azure portal.

## Find and edit the track

[!INCLUDE [task-list-tracks-portal](includes/task-list-tracks-portal.md)]

### Download and edit the track

1. Select the **vertical ellipses** next to the text track you want to work with. Live transcription text tracks are usually named *auto-generated-best_4800.vtt*.
1. Select **Download**. Save the file locally.
1. Open the file in your favorite text edit.
1. Reminder: Be careful with the timestamps.
1. Edit the text and correct anything that live transcription didn't capture properly.
1. Check for complete sentences and grammar.
1. Save the edited file with either the same name if you plan to overwrite the source file, or with a different name if not.

### Upload the edited file

You can either upload a file with a different file name or you can overwrite the existing file.

1. Select **Upload**. The upload screen will appear.
1. Select **file icon** to select the file you want to upload. If the file already exists in the asset, you will get a warning message.
1. If you want to overwrite the file, select the **Overwrite** checkbox.
1. Select **Upload**. The file will begin uploading.

You can upload additional files in the same way you uploaded the edited file.

### Edit the .ism file to use the track

1. Navigate to the storage container associated with the asset.
1. Select the .ism file.  The file screen will appear.
1. Select edit to view and edit the .ism file.
1. Add the following XML to the .ism file.
1. Set the `systemLanguage` parameter to the language designator for the language. For example, "en-us" for United States English or "ja-JP" for Japanese.
1. Set the `trackID` to a number.
1. Set the `trackName` to the language for the track.
1. Set the `outputFlag` parameter to:
    1. `3` to tell the client player to display the track.
    1. `2` to tell the client player that the track should be WHAT?
    1. `1` to tell the client player to hide the track.

The example below sets the text track to visible.

```html

<textstream src="english.vtt" systemBitrate="4800" systemLanguage="en-us">
    <param name="trackID" value="1" valuetype="data" />
    <param name="trackName" value="english" valuetype="data" />
    <param name="outputFlag" value="3" valuetype="data" />
</textstream>

```
