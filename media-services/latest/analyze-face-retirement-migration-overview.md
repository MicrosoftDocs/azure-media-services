---
title: Media Services Face Detector preset retirement and migration
description: This article discusses Media Services Face Detector retirement and migration.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Media Services Face Detector retirement and migration

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article discusses Media Services Face Detector retirement and migration.

## Overview

[!INCLUDE [warning-video-analyzer-retirement](includes/warning-video-analyzer-retirement.md)]

## Migration steps

There **will not be** a direct replacement for the Face Detector. If you would like to instead detect people in a video, we recommend updating your
applications to use the Video Indexer APIs for [detecting observed people](/azure/azure-video-indexer/observed-people-tracing) and [matching observed people to faces](/azure/azure-video-indexer/matched-person) and [submit a request](https://aka.ms/facerecognition) to get access to the Limited Access program for these features. See the [Limited Access policy](https://aka.ms/AAh91ff) for more details.

[!INCLUDE [media-services-community](includes/media-services-community.md)]

