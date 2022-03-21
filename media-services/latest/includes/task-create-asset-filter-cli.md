---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
ms.custom: CLI, devx-track-azurecli
---

### Create or update an asset filter in the portal

1. Navigate to the Media Services account you want to work with.
1. Select **Assets**. The assets screen will appear.
1. Select the asset you want to work with from the list.

### Add a filter

1. Select **+ Add an asset filter**. The Add asset filter screen will appear.
1. Enter a name in the **Asset filter name** field.

### Update a filter

1. Select a filter from the filters list. The Update asset filter screen will appear.

### Time constraints

1. Select the **Time range constraints** tab.
1. If you need to change the timescale of the filter, check the manifest to get the timescale and timestamps, enter a number into the **Timescale** field.
1. Optionally, you can set:
    1. The earliest timestamp that should appear in the playback manifest.
    1. The last timestamp that should appear in the playback manifest.
    1. The limit for rewinding content.
    1. How much time to daley your live broadcast.

### Track constraints

1. Select the **Track constraints tab**.
1. Enter the bitrate in the **HLS startup bitrate** field to set the first video track to appear in the HLS playlist to allow HLS native players to start downloading from this quality level.
1. From the **Track selection rules** dropdown lists, select the track, video, audio or text.
1. From the **Type dropdown** list select one of the conditions for the rule.
1. In the **Value** field, enter the value for the condition of the rule.

Once you have finished configuring the asset filter select **Save**.
