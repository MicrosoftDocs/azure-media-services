---
title: Media Services Face Redactor preset retirement and migration
description: This article discusses the retirement and migration for Media Services Face Redactor retirement and migration.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 08/24/2022
ms.author: inhenkel
---

# Media Services Face Redactor retirement and migration

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

This article discusses the retirement and migration for Media Services Face Detector retirement and migration.

## Overview

As Microsoft’s [Responsible AI Standards](https://blogs.microsoft.com/on-the-issues/2022/06/21/microsofts-framework-for-building-ai-systems-responsibly/) outlines, Microsoft is committed to fairness, privacy, security, and
transparency with respect to AI systems. To align with these standards, Azure Media Services is retiring the Face Redactor Restv2 preset on September 14, 2023. This preset offers face detection and redaction (blurring) of selected individuals in video files. After September 14, 2023, any applications you have developed using the Azure Media Redactor (RESTv2) will begin experiencing errors or failed job submissions.

> [!NOTE]
> There is no replacement planned for the China region.

## Migration steps

There **will not be** a direct replacement for the Face Redactor. If you would like to instead detect people in a video, we recommend you update your
applications to use the Video Indexer APIs for [detecting observed people](/azure/azure-video-indexer/observed-people-tracing) and [matching observed people to faces](/azure/azure-video-indexer/matched-person) and [submit a request](https://aka.ms/facerecognition) to get access to the
Limited Access program for these features. See the [Limited Access policy](https://aka.ms/AAh91ff) for more details.

## Microsoft Q&A

If you have further questions, please go to [Microsoft Q&A](https://aka.ms/azureqa) the community support channel to get answers to technical questions.
