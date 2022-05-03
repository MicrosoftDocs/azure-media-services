---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/03/2022
ms.author: inhenkel
title: Can't start a streaming endpoint
---

<!-- 2203080030000664 -->

## Can't start a streaming endpoint

### Cause

#### Custom policy

You may have created a custom policy that enables only HTTPS.  This is not currently supported by Media Services.

#### Streaming endpoint with CDN

You may have stopped a streaming endpoint with a CDN.

### Solution

#### Custom policy solution

Possible workarounds:

1. In the Azure portal, disable your custom policy.
1. Create a streaming endpoint with a CDN enabled and disable HTTP for the CDN endpoint.

Or

1. Don't enable the CDN for the streaming endpoint with the portal or the API.
1. Instead, go to the Azure CDN page in the Azure portal or use the Azure CDN API to create an endpoint that points to the Media Services endpoint, setting the origin for the CDN endpoint to the hostname for the streaming endpoint.

#### Streaming endpoint and CDN solution

See [Streaming endpoint won't stop](#a-streaming-endpoint-with-a-cdn-wont-stop)