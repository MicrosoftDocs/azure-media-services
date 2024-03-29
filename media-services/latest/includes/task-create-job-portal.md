---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/01/2022
ms.author: inhenkel
title: Create a job in the portal

---

### Create a job in the portal

1. Navigate to the Media Services account you want to work with.
1. Select **Transforms + jobs** from the menu.
1. Select the transform you want to use for the job. The transform screen will appear.
1. Select **Add job**. The Create a job screen will appear.
1. For the **Input source**, the **Asset** radio button should be selected by default.  If not, select it now.
1. Select **Select an existing asset**. The Select an asset screen will appear.
1. Select one of the assets in the list. You can only select one at a time for the job.
1. Select **Select**.
1. For the transform, select the **Use existing** radio button.
1. Select a transform from the **Transform** dropdown list.
1. Under Configure output, default settings will be auto-populated. You can leave them as they are or change them.
1. Select **Create**.
1. Select **Transforms + Jobs**. The transform will now show up in the table of jobs along with its status.
1. To see details about the job, select the job listed under **Name** in the table of jobs. The job detail screen will open.
1. Select the output asset **Asset name** from the **Outputs** list. The asset screen will open.
1. Select the link for the asset next to Storage container.  A new browser tab will open and you'll see the results of the job that used the transform.  There should be several files in the output asset such as:
    1. Encoded video files with .mpi and .mp4 extensions.
    1. A *XXXX_.ism* file.
    1. A *XXXX.isc* file.
    1. A *ThumbnailXXXX.jpg* file.
