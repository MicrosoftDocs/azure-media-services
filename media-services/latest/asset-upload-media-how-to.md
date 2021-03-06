---
title: Upload media
description: Learn how to upload media for streaming or encoding.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 3/16/2022
ms.author: inhenkel
---

# Upload media for streaming or encoding

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

In Media Services, you upload your digital files (media) into a blob container associated with an asset. The [Asset](/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files). Once the files are uploaded into the asset's container, your content is stored securely in the cloud for further processing  and streaming.

## Collect values

Before you get started, you'll need to collect or think about a few values.

1. The local file path to the file you want to upload
1. The asset ID for the asset (container)
1. The name you want to use for the uploaded file including the extension
1. The name of the storage account you are using
1. The access key for your storage account

## File naming

[!INCLUDE [reserved_characters](./includes/reserved_characters.md)]

## [Portal](#tab/portal/)

[!INCLUDE [Upload files with the portal](./includes/task-upload-file-to-asset-portal.md)]

## [CLI](#tab/cli/)

[!INCLUDE [Upload files with the CLI](./includes/task-upload-file-to-asset-cli.md)]

## [Python](#tab/python)

Assuming that your code has already established authentication and you have already created an input Asset, use the following code snippet to upload local files to that asset (in_container).

```python
#The storage objects
from azure.storage.blob import BlobServiceClient, BlobClient

#Establish storage variables
storage_account_name = '<your storage account name'
storage_account_key = '<your storage account key'
storage_blob_url = 'https://<your storage account name>.blob.core.windows.net/'

in_container = 'asset-' + inputAsset.asset_id

#The file path of local file you want to upload
source_file = "ignite.mp4"

# Use the Storage SDK to upload the video
blob_service_client = BlobServiceClient(account_url=storage_blob_url, credential=storage_account_key)
blob_client = blob_service_client.get_blob_client(in_container,source_file)

# Upload the video to storage as a block blob
with open(source_file, "rb") as data:
    blob_client.upload_blob(data, blob_type="BlockBlob")
```

---
<!-- add these to the tabs when available -->
For other methods see the [Azure Storage documentation](/azure/storage/blobs/) for working with blobs in [.NET](/azure/storage/blobs/storage-quickstart-blobs-dotnet), [Java](/azure/storage/blobs/storage-quickstart-blobs-java), [Python](/azure/storage/blobs/storage-quickstart-blobs-python), and [JavaScript (Node.js)](/azure/storage/blobs/storage-quickstart-blobs-nodejs).
