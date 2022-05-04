---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Unable to upload media
---

<!-- 2204120050001942 -->

## Unable to upload media

You are unable to upload media to a storage account.

| Cause | Solution |
| ----- | -------- |
| You are attempting to use HTTP. | Use HTTPS. The HTTP protocol is no longer supported for uploading content.  |
| You aren't waiting long enough for the storage account to be deployed. | If you created the storage account programmatically, add code to test that the storage account is deployed before attempting to upload media. |
