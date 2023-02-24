---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 02/24/2023
ms.author: inhenkel
title: Upload captions
---

## Upload captions

Once the job is completed, the resulting files from the encoder will be in the output asset.  **You will use this asset going forward.**

1. Navigate to the output asset used to hold the results of encoding.
1. Select **Add text track**.
1. Enter a name in the **Name** field. For example, for an English text track enter *English*.
1. Select **Upload new** radio button. Alternatively, if you have already created or uploaded a VTT file, you can select the **Use existing** radio button and select the track.
1. Enter the text to be displayed in the player in the **Display name** field.
1. Select either **Visible** radio button to ensure that the track will be displayed in the player client.
1. Select the **HLS settings** checkboxes to set the track as the default track and/or set forced. For English, set it as the default track.
1. Select the **Accessibility characteristics** checkboxes to identify what accessibility guideline the text track is used for.
1. Select **I agree and upload** to upload the text track.
