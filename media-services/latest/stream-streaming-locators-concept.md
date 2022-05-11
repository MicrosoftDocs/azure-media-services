---
title: Streaming Locators in Azure Media Services
description: This article gives an explanation of what Streaming Locators are, and how they are used by Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 3/16/2022
ms.author: inhenkel
---

# Streaming Locators

To make videos in the output Asset available to clients for playback, you have to create a [Streaming Locator](/rest/api/media/streaminglocators) and then build streaming URLs. To build a URL, you need to concatenate the Streaming Endpoint host name and the Streaming Locator path. For .NET sample, see [Get a Streaming Locator](stream-files-tutorial-with-api.md#get-a-streaming-locator).

The process of creating a **Streaming Locator** is called publishing. By default, the **Streaming Locator** is valid immediately after you make the API calls, and lasts until it is deleted, unless you configure the optional start and end times.

When creating a **Streaming Locator**, you must specify an **Asset** name and a **Streaming Policy** name. For more information, see the following topics:

* [Assets](assets-concept.md)
* [Streaming Policies](stream-streaming-policy-concept.md)
* [Content Key Policies](drm-content-key-policy-concept.md)

You can also specify the start and end time on your Streaming Locator, which will only let your user play the content between these times (for example, between 5/1/2019 to 5/5/2019).

## Considerations

- **Streaming Locators** are not updatable.
- Properties of **Streaming Locators** that are of the Datetime type are always in UTC format.
- You should design a limited set of policies for your Media Service account and reuse them for your Streaming Locators whenever the same options are needed. For more information, see [Quotas and limits](limits-quotas-constraints-reference.md).

## Streaming locator How-Tos and Tutorials

- [Create a streaming locator](/streaming-locator-create-how-to?amspage=stream-streaming-locators-concept)
- [Show the details of a streaming locator](streaming-locator-show-how-to.md?amspage=stream-streaming-locators-concept)
- [List streaming locators](streaming-locator-list-how-to.md?amspage=stream-streaming-locators-concept)
- [List streaming locator paths](streaming-locator-list-paths-how-to.mdb?amspage=stream-streaming-locators-concept)
- [List streaming locator content keys](streaming-locator-list-content-keys-how-to.md?amspage=stream-streaming-locators-concept)
- [Delete a streaming locator](streaming-locator-delete-how-to.md?amspage=stream-streaming-locators-concept)