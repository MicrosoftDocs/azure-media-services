---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Can't start a streaming endpoint
---

<!-- 2203080030000664 -->

## A streaming endpoint won't start.

| Cause | Solution |
| ----- | -------- |
| You may have created a custom policy that enables only HTTPS.  This is not currently supported by Media Services. | **Possible workarounds:**<br/>1. In the Azure portal, disable your custom policy.<br/>2. Create a streaming endpoint with a CDN enabled and disable HTTP for the CDN endpoint.<br/>**Or**<br/>1. Don't enable the CDN for the streaming endpoint with the portal or the API.<br/>2. Instead, go to the Azure CDN page in the Azure portal or use the Azure CDN API to create an endpoint that points to the Media Services endpoint, setting the origin for the CDN endpoint to the hostname for the streaming endpoint.<br/> |
| You may have stopped a streaming endpoint with a CDN. | See [Streaming endpoint won't stop](#a-streaming-endpoint-with-a-cdn-wont-stop) |