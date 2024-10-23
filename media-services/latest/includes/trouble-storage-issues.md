---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 05/11/2022
ms.author: inhenkel
title: Storage account connection issues
---

<!-- Moved from storage account concept page -->

## Storage account connection issues

### Disconnected state

The "Disconnected" state for a Media Services account indicates that the account no longer has access to one or more of the attached storage accounts due to a change in storage access keys. Up-to-date storage access keys are required by Media Services to perform many tasks in the account.

The following are the primary scenarios that would result in a Media Services account not having access to attached storage accounts.


| Cause | Solution |
| ----- | -------- |
|The Media Services account or attached storage account(s) were migrated to separate subscriptions. |Migrate the storage account(s) or Media Services account so that they're all in the same subscription or use managed identity for storage account authentication if your storage account is in the same tenant. |
|The Media Services account is using an attached storage account in a different subscription as it was an early Media Services account where this was supported. All early Media Services accounts were converted to modern Azure Resources Manager based accounts and will have a Disconnected state. |Migrate the storage account or Media Services account so that they're all in the same subscription or use managed identity for storage account authentication if your storage account is in the same tenant.|

### Media Services account cannot access storage account

| Cause | Solution |
| ----- | -------- |
|The Media Services managed identity doesn't hasn't been given the Storage Blob Data Contributor role. | To check this in the Azure Portal, first find out which identity is set for the storage account by selecting "Storage accounts" from the menu of the Media Services account, this should be either "System-assigned" or the name of a user-assigned Managed Identity. Next, go to the storage account in the portal, select "Access Control (IAM)" from the menu, select "Role assignments" from the toolbar, then add the role assignment. When adding the role assignment, the Role should be set to "Storage Blob Data Contributor" and the members should be set to the Managed Identity used by the Media Services account to access the storage account. After adding the role assignment, it may take a few minutes for the change to take effect.|