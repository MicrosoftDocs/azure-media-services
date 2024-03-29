---
title: Develop with Azure Media Services v3 APIs
description: Learn about rules that apply to entities and APIs when developing with Media Services v3.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---

# Develop with Media Services v3 APIs

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

As a developer, you can use client libraries for (.NET, Python, Node.js, Java, and Go) that allow you to interact with the REST API to easily create, manage, and maintain custom media workflows. The [Media Services v3](https://aka.ms/ams-v3-rest-sdk) API is based on the OpenAPI specification (formerly known as a Swagger).

This article discusses rules that apply to entities and APIs when you develop with Media Services v3.

[!INCLUDE [warning-rest-api-retry-policy.md](./includes/warning-rest-api-retry-policy.md)]

## Accessing the Azure Media Services API

To be authorized to access Media Services resources and the Media Services API, you must first be authenticated. Media Services supports [Azure Active Directory (Azure AD)-based](/azure/active-directory/fundamentals/active-directory-whatis) authentication. Two common authentication options are:

* **Service principal authentication**: Used to authenticate a service (for example: web apps, function apps, logic apps, API, and microservices). Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs. For example, for web apps there should always be a mid-tier that connects to Media Services with a Service Principal.
* **User authentication**: Used to authenticate a person who is using the app to interact with Media Services resources. The interactive app should first prompt the user for the user's credentials. An example is a management console app used by authorized users to monitor encoding jobs or live streaming.

The Media Services API requires that the user or app making the REST API requests have access to the Media Services account resource and use a **Contributor** or **Owner** role. The API can be accessed with the **Reader** role but only **Get** or **List**  operations will be available. For more information, see [Azure role-based access control (Azure RBAC) for Media Services accounts](security-rbac-concept.md).

Instead of creating a service principal, consider using managed identities for Azure resources to access the Media Services API through Azure Resource Manager. To learn more about managed identities for Azure resources, see [What is managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/overview).

### Azure AD service principal

The Azure AD app and service principal should be in the same tenant. After you create the app, give the app **Contributor** or **Owner** role access to the Media Services account.

If you're not sure whether you have permissions to create an Azure AD app, see [Required permissions](/azure/active-directory/develop/howto-create-service-principal-portal#permissions-required-for-registering-an-app).

In the following figure, the numbers represent the flow of the requests in chronological order:

![Middle-tier app authentication with AAD from a web API](./media/use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

1. A middle-tier app requests an Azure AD access token that has the following parameters:

   * Azure AD tenant endpoint.
   * Media Services resource URI.
   * Resource URI for REST Media Services.
   * Azure AD app values: the client ID and client secret.

   To get all the needed values,
see [Access Azure Media Services API](./access-api-howto.md).

2. The Azure AD access token is sent to the middle tier.
4. The middle tier sends request to the Azure Media REST API with the Azure AD token.
5. The middle tier gets back the data from Media Services.

### Samples

See the following samples that show how to connect with Azure AD service principal:
* [Connect with .NET](configure-connect-dotnet-howto.md)
* [Connect with Node.js](configure-connect-nodejs-howto.md)
* [Connect with Python](configure-connect-python-howto.md)
* [Connect with Java](configure-connect-java-howto.md)

## Naming conventions

Azure Media Services v3 resource names (for example, Assets, Jobs, Transforms) are subject to Azure Resource Manager naming constraints. In accordance with Azure Resource Manager, the resource names are always unique. Thus, you can use any unique identifier strings (for example, GUIDs) for your resource names.

Media Services resource names can't include: '<', '>', '%', '&', ':', '&#92;', '?', '/', '*', '+', '.', the single quote character, or any control characters. All other characters are allowed. The max length of a resource name is 260 characters.

For more information about Azure Resource Manager naming, see [Naming requirements](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/resource-api-reference.md#arguments-for-crud-on-resource) and [Naming conventions](/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging).

### Names of files/blobs within an asset

The names of files/blobs within an asset must follow both the [blob name requirements](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata) and the [NTFS name requirements](/windows/win32/fileio/naming-a-file). The reason for these requirements is the files can get copied from blob storage to a local NTFS disk for processing.

## Long-running operations

The operations marked with `x-ms-long-running-operation` in the Azure Media Services [swagger files](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/mediaservices/resource-manager/Microsoft.Media/stable/2018-07-01/streamingservice.json) are long running operations.

For details about how to track asynchronous Azure operations, see [Async operations](/azure/azure-resource-manager/management/async-operations).

Media Services has the following long-running operations:

* [Create Live Events](/rest/api/media/liveevents/create)
* [Update Live Events](/rest/api/media/liveevents/update)
* [Delete Live Event](/rest/api/media/liveevents/delete)
* [Start Live Event](/rest/api/media/liveevents/start)
* [Stop LiveEvent](/rest/api/media/liveevents/stop)

  Use the `removeOutputsOnStop` parameter to delete all associated Live Outputs when stopping the event.
* [Reset LiveEvent](/rest/api/media/liveevents/reset)
* [Create LiveOutput](/rest/api/media/liveevents/create)
* [Delete LiveOutput](/rest/api/media/liveevents/delete)
* [Create StreamingEndpoint](/rest/api/media/streamingendpoints/create)
* [Update StreamingEndpoint](/rest/api/media/streamingendpoints/update)
* [Delete StreamingEndpoint](/rest/api/media/streamingendpoints/delete)
* [Start StreamingEndpoint](/rest/api/media/streamingendpoints/start)
* [Stop StreamingEndpoint](/rest/api/media/streamingendpoints/stop)
* [Scale StreamingEndpoint](/rest/api/media/streamingendpoints/scale)

On successful submission of a long operation, you receive a '201 Created' and must poll for operation completion using the returned operation ID.

The [track asynchronous Azure operations](/azure/azure-resource-manager/management/async-operations) article explains in depth how to track the status of asynchronous Azure operations through values returned in the response.

Only one long-running operation is supported for a given Live Event or any of its associated Live Outputs. Once started, a long running operation must complete before starting a subsequent long-running operation on the same LiveEvent or any associated Live Outputs. For Live Events with multiple Live Outputs, you must await the completion of a long running operation on one Live Output before triggering a long running operation on another Live Output.

## SDKs

> [!NOTE]
> The Azure Media Services v3 SDKs aren't guaranteed to be thread-safe. When developing a multi-threaded app, you should add your own thread synchronization logic to protect the client or use a new AzureMediaServicesClient object per thread. You should also be careful of multi-threading issues introduced by optional objects provided by your code to the client (like an HttpClient instance in .NET).

|SDK|Reference|
|---|---|
|[.NET SDK](https://aka.ms/ams-v3-dotnet-sdk)|[.NET ref](/dotnet/api/overview/azure/media-services?view=azure-dotnet&preserve-view=true)|
|[Java SDK](https://aka.ms/ams-v3-java-sdk)|[Java ref](/java/api/overview/azure/mediaservices/management?view=azure-java-legacy&preserve-view=true)|
|[Python SDK](https://aka.ms/ams-v3-python-sdk)|[Python ref](/python/api/azure-mgmt-media/azure.mgmt.media?view=azure-python&preserve-view=true)|
|[Node.js SDK](https://aka.ms/ams-v3-nodejs-sdk) |[Node.js ref](/javascript/api/overview/azure/arm-mediaservices-readme?view=azure-node-latest&preserve-view=true)|
|[Go SDK](https://aka.ms/ams-v3-go-sdk) |[Go ref](https://aka.ms/ams-v3-go-ref)|

### See also

- [EventGrid .NET SDK that includes Media Service events](https://www.nuget.org/packages/Microsoft.Azure.EventGrid/)
- [Definitions of Media Services events](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/eventgrid/data-plane/Microsoft.Media/stable/2018-01-01/MediaServices.json)

## Azure Media Services Explorer

[Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE) is a tool available to Windows customers who want to learn about Media Services. AMSE is a Winforms/C# application that does upload, download, encode, stream VOD and live content with Media Services. The AMSE tool is for clients who want to test Media Services without writing any code. The AMSE code is provided as a resource for customers who want to develop with Media Services.

AMSE is an Open Source project, support is provided by the community (issues can be reported to https://github.com/Azure/Azure-Media-Services-Explorer/issues). This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information, see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact opencode@microsoft.com with any other questions or comments.

## Filtering, ordering, paging of Media Services entities

See [Filtering, ordering, paging of Azure Media Services entities](filter-order-page-entities-how-to.md).

[!INCLUDE [media-services-community](includes/media-services-community.md)]
