---
title: Media Services account ARM template
description: This article shows you how to use an ARM template to create a media services account.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: quickstart
ms.date: 01/09/2023
ms.author: inhenkel
---

# Quickstart: Media Services account ARM template

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows you how to use an Azure Resource Manager template (ARM template) to create a media services account.

Readers who are experienced with ARM templates can continue to the [deployment section](#deploy-the-template).

<!--If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template will open in the Azure portal.-->

<!--
[![Deploy to Azure](../../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.media%2Fmedia-services-create%2Fazuredeploy.json)
-->

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

If you have never deployed an ARM template before, it is helpful to read about [Azure ARM templates](/azure/azure-resource-manager/templates/) and go through the [tutorial](/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/media-services-create/).

<!--
The syntax for the JSON code fence is:

:::code language="json" source="~/../quickstart-templates/quickstarts/microsoft.media/media-services-create/azuredeploy.json":::
-->

Three Azure resource types are defined in the template:

- [Microsoft.Storage/storageAccounts](/azure/templates/microsoft.storage/storageaccounts): create a storage account
- [Microsoft.Media/mediaservices](/azure/templates/microsoft.media/mediaservices): create a Media Services account

## Set the account

```cloudshell-bash

az account set --subscription {your subscription name or id}

```

## Create a resource group

```cloudshell-bash

az group create --name {the name you want to give your resource group} --location "{pick a location}"

```

## Assign a variable to your deployment file

For convenience, create a variable that stores the path to the template file. This variable makes it easier for you to run the deployment commands because you don't have to retype the path every time you deploy.

```cloudshell-bash

templateFile="{provide the path to the template file}"

```

## Deploy the template

You will be prompted to enter the media services account name.

```cloudshell-bash

az deployment group create --name {the name you want to give to your deployment} --resource-group {the name of resource group you created} --template-file $templateFile

```

## Review deployed resources

You should see a JSON response similar to the below:

```json
{
  "id": "/subscriptions/{subscriptionid}/resourceGroups/amsarmquickstartrg/providers/Microsoft.Resources/deployments/amsarmquickstartdeploy",
  "location": null,
  "name": "amsarmquickstartdeploy",
  "properties": {
    "correlationId": "{correlationid}",
    "debugSetting": null,
    "dependencies": [
      {
        "dependsOn": [
          {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/amsarmquickstartrg/providers/Microsoft.Storage/storageAccounts/storagey44cfdmliwatk",
            "resourceGroup": "amsarmquickstartrg",
            "resourceName": "storagey44cfdmliwatk",
            "resourceType": "Microsoft.Storage/storageAccounts"
          }
        ],
        "id": "/subscriptions/35c2594a-23da-4fce-b59c-f6fb9513eeeb/resourceGroups/amsarmquickstartrg/providers/Microsoft.Media/mediaServices/{accountname}",
        "resourceGroup": "amsarmquickstartrg",
        "resourceName": "{accountname}",
        "resourceType": "Microsoft.Media/mediaServices"
      }
    ],
    "duration": "PT1M10.8615001S",
    "error": null,
    "mode": "Incremental",
    "onErrorDeployment": null,
    "outputResources": [
      {
        "id": "/subscriptions/{subscriptionid}/resourceGroups/amsarmquickstartrg/providers/Microsoft.Media/mediaServices/{accountname}",
        "resourceGroup": "amsarmquickstartrg"
      },
      {
        "id": "/subscriptions/{subscriptionid}/resourceGroups/amsarmquickstartrg/providers/Microsoft.Storage/storageAccounts/storagey44cfdmliwatk",
        "resourceGroup": "amsarmquickstartrg"
      }
    ],
    "outputs": null,
    "parameters": {
      "mediaServiceName": {
        "type": "String",
        "value": "{accountname}"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.Media",
        "registrationPolicy": null,
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "capabilities": null,
            "locations": [
              "eastus"
            ],
            "properties": null,
            "resourceType": "mediaServices"
          }
        ]
      },
      {
        "id": null,
        "namespace": "Microsoft.Storage",
        "registrationPolicy": null,
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "capabilities": null,
            "locations": [
              "eastus"
            ],
            "properties": null,
            "resourceType": "storageAccounts"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "templateHash": "{templatehash}",
    "templateLink": null,
    "timestamp": "2020-11-24T23:25:52.598184+00:00",
    "validatedResources": null
  },
  "resourceGroup": "amsarmquickstartrg",
  "tags": null,
  "type": "Microsoft.Resources/deployments"
}

```

In the Azure portal, confirm that your resources have been created.

## Clean up resources

If you aren't planning to use the resources you just created, you can delete the resource group.

```cloudshell-bash

az group delete --name {name of the resource group}

```

[!INCLUDE [media-services-community](includes/media-services-community.md)]
