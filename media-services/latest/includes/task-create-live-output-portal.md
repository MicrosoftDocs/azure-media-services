---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
---

### Create a live output in the portal

If you plan to encode a live event for streaming, you must create an output asset to house the resulting files.

If you aren't already at the live event screen:

1. Navigate to the Media Services account you want to work with.
1. Select **Live streaming** from the menu.
1. Select the live event you want to work with.

At the live event screen:

1. Select **+ Create an output**. The Create an output screen will appear.
1. Enter a name for the output in the **Name** field.
1. Enter the Days, Hours, Minutes and Seconds for the **Rewind window** fields. The rewind window determines the maximum length of content saved in the asset and how far back in time a viewer can go from the current live position in the client player. The default is 0 days, 8 hours, 0 minutes, and 0 seconds.
1. Enter a new asset name if you don't want the one that is automatically generated in the **Asset name** field.
1. Select the storage account from the **Asset storage account** dropdown list that you want to house the asset. The list will include all of the storage accounts associated with the Media Services account.
1. Enter a manifest name in the **Manifest file name** field.

#### Advanced settings

To set an archive start timestamp, enter the timestamp in the **Archive start timestamp** field.
To set the HLS package settings, enter the number of fragments per second in the **Fragments per HLS segment** field.
