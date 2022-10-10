---
title: Use PowerShell to create an Azure AD app to access the Azure Media Services API
description: Learn how to use PowerShell to create an Azure Active Directory (Azure AD) app and set it up to access the Azure Media Services API.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: article
ms.date: 10/05/2022
---

# Use PowerShell to create an Azure AD app to use with the Azure Media Services API

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]



Learn how to use a PowerShell script to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.

## Prerequisites

- An Azure account. If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
- A Media Services account. For more information, see [Create an Azure Media Services account in the Azure portal](media-services-portal-create-account.md).

- Azure PowerShell. For more information, see [How to use Azure PowerShell](/powershell/azure/).

[!INCLUDE [updated-for-az](../latest/includes/updated-for-az.md)]

## Create an Azure AD app by using PowerShell

```powershell
Connect-AzAccount
Import-Module Az.Resources
Set-AzContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzADServicePrincipal -ObjectId $ServicePrincipal.Id
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

For more information, see the following articles:

- [Use Azure PowerShell to create a service principal to access resources](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
- [Add or remove Azure role assignments using Azure PowerShell](/azure/role-based-access-control/role-assignments-powershell)
- [How to manually configure daemon apps by using certificates](https://github.com/azure-samples/active-directory-dotnetcore-daemon-v2)
