---
title: Media Services V2 vs v3 API access
description: This article describes the API access differences between Azure Media Services v2 to v3.
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 06/29/2023
ms.author: inhenkel
---

# API access differences between Azure Media Services V2 to v3 API

![migration guide logo](./media/migration-guide/azure-media-services-logo-migration-guide.svg)

<hr color="#5ea0ef" size="10">

![migration steps 2](./media/migration-guide/steps-2.svg)

[!INCLUDE [migration-no-longer-necessary](includes/migration-no-longer-necessary.md)]

This article describes the API access differences between Azure Media Services V2 to V3.

## API Access

All Media Services accounts will have access to the V3 API. However, we strongly
recommend migration development on a fresh account before applying updated code
to an existing V2 account. This is because V3 entities aren't backwards
compatible with V2. Some V2 entities like Assets are forward compatible with V3.
You can continue to use existing accounts if you don’t mix the V2 and V3 APIs
and then try to go back to V2, but this is discouraged.

Access to the V2 API will be available until it is retired in 2024.

## Create a V3 account

While you are migrating, you can create a V3 account that still has access to V2.  Creating the account can be done with:

- The REST API and older version
- Selecting the checkbox in the portal.

All the .NET, CLI, and other SDKs will be targeting the latest 2020-05-01 API, so find or configure the older API versions.

> [!NOTE]
> New accounts created with the 2020-05-01 (or later) API cannot use V2 APIs.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
