---
title: How to edit a text track in the Azure portal
description: Your live event is over and you have used live transcription to create a VTT or TTML file for use with captions and transcripts for the captured video.  However, the live transcription will likely need some editing.  You may later want to deliver the text in multiple languages and allow your viewers to choose which to use in the player.  This article covers how to edit the source VTT file in the Azure portal.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 02/14/2023
ms.author: inhenkel
---

# How to edit a text track in the Azure portal

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

When your live event has used live transcription to create a VTT or TTML file for use with captions and transcripts for the captured video, it's likely that the live transcription will need some editing.  You may also want to deliver the text in multiple languages and allow your viewers to choose which to use in the player.  This article covers how to edit the source VTT file in the Azure portal.

## Find and edit the track

[!INCLUDE [task-list-tracks-portal](includes/task-list-tracks-portal.md)]

## Edit the track

There are two ways to edit the track. You can either edit the track in the Azure portal or download the track and edit it locally.

> [!WARNING]
> Be careful that you don't edit the timestamps!

### Edit the track in the Azure portal

1. Select **Edit captions** next to the track you want to edit. The Captions editing screen will appear.
1. Edit the file.
1. Select **Save**.

### Download and edit the track

1. Select the **vertical ellipsis** next to the text track you want to work with. **NOTE:** Live transcription text tracks are usually named *auto-generated-best_4800.vtt*.
1. Select **Download**. Save the file locally.
1. Open the file in your favorite text edit.
1. Edit the text or correct anything that live transcription didn't capture.
1. Save the edited file.

[!INCLUDE [task-upload-captions](includes/task-upload-captions.md)]

[!INCLUDE [task-view-captions-ism](includes/task-view-captions-ism.md)]

[!INCLUDE [media-services-community](includes/media-services-community.md)]
