---
title: Overview of using private links with Azure Media Services
description: This article gives an overview of using private links with Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 03/29/2022
ms.author: inhenkel
---

# Overview of using Azure Private Link with Azure Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article gives an overview of using private links with Azure Media Services.

## When to use Private Link with Media Services

Private Link allows Media Services to be accessed from private networks. When used with the network access controls provided by Media Services, private links can enable Media Services to be used without exposing endpoints to the public internet.

## Azure Private Endpoint and Azure Private Link

An [Azure Private Endpoint](/azure/private-link/private-endpoint-overview) is a network interface that uses a private IP address from your virtual network.  This network interface connects you privately and securely to a service via Azure Private Link.

Media Services endpoints may be accessed from a virtual network using private endpoints. Private endpoints may also be accessed from peered virtual networks or other networks connected to the virtual network using Express Route or VPN.

[Azure Private Links](/azure/private-link/) allow access to Media Services private endpoints in your virtual network without exposing them to the public Internet. It routes traffic over the Microsoft backbone network.

## Restricting access

> [!Important]
> Creating a private endpoint **DOES NOT** implicitly disable internet access to it.

Internet access to the endpoints in the Media Services account can be restricted in one of two ways:

- Restricting access to all resources within the Media Services account.
- Restricting access separately for each resource by using the IP allowlist.

## Media Services endpoints

| Endpoint                    | Description                                                               | Supports private link | Internet access control |
| --------------------------- | ------------------------------------------------------------------------- | --------------------- | ----------------------- |
| Streaming Endpoint          | The origin server for streaming video and formats media into HLS and DASH | Yes                   | IP allowlist            |
| Streaming Endpoint with CDN | Stream media to many viewers                                              | No                    | Managed by CDN          |
| Key Delivery                | Provides media content keys and DRM licenses to media viewers             | Yes                   | IP allowlist            |
| Live event                  | Ingests media content for live streaming                                  | Yes                   | IP allowlist            |

> [!NOTE]
> Media Services accounts created with API versions prior to 2020-05-01 also have an endpoint for the legacy RESTv2 API endpoint (pending deprecation).  This endpoint does not support private links.

## Private endpoints, Azure Storage and Media Services

Media Services always uses the public endpoint to access storage accounts. Creating a private endpoint for a storage account does not affect how Media Services accesses the storage account.

Customers who configure a private endpoint for a storage account often also choose to restrict public network access to their storage account (using either the *publicNetworkAccess* or *networkAcls* properties of the storage account). Media Services is still able to access storage accounts using the public endpoint when the *publicNetworkAccess* or *networkAcls* properties would normally prevent this access, if all of the following conditions are met:

- The storage account *bypass* property under *networkAcls* is set to *AzureServices*, and
- The Media Services account has a Managed Identity, and
- The Managed Identity of the Media Services account has been granted the *Storage Blob Data Contributor* and *Reader* roles for the storage account, and
- Media Services is configured to access the storage account using Managed Identity.

This may appear to be a lot of conditions, but it is also the default options the portal will configure when creating accounts.

Consider the network architecture shown here:

:::image type="content" source="media/private-endpoint-link-diagrams/private-endpoint-storage.png" alt-text="A diagram showing how private endpoints and links protect content but allow Media Services access to the storage account." lightbox="media/private-endpoint-link-diagrams/private-endpoint-storage.png":::

With a VNet with private endpoints for storage accounts and for Media Services resources, you would use the private endpoint to access the storage account from your on-premises network. As you would have a private endpoint for your storage account, you would block all internet access to the storage account. As a trusted service, Media Services is still able to access the storage account via the public interface.

## More information about private link enabled Azure services

| Service                | Media Services integration                      | Private link documentation |
| ---------------------- | ----------------------------------------------- | -------------------------- |
| Azure Storage          | Used to store media                             | [Use private endpoints for Azure Storage](/azure/storage/common/storage-private-endpoints) |
| Azure Key Vault        | Used to store [customer-managed keys](security-customer-managed-keys-portal-tutorial.md)             | [Configure Azure Key Vault networking settings](/azure/key-vault/general/how-to-azure-key-vault-network-security) |
| Azure Resource Manager | Provides access to Media Services APIs          | [Use REST API to create private link for managing Azure resources](/azure/azure-resource-manager/management/create-private-link-access-rest) |
| Event Grid             | Provides [notifications of Media Services events](./monitoring/job-state-events-cli-how-to.md) | [Configure private endpoints for Azure Event Grid topics or domains](/azure/event-grid/configure-private-endpoints)  |

## Private endpoints are created on the Media Services account

Private Endpoints for Key Delivery, Streaming Endpoints, and Live Events are created on the Media Services account instead of being created individually.

A private IP address is created for each Streaming Endpoint or Live Event in the Media Services account when a Media Services private endpoint resource is created. For example, if you have two started Streaming Endpoints, a single private endpoint should be created to connect both Streaming Endpoints to a virtual network. Resources can be connected to multiple virtual networks at the same time.

Internet access to the Media Services account should be restricted, either for all the resources within the account or separately for each resource.

## Private Link pricing
For pricing details, see [Azure Private Link Pricing](https://azure.microsoft.com/pricing/details/private-link)

## Private Link how-tos and FAQs

- [Create a Media Services and Storage account with a Private Link using an Azure Resource Management template](security-private-link-arm-how-to.md)
- [Create a Private Link for a Streaming Endpoint](security-private-link-streaming-endpoint-how-to.md)