---
title: Media Services Face Detector preset retirment and migration
description: As Microsoft’s Responsible AI Standards outlines, Microsoft is committed to fairness, privacy, security, and
transparency with respect to AI systems. To align with these standards, Azure Media Services is retiring the Face Detector preset on September 14, 2023.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 08/24/2022
ms.author: inhenkel
---

# Media Services Face Detector retirement and migration

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Executive summary

As Microsoft’s [Responsible AI Standards](https://blogs.microsoft.com/on-the-issues/2022/06/21/microsofts-framework-for-building-ai-systems-responsibly/) outline, Microsoft is committed to fairness, privacy, security, and transparency
with respect to AI systems. To better align with these standards, Azure Media Services is retiring the [Face Detector preset](analyze-face-redaction-concept.md) on September 14, 2023. This preset offers face detection and redaction (blurring) of selected individuals in video files. After September 14, 2023, any applications developed using the Azure Media Services v3 API with Face Detector preset will begin experiencing errors or failed job submissions.

## Migration steps

There **will not be** a direct replacement for the Face Detector. If you would like to instead detect people in a video, we recommend updating your
applications to use the Video Indexer APIs for [detecting observed people](/azure/azure-video-indexer/observed-people-tracing) and [matching observed people to faces](/azure/azure-video-indexer/matched-person) and [submit a request](https://aka.ms/facerecognition) to get access to the Limited Access program for these features. See the [Limited Access policy](https://aka.ms/AAh91ff) for more details.

## Microsoft Q&A

If you have further questions, please go to [Microsoft Q&A](https://aka.ms/azureqa) the community support channel to get answers to technical questions.
