---
title: How to get a Media Processor instance using REST
description: Learn how to create a media processor component to encode, convert format, encrypt, or decrypt media content for Azure Media Services.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: article
ms.date: 3/10/2021
---

<!-- ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41 -->

# How to get a Media Processor instance

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)


## Overview

Media Processors are a component that handles a specific video or audio processing task, such as encoding, format conversion, encrypting, or decrypting media content. All tasks submitted to Media Services require a media processor to encode, encrypt, or convert the video or audio content.

## Azure media processors

The following topic provides lists of media processors:

* [Encoding media processors](scenarios-and-availability.md)
* [Analytics media processors](scenarios-and-availability.md)

>[!NOTE]
>When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).

## Connect to Media Services

For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).


## Get a media processor

The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).

Request:

```console
GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/json
Accept-Charset: UTF-8
User-Agent: Microsoft ADO.NET Data Services
Authorization: Bearer <token>
x-ms-version: 2.19
Host: media.windows.net
```

Response:

```console
. . .

{
   "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
   "value":[
      {
         "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
         "Description":"Media Encoder Standard",
         "Name":"Media Encoder Standard",
         "Sku":"",
         "Vendor":"Microsoft",
         "Version":"1.1"
      }
   ]
}
```
