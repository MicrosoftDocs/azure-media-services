---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/23/2022
ms.author: inhenkel
---

> [!WARNING]
> It is not advised to attempt to wrap the REST API for Media Services directly into your own library code, as doing so properly for production purposes would require you to implement the full Azure Resource Management retry logic and understand how to manage long running operations in Azure Resource Management APIs. This is handled by the client SDKs for various languages - .NET, Java, TypeScript, Python, etc. - automatically and reduces the chances of you having issues with retry logic or failed API calls. The client SDKs all handle this for you already.
