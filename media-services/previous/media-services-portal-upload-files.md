---
title: Upload files to a Media Services account in the Azure portal
description: This tutorial walks you through the steps of uploading files to a Media Services account in the Azure portal.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: conceptual
ms.date: 10/07/2022
---

<!-- ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6 -->

# Upload files to a Media Services account in the Azure portal

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
>

> [!NOTE]
> No new features or functionality are being added to Media Services v2. See [Media Services v3](../latest/index.yml). Also, see [migration guidance from v2 to v3](../latest/migrate-v-2-v-3-migration-introduction.md)

In Azure Media Services, you upload your digital files to an asset. The asset can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata for these files). After the files are uploaded, your content is stored securely in the cloud for further processing and streaming.

Media Services has a maximum file size for processing files. For details about file size limits, see [Media Services quotas and limitations](media-services-quotas-and-limitations.md).

To complete this tutorial, you need an Azure account. For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

## Upload files

1. In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.
2. Select **Settings** > **Assets**. Then, select the **Upload** button.

    ![Upload files](./media/media-services-portal-vod-get-started/media-services-upload.png)

    The **Upload a video asset** window appears.

   > [!NOTE]
   > Media Services doesn't limit the file size for uploading videos.

3. On your computer, go to the video that you want to upload. Select the video, and then select **OK**.

    The upload begins. You can see the progress under the file name.

When the upload is finished, the new asset is listed in the **Assets** pane.
