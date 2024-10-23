---
title: Azure Private endpoints with Azure Media Services
description: This article gives an overview of using a private endpoint with Azure Media Services. Media Services endpoints include streaming endpoints that are origin servers for streaming video and formats media into HLS and DASH, key delivery that provides media content keys and DRM licenses to media viewers, live events that ingest media content for live streaming, and the Media Services storage account that stores media blobs and associated streaming files in an asset (container).
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: conceptual
ms.date: 02/24/2023
ms.author: inhenkel
---

# Azure private endpoints with Azure Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article gives an overview of using a private endpoint with Azure Media Services. Media Services endpoints include streaming endpoints that are origin servers for streaming video and formats media into HLS and DASH, key delivery that provides media content keys and DRM licenses to media viewers, live events that ingest media content for live streaming, and the Media Services storage account that stores media blobs and associated streaming files in an asset (container). You are encouraged to learn about [Azure Private Endpoint](/azure/private-link/private-endpoint-overview) before you continue reading this article.

## Azure private endpoints

An [Azure private endpoint](/azure/private-link/private-endpoint-overview) is a network interface that uses a private IP address from your virtual network.

## Practice with Azure private endpoints

If you aren't already familiar with using private endpoints, work through the following tutorials and quickstarts.

> [!TIP]
> Pay special attention to the prerequisites and don't skip them! Depending on your subscription, you may not be able to create VMs in other regions than what is suggested.

- [Connect to a web app using an Azure Private Endpoint](/azure/private-link/tutorial-private-endpoint-webapp-portal).
- [Connect to a storage account using an Azure Private Endpoint](/azure/private-link/tutorial-private-endpoint-storage-portal).
- [Create a private endpoint by using the Azure portal](/azure/private-link/create-private-endpoint-portal).

## When to use private endpoints

Use private endpoints when you want to make your resources accessible to a virtual network.

## Private endpoint enabled Azure services

The following table shows the services that are typically used with Media Services.  Review the documentation in the table below to understand how private endpoints and Private Link are used for each.

| Service                | Media Services integration                      | Private endpoint documentation |
| ---------------------- | ----------------------------------------------- | ------------------------------ |
| Azure Storage          | Used to store media                             | [Use private endpoints for Azure Storage](/azure/storage/common/storage-private-endpoints) |
| Azure Key Vault        | Used to store [customer-managed keys](security-customer-managed-keys-portal-tutorial.md) | [Configure Azure Key Vault networking settings](/azure/key-vault/general/how-to-azure-key-vault-network-security) |
| Event Grid             | Provides [notifications of Media Services events](./monitoring/job-state-events-cli-how-to.md) | [Configure private endpoints for Azure Event Grid topics or domains](/azure/event-grid/configure-private-endpoints)  |

> [!TIP]
> You can still protect your content by using [dynamic encryption and key delivery](drm-content-protection-concept.md) and [Digital Rights Management (DRM) licenses](drm-playready-license-template-concept.md) such as [Widevine](drm-widevine-license-template-concept.md), [FairPlay](drm-fairplay-license-overview.md), and [PlayReady](drm-playready-license-template-concept.md) even if you aren't using a virtual network.  DRM can be used in addition to private endpoints.

## Media Services endpoints

Media Services endpoints may be accessed from a virtual network using private endpoints. Private endpoints may also be accessed from peered virtual networks or other networks connected to the virtual network using Express Route or VPN. You can also use Private Links with Media Services endpoints.

| Endpoint                    | Description                                                               | Supports private endpoint | Internet access control |
| --------------------------- | ------------------------------------------------------------------------- | ------------------------- | ----------------------- |
| Key delivery                | Provides media content keys and DRM licenses to media viewers             | Yes                       | IP allowlist            |
| Live event                  | Ingests media content for live streaming                                  | Yes                       | IP allowlist            |
| Streaming endpoint          | The origin server for streaming video and formats media into HLS and DASH | Yes                       | IP allowlist            |
| Streaming endpoint with CDN | Stream media to many viewers                                              | No                        | Managed by CDN          |

> [!IMPORTANT]
> Media Services accounts created with API versions prior to 2020-05-01 also have an endpoint for the legacy RESTv2 API endpoint (pending deprecation).

## Private endpoints for Media Services account resources

Private endpoints for key delivery, streaming endpoints, and live events are created on the Media Services account. You generally create one private endpoint for each type of Media Services endpoint. For example, you can create one private endpoint for several streaming endpoints.

In this way, multiple instances of a resource, for example, live events within a Media Services account, can be connected to a virtual network with a singe private endpoint. To connect to multiple virtual networks, you would create multiple private endpoints.

See [Private endpoint connections overview](security-private-endpoint-connect-private-endpoint-concept.md) for a discussion of network access flags, DNS NAME changes, and IP level allowlists.

See [Azure Policy for Media Services](security-azure-policy.md#azure-policies-private-endpoints-and-media-services) to understand the application of Azure Policy for private endpoint scenarios.

## Media Services storage private endpoints

With a virtual network and private endpoints for storage accounts, you can use the private endpoint to access the storage account from your on-premises network.

Media Services always uses the public endpoint to access storage accounts. Media Services accounts can be configured to work with storage accounts that block access from the internet by meeting the requirements below:

Customers who configure a private endpoint for a storage account can restrict public network access to their storage account (using either the *publicNetworkAccess* or *networkAcls* properties of the storage account). Media Services is still able to access storage accounts using the public endpoint when the *publicNetworkAccess* or *networkAcls* properties would normally prevent this access, if all of the following conditions are met:

- The storage account *bypass* property under *networkAcls* is set to *AzureServices*, and
- The Media Services account has a Managed Identity, and
- The Managed Identity of the Media Services account has been granted the *Storage Blob Data Contributor* and *Reader* roles for the storage account, and
- Media Services is configured to access the storage account using Managed Identity.

## Media Services streaming and live event private endpoint configurations

The following examples describe the configurations that you can use for private streaming.

### No private endpoints

When private endpoints aren't used, requests from viewers to access media content and keys are routed via the internet.

:::image type="content" source="media/diagrams/private-link-network-diagram-no-private-endpoints-horizontal.svg" alt-text="A diagram that show that when there is no private endpoint, internet access is available for both the streaming endpoint and the key delivery endpoint" lightbox="media/diagrams/private-link-network-diagram-no-private-endpoints-horizontal.svg":::

### Private endpoints for streaming and key delivery

Private endpoints can be created for streaming endpoints and the key delivery service to allow these resources to be accessed directly, rather than via the internet. This can be useful when users inside a network don't have access to the Internet.

:::image type="content" source="media/diagrams/private-endpoint-streaming-key-delivery-horizontal.svg" alt-text="A diagram that shows viewers accessing content through the streaming endpoint private endpoint and through the key delivery endpoint private endpoint." lightbox="media/diagrams/private-endpoint-streaming-key-delivery-horizontal.svg":::

### Disabled internet access

If all users access Media Services resources using private endpoints, internet access to these resources can be disabled.

:::image type="content" source="media/diagrams/private-endpoint-disabled-internet-horizontal.svg" alt-text="A diagram showing internet access blocked to the streaming endpoint and the key delivery endpoint." lightbox="media/diagrams/private-endpoint-disabled-internet-horizontal.svg":::

### Private endpoints for live events

Private Endpoints can also be created for Live Events, allowing live content to be ingested to Media Services without the internet.

:::image type="content" source="media/diagrams/private-endpoint-live-events-horizontal.svg" alt-text="A diagram showing the live event with internet access blocked." lightbox="media/diagrams/private-endpoint-live-events-horizontal.svg":::

### Private endpoints for live events while streaming to the Internet

It's also possible to create a private endpoint for a live event, while using a streaming endpoint to stream to the internet. This may be useful for scenarios that require secure ingest while targeting a large audience.

:::image type="content" source="media/diagrams/private-endpoint-live-events-stream-internet-horizontal.svg" alt-text="A diagram showing the live event blocked but streaming accessed via the internet." lightbox="media/diagrams/private-endpoint-live-events-stream-internet-horizontal.svg":::

## How-tos and tutorials

- [Create a private endpoint for a streaming endpoint in the portal](security-private-endpoint-streaming-endpoint-how-to.md)

[!INCLUDE [media-services-community](includes/media-services-community.md)]
