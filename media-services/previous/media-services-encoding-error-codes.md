---
title: Azure Media Services encoding error codes
description: This topic lists error codes that could be returned in case an error was encountered during the encoding task execution..
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: article
ms.date: 10/05/2022
---

<!-- ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2 -->

# Encoding error codes

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.  To get error details in your .NET code, use the [ErrorDetails](/previous-versions/azure/jj126075(v=azure.100)) class. To get error details in your REST code, use the [ErrorDetail](/rest/api/media/operations/errordetail) REST API.

| ErrorDetail.Code | Possible causes for error |
| --- | --- |
| Unknown |Unknown error while executing the task |
| ErrorDownloadingInputAssetMalformedContent |Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on. |
| ErrorDownloadingInputAssetServiceFailure |Category of errors that covers problems on the service side - for example network or storage errors while downloading. |
| ErrorParsingConfiguration |Category of errors where task \<see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML. |
| ErrorExecutingTaskMalformedContent |Category of errors during the execution of the task where issues inside the input media files cause failure. |
| ErrorExecutingTaskUnsupportedFormat |Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration. For example, trying to produce an audio-only output from an asset that has only video |
| ErrorProcessingTask |Category of other errors that the media processor encounters during the processing of the task that are unrelated to content. |
| ErrorUploadingOutputAsset |Category of errors when uploading the output asset |
| ErrorCancelingTask |Category of errors to cover failures when attempting to cancel the Task |
| TransientError |Category of errors to cover transient issues (eg. temporary networking issues with Azure Storage) |

To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
