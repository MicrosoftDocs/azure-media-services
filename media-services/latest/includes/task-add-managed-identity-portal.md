---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/31/2022
ms.author: inhenkel
title: Add a Managed Identity in the portal
---

### Add a Managed Identity to storage in the portal

#### Managed identity and storage accounts

If you are using managed identities to secure your storage accounts, the attached storage accounts must first be assigned the [Storage Blob Contributor role](/azure/role-based-access-control/built-in-roles#storage-blob-data-contributor).

#### Check managed identity role assignment

1. Navigate to the Media Services account you want to work with.
1. Select Storage accounts from the menu. The Storage accounts screen will appear. In the Storage authentication type selections, either the **Managed Identity** radio button or the **System authentication** radio button will be selected.

#### Add a role assignment

1. Select the storage account from the storage account cards on the Storage accounts page. The properties page of the storage account will appear.
1. Select **Access Control (IAM)** from the menu.
1. Select the **Role assignments** tab.
1. Select **+ Add** to add a role assignment.
1. Select **Add role assignment** from the dropdown list.
1. Enter *Storage Blob Data Contributor* in the search field.
1. Select *Storage Blob Data Contributor* from the returned list.
1. Select the **Members** tab.
1. Select the **Managed Identity** radio button from the Assign access to selections.
1. Select **+ Select members**. The Select members screen will appear.
1. Select the subscription you are working with from the **Subscription** dropdown list.
1. Select the managed identity type from the **Managed identity** dropdown list. A list of managed identities in your subscription will appear.
1. Select the managed identities that you want to add a role to.
1. Select the **Select** button.
1. If you would like to add conditions to the role assignment, select the **Conditions(optional)** tab and add conditions.
1. Select the **Review + assign** button.
