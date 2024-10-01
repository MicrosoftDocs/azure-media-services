---
title: Azure Policy built-in support in Media Services
description: This article discusses Azure Policy built-in support for Azure Media Services scenarios.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Azure Policy for Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Azure Media Services provides built-in [Azure Policy](/azure/governance/policy/overview) definitions to help enforce organizational standards and compliance at-scale.
Common use cases for Azure Policy include implementing governance for resource consistency,regulatory compliance, security, cost and management.

Media Services provides several common use case definitions for Azure Policy that a built-in to help you get started.

## Built-in Azure Policy definitions for Media Services

Several built in policy definitions are available for use with Media Services to help get you started, and allow you to define your own custom policies.

[!INCLUDE [Azure Policy Media Services](./includes/policies-media-services.md)]

The [list of built-in policy definitions for Media Services](/azure/governance/policy/samples/built-in-policies#media-services) provides the latest definitions and links the code definitions and how to access them in the Portal.

## Common scenarios that require Azure Policy

* If your enterprise security requires you to ensure that all Media Services accounts are created with Private Links, you can use a policy definition to ensure that accounts are only created with the 2020-05-01 API (or later) to disable access to the legacy REST v2 API and access the Private Link feature.
* If you want to enforce specific options on the tokens used for Content Key Policies, an Azure Policy definition can be constructed to support the specific requirements.
* If your security goals require you to restrict a Job input source to only come from your trusted storage accounts, and restrict access to external HTTP(S) inputs through the use of JobInputHttp, an Azure policy can be constructed to limit the input URI pattern.

## Example policy definitions

Azure Media Services maintains and publishes a set of sample Azure Policy definitions in Git hub.
See the [built-in policy definitions for Media Services](https://github.com/Azure/azure-policy/tree/master/built-in-policies/policyDefinitions/Media%20Services) samples in the azure-policy Git hub repository.

## Azure Policies, private endpoints and Media Services

Media Services defines a set of [built-in Azure Policy definitions](/azure/governance/policy/samples/built-in-policies#media-services) to help enforce organizational standards and to assess compliance at-scale.

### Azure Policy for Private Endpoints in the portal

The [Configure Azure Media Services with private endpoints](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc5632066-946d-4766-9544-cd79bcc1286e) policy can be used to automatically create private endpoints for Media Services resources. The parameters for the policy set the subnet where the private link should be created and the group ID to use when creating the private endpoint. To automatically create private endpoints for key delivery, live events, and streaming endpoints, the policy must be assigned separately for each of the group IDs (i.e., a policy assignment would be created with the group ID set to *keydelivery*, a second policy assignment would be created with the group ID set to *liveevent* and a third assignment would set the group ID to *streamingendpoint*). As this policy deploys resources, the policy must be created with a Managed Identity.

The [Configure Azure Media Services to use private DNS zones](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4a7f6c1-585e-4177-ad5b-c2c93f4bb991) policy can be used to create private DNS zones for Media Services private endpoints. This policy is also applied separately for each group ID.

The [Azure Media Services should use private link](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4a591bf5-918e-4a5f-8dad-841863140d61) policy will generate audit events for Media Services resources that do not have private link enabled.

### Azure Policy for network security

When private link is used to access Media Services resources, a common requirement is to limit access to these resources from the internet. The [Azure Media Services accounts should disable public network access](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F8bfe3603-0888-404a-87ff-5c1b6b4cc5e3) policy can be used to audit Media Services accounts that permit public network access.

### Outbound network security

Azure Policy can be used to restrict how Media Services accesses external services. The [Azure Media Services jobs with HTTPS inputs should limit input URIs to permitted URI patterns](https://ms.portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe9914afe-31cd-4b8a-92fa-c887f847d477) policy be used to either entirely block Media Services jobs that read from HTTP and HTTPS URLS or to limit Media Services jobs to reading from URLs that match specific patterns.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
