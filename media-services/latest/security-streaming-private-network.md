---
title: Streaming to a private network with Media Services
description: This article gives an overview of streaming to a private network with Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: overview
ms.date: 3/16/2022
ms.author: inhenkel
---


# Streaming to a private network with Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article gives an overview of streaming to a private network with Media
Services.

## Media Services streaming and private endpoint

A private endpoint is an endpoint that is behind a firewall. Users can connect to the private endpoint using a VPN or Express Route, and can access content on that endpoint without transferring data across the public internet.  Media Services can stream content directly to users on an Azure virtual network. It is easiest to understand private network streaming by looking at examples.

## Example configurations

The following examples describe the configurations that you can use for private streaming.

### No private endpoints

When private endpoints are not used, requests from viewers to access media content and keys are routed via the internet.

:::image type="content" source="media/private-endpoint-link-diagrams/no-private-endpoint.png" alt-text="A diagram that show that when there is no private endpoint, internet access is available for both the streaming endpoint and the key delivery endpoint":::

### Private endpoints for streaming and key delivery

Private endpoints can be created for streaming endpoints and the key delivery service to allow these resources to be accessed directly, rather than via the internet. This can be useful when users inside a network do not have access to the internet.

:::image type="content" source="media/private-endpoint-link-diagrams/private-endpoint-key-delivery-streaming.png" alt-text="A diagram that shows viewers accessing content through the streaming endpoint private endpoint and through the key delivery endpoint private endpoint.":::

### Disabled internet access

If all users access Media Services resources using private endpoints, internet access to these resources can be disabled.

:::image type="content" source="media/private-endpoint-link-diagrams/internet-access-blocked.png" alt-text="A diagram showing internet access blocked to the streaming endpoint and the key delivery endpoint.":::

### Private endpoints for live events

Private Endpoints can also be created for Live Events, allowing live content to be ingested to Media Services without the internet.

:::image type="content" source="media/private-endpoint-link-diagrams/live-event-blocked.png" alt-text="A diagram showing the live event with internet access blocked.":::

### Private endpoints for live events while streaming to the Internet

It is also possible to create a private endpoint for a live event, while using a streaming endpoint to stream to the internet. This may be useful for scenarios that require secure ingest while targeting a large audience.

:::image type="content" source="media/private-endpoint-link-diagrams/live-event-blocked-stream-internet.png" alt-text="A diagram showing the live event blocked but streaming accessed via the internet.":::

## Azure Policy and Media Services

Media Services defines a set of [built-in Azure Policy definitions](https://docs.microsoft.com/azure/governance/policy/samples/built-in-policies#media-services) to help enforce organizational standards and to assess compliance at-scale.

## Azure Policy for Private Endpoints in the portal

The [Configure Azure Media Services with private endpoints](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc5632066-946d-4766-9544-cd79bcc1286e) policy can be used to automatically create private endpoints for Media Services resources. The parameters for the policy set the subnet where the private link should be created and the group ID to use when creating the private endpoint. To automatically create private endpoints for Key Delivery, Live Events, and Streaming Endpoints, the policy must be assigned separately for each of the group IDs (i.e., a policy assignment would be created with the group ID set to *keydelivery*, a second policy assignment would be created with the group ID set to *liveevent* and a third assignment would set the group ID to *streamingendpoint*). As this policy deploys resources, the policy must be created with a Managed Identity.

The [Configure Azure Media Services to use private DNS zones](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4a7f6c1-585e-4177-ad5b-c2c93f4bb991) policy can be used to create private DNS zones for Media Services private endpoints. This policy is also applied separately for each group ID.

The [Azure Media Services should use private link](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4a591bf5-918e-4a5f-8dad-841863140d61) policy will generate audit events for Media Services resources that do not have private link enabled.

## Azure Policy for network security

When private link is used to access Media Services resources, a common requirement is to limit access to these resources from the internet. The [Azure Media Services accounts should disable public network access](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F8bfe3603-0888-404a-87ff-5c1b6b4cc5e3)” policy can be used to audit Media Services accounts that permit public network access.

## Outbound network security

Azure Policy can be used to restrict how Media Services accesses external services. The [Azure Media Services jobs with HTTPS inputs should limit input URIs to permitted URI patterns](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe9914afe-31cd-4b8a-92fa-c887f847d477) policy be used to either entirely block Media Services jobs that read from HTTP and HTTPS URLS or to limit Media Services jobs to reading from URLs that match specific patterns.
