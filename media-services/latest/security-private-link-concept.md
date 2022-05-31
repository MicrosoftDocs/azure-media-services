---
title: Azure Private endpoints and Private Link with Azure Media Services
description: This article gives an overview of creating a private endpoint and using Private Links with Azure Media Services. Media Services endpoints include streaming endpoints that are origin servers for streaming video and formats media into HLS and DASH, key delivery that provides media content keys and DRM licenses to media viewers, live events that ingest media content for live streaming, and the Media Services storage account that stores media blobs and associated streaming files in an asset (container).
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 05/25/2022
ms.author: inhenkel
---

# Azure private endpoints and Private Link with Azure Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article gives an overview of creating a private endpoint and using Private Links with Azure Media Services. We encourage you to learn about [Azure Private Endpoint](/azure/private-link/private-endpoint-overview) before reading this article.

## Azure private endpoints and Azure Private Link

An [Azure private endpoint](/azure/private-link/private-endpoint-overview) is a network interface that uses a private IP address from your virtual network.  This network interface connects you privately and securely to a service via Azure Private Link.

Media Services endpoints may be accessed from a virtual network using private endpoints. Private endpoints may also be accessed from peered virtual networks or other networks connected to the virtual network using Express Route or VPN.

[Azure Private Links](/azure/private-link/) allow access to Media Services private endpoints in your virtual network without exposing them to the public Internet. It routes traffic over the Microsoft backbone network.

> [!NOTE]
> Media Services accounts created with API versions prior to 2020-05-01 also have an endpoint for the legacy RESTv2 API endpoint (pending deprecation). It doesn't support private links.

## Practice with Azure private endpoints and Private Link Service

Try the [Create a private endpoint in the portal quickstart](/azure/private-link/create-private-endpoint-portal) and the [Create a Private Link in the portal quickstart](/azure/private-link/create-private-link-service-portal) to get some hands-on experience before attempting to use them with Media Services.

## When to use private endpoints

Use private endpoints and Private Link when you want to secure a virtual network with resources behind a firewall.

## Content protection without a firewall

You can still protect your content by using [dynamic encryption and key delivery](drm-content-protection-concept.md) and [digital rights management licenses]() such as [Widevine](drm-widevine-license-template-concept.md), [FairPlay](drm-fairplay-license-overview.md), and [PlayReady](drm-playready-license-template-concept.md) even if you aren't using a virtual network and a firewall.  DRM can also be used in addition to private endpoints.

## Private Link enabled Azure services

The following table shows the services that are typically used with Media Services.  Review the documentation in the table below to understand how private endpoints and Private Link are used for each.

| Service                | Media Services integration                      | Private link documentation |
| ---------------------- | ----------------------------------------------- | -------------------------- |
| Azure Storage          | Used to store media                             | [Use private endpoints for Azure Storage](/azure/storage/common/storage-private-endpoints) |
| Azure Key Vault        | Used to store [customer-managed keys](security-customer-managed-keys-portal-tutorial.md)             | [Configure Azure Key Vault networking settings](/azure/key-vault/general/how-to-azure-key-vault-network-security) |
| Azure Resource Manager | Provides access to Media Services APIs          | [Use REST API to create private link for managing Azure resources](/azure/azure-resource-manager/management/create-private-link-access-rest) |
| Event Grid             | Provides [notifications of Media Services events](./monitoring/job-state-events-cli-how-to.md) | [Configure private endpoints for Azure Event Grid topics or domains](/azure/event-grid/configure-private-endpoints)  |

## Media Services endpoints

| Endpoint                    | Description                                                               | Supports private link | Internet access control |
| --------------------------- | ------------------------------------------------------------------------- | --------------------- | ----------------------- |
| Key delivery                | Provides media content keys and DRM licenses to media viewers             | Yes                   | IP allowlist            |
| Live event                  | Ingests media content for live streaming                                  | Yes                   | IP allowlist            |
| Storage account             | Stores media blobs and associated streaming files in an asset (container) | Yes                   | ACLs, Managed Identity  |
| Streaming endpoint          | The origin server for streaming video and formats media into HLS and DASH | Yes                   | IP allowlist            |
| Streaming endpoint with CDN | Stream media to many viewers                                              | No                    | Managed by CDN          |

## Private endpoints for Media Services account resources

Private endpoints for key delivery, streaming endpoints, and live events are created on the Media Services account instead of being created individually.

Resources can be connected to multiple virtual networks at the same time. A private IP address is created for each streaming endpoint or live event in the Media Services account when a Media Services private endpoint resource is created. For example, if you've started two streaming endpoints, a single private endpoint should be created to connect both streaming endpoints to the virtual network.

See [Private endpoint connections overview](security-private-link-connect-private-endpoint-concept.md) for a discussion of network access flags, DNS NAME changes, and IP level allowlists.

See [Azure Policy for Media Services](security-azure-policy.md#azure-policies-private-endpoints-and-media-services) to understand the application of Azure Policy for private endpoint scenarios.

## Azure Storage private endpoints and Media Services

With a virtual network and private endpoints for storage accounts, use the private endpoint and Private Link service to access the storage account from your on-premises network. This will block all internet access to the storage account. As a trusted service, Media Services is still able to access the storage account via the public interface.

> [!NOTE]
> Media Services always uses the public endpoint to access storage accounts. Creating a private endpoint for a storage account does not affect how Media Services accesses the storage account.

Customers who configure a private endpoint for a storage account often also choose to restrict public network access to their storage account (using either the *publicNetworkAccess* or *networkAcls* properties of the storage account). Media Services is still able to access storage accounts using the public endpoint when the *publicNetworkAccess* or *networkAcls* properties would normally prevent this access, if all of the following conditions are met:

- The storage account *bypass* property under *networkAcls* is set to *AzureServices*, and
- The Media Services account has a Managed Identity, and
- The Managed Identity of the Media Services account has been granted the *Storage Blob Data Contributor* and *Reader* roles for the storage account, and
- Media Services is configured to access the storage account using Managed Identity.

## Streaming and private endpoint configurations

The following examples describe the configurations that you can use for private streaming.

### No private endpoints

When private endpoints aren't used, requests from viewers to access media content and keys are routed via the internet.

:::image type="content" source="media/diagrams/private-link-network-diagram-no-private-endpoints.svg" alt-text="A diagram that show that when there is no private endpoint, internet access is available for both the streaming endpoint and the key delivery endpoint" lightbox="media/diagrams/private-link-network-diagram-no-private-endpoints.svg":::

### Private endpoints for streaming and key delivery

Private endpoints can be created for streaming endpoints and the key delivery service to allow these resources to be accessed directly, rather than via the internet. This can be useful when users inside a network don't have access to the internet.

:::image type="content" source="media/diagrams/private-link-network-diagram-private-endpoints-streaming-key-delivery.svg" alt-text="A diagram that shows viewers accessing content through the streaming endpoint private endpoint and through the key delivery endpoint private endpoint." lightbox="media/diagrams/private-link-network-diagram-private-endpoints-streaming-key-delivery.svg":::

### Disabled internet access

If all users access Media Services resources using private endpoints, internet access to these resources can be disabled.

:::image type="content" source="media/diagrams/private-link-network-diagram-disabled-internet-access.svg" alt-text="A diagram showing internet access blocked to the streaming endpoint and the key delivery endpoint." lightbox="media/diagrams/private-link-network-diagram-disabled-internet-access.svg":::

### Private endpoints for live events

Private Endpoints can also be created for Live Events, allowing live content to be ingested to Media Services without the internet.

:::image type="content" source="media/diagrams/private-endpoint-live-events-private-link-horizontal.svg" alt-text="A diagram showing the live event with internet access blocked." lightbox="media/diagrams/private-endpoint-live-events-private-link-horizontal.svg":::

### Private endpoints for live events while streaming to the Internet

It's also possible to create a private endpoint for a live event, while using a streaming endpoint to stream to the internet. This may be useful for scenarios that require secure ingest while targeting a large audience.

:::image type="content" source="media/diagrams/private-link-network-diagram-live-events-stream-internet-private-link-horizontal.svg" alt-text="A diagram showing the live event blocked but streaming accessed via the internet." lightbox="media/diagrams/private-link-network-diagram-live-events-stream-internet-private-link-horizontal.svg":::

## Private Link pricing

For pricing details, see [Azure Private Link Pricing](https://azure.microsoft.com/pricing/details/private-link)

## How-tos and tutorials

- [Create a Private Link for a streaming endpoint in the portal](security-private-link-streaming-endpoint-how-to.md)
- [Create a Media Services account and storage with Private Link using an ARM template](security-private-link-arm-how-to.md)