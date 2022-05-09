---
title: Media Services account Bicep
description: This article shows you how to use Bicep to create a media services account.
author: schaffererin
ms.service: media-services
ms.topic: quickstart
ms.date: 05/09/2022
ms.author: v-eschaffer
---

# Quickstart: Media Services account Bicep

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows you how to use Bicep to create a media services account.

## Introduction

[Bicep](/azure/azure-resource-manager/bicep/overview) is a domain-specific language (DSL) that uses declarative syntax to deploy Azure resources. It provides concise syntax, reliable type safety, and support for code reuse. Bicep offers the best authoring experience for your infrastructure-as-code solutions in Azure.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

If you have never deployed a Bicep file before, it is helpful to read about [Bicep files](/azure/azure-resource-manager/bicep/file) and go through the [quickstart](/azure/azure-resource-manager/bicep/quickstart-create-bicep-use-visual-studio-code?tabs=CLI).

## Review the Bicep file

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/media-services-create/).

:::code language="bicep" source="~/../quickstart-templates/quickstarts/microsoft.media/media-services-create/main.bicep":::

The following Azure resources are defined in the Bicep file:

- [Microsoft.Storage/storageAccounts](/azure/templates/microsoft.storage/storageaccounts): create a storage account.
- [Microsoft.Media/mediaservices](/azure/templates/microsoft.media/mediaservices): create a Media Services account.

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.
1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

    # [CLI](#tab/CLI)

    ```azurecli
    az group create --name exampleRG --location eastus
    az deployment group create --resource-group exampleRG --template-file main.bicep
    ```

    # [PowerShell](#tab/PowerShell)

    ```azurepowershell
    New-AzResourceGroup -Name exampleRG -Location eastus
    New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep
    ```

    ---

    When the deployment finishes, you should see a message indicating the deployment succeeded.

## Review deployed resources

Use the Azure portal, Azure CLI, or Azure PowerShell to list the deployed resources in the resource group.

# [CLI](#tab/CLI)

```azurecli-interactive
az resource list --resource-group exampleRG
```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive
Get-AzResource -ResourceGroupName exampleRG
```

---

## Clean up resources

When it's no longer needed, delete the resource group, which also deletes the resources in the resource group.

# [CLI](#tab/CLI)

```azurecli-interactive
az group delete --name exampleRG
```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive
Remove-AzResourceGroup -Name exampleRG
```

---
