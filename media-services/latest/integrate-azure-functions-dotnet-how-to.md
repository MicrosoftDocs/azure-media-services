---
title: Develop Azure Functions with Media Services v3
description: This article shows how to start developing Azure Functions with Media Services v3 using Visual Studio Code.
author: xpouyat
ms.service: media-services
ms.topic: tutorial
ms.date: 08/18/2022
ms.author: inhenkel
ms.custom: contperf-fy22q4
---

# Develop Azure Functions with Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows you how to get started with creating Azure Functions that use Media Services. The Azure Function in the associated sample for this  article encodes a video file with Media Encoder Standard. As soon as the encoding job has been created, the function returns the job name and output asset name. To review Azure Functions, see [Overview](/azure/azure-functions/functions-overview) and other topics in the **Azure Functions** section.

If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-v3-dotnet-core-functions-integration). This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and live streaming operations.

## Prerequisites

- Before you can create your first function, you need to have an active Azure account. If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).
- If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](account-create-how-to.md).
- Install [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).

This article explains how to create a C# .NET 5 function that communicates with Azure Media Services. To create a function with another language, look to this [article](/azure/azure-functions/functions-develop-vs-code).

## Azure Functions in Visual Studio Code

Follow the steps for setting up and using the [Azure Functions extension](/azure/azure-functions/functions-develop-vs) in Visual Studio Code, using the *Isolated process* steps.

When you have a project set up, come back to this page.

## Generated project files

The project template creates a project in your chosen language and installs required dependencies. The new project has these files:

* **host.json**: Lets you configure the Functions host. These settings apply when you're running functions locally and when you're running them in Azure. For more information, see [host.json reference](/azure/azure-functions/functions-host-json).

* **local.settings.json**: Maintains settings used when you're running functions locally. These settings are used only when you're running functions locally.

    >[!IMPORTANT]
    >Because the local.settings.json file can contain secrets, you need to exclude it from your project source control.

* **HttpTriggerEncode.cs** class file that implements the function.

### HttpTriggerEncode.cs

This is the C# code for your function. Its role is to take a Media Services asset or a source URL and launches an encoding job with Media Services. It uses a Transform that is created if it does not exist. When it is created, it used the preset provided in the input body.

>[!IMPORTANT]
>Replace the full content of HttpTriggerEncode.cs file with [`HttpTriggerEncode.cs` from this repository](https://github.com/Azure-Samples/media-services-v3-dotnet-core-functions-integration/blob/main/Tutorial/HttpTriggerEncode.cs).

Once you are done defining your function, select **Save and Run**.

The source code for the **Run** method of the function is:

[!code-csharp[Main](~/../media-services-v3-dotnet-core-functions-integration/Tutorial/HttpTriggerEncode.cs#Run)]

### local.settings.json

Update the file with the following content (and replace the values).

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated",
    "AadClientId": "00000000-0000-0000-0000-000000000000",
    "AadEndpoint": "https://login.microsoftonline.com",
    "AadSecret": "00000000-0000-0000-0000-000000000000",
    "AadTenantId": "00000000-0000-0000-0000-000000000000",
    "AccountName": "amsaccount",
    "ArmAadAudience": "https://management.core.windows.net/",
    "ArmEndpoint": "https://management.azure.com/",
    "ResourceGroup": "amsResourceGroup",
    "SubscriptionId": "00000000-0000-0000-0000-000000000000"
  }
}
```

## Test your function

When you run the function locally in VS Code, the function should be exposed as:

```url
http://localhost:7071/api/HttpTriggerEncode
```

To test it, you can use the REST client of your choice to do a POST on this URL using a JSON input body.

JSON input body example:

```json
{
    "inputUrl":"https://nimbuscdn-nimbuspm.streaming.mediaservices.windows.net/2b533311-b215-4409-80af-529c3e853622/Ignite-short.mp4",
    "transformName" : "TransformAS",
    "builtInPreset" :"AdaptiveStreaming"
 }
```

The function should return 200 OK with an output body containing the job and output asset names.
