---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/11/2022
ms.author: inhenkel
title: Storage account connection issues
---

<!-- Moved from storage account concept page -->

## Storage account connection issues

The "Disconnected" state for a Media Services account indicates that the account no longer has access to one or more of the attached storage accounts due to a change in storage access keys. Up-to-date storage access keys are required by Media Services to perform many tasks in the account.

The following are the primary scenarios that would result in a Media Services account not having access to attached storage accounts.


| Cause | Solution |
| ----- | -------- |
|The Media Services account or attached storage account(s) were migrated to separate subscriptions. |Migrate the storage account(s) or Media Services account so that they're all in the same subscription or use managed identity for storage account authentication if your storage account is in the same tenant. |
|The Media Services account is using an attached storage account in a different subscription as it was an early Media Services account where this was supported. All early Media Services accounts were converted to modern Azure Resources Manager based accounts and will have a Disconnected state. |Migrate the storage account or Media Services account so that they're all in the same subscription or use managed identity for storage account authentication if your storage account is in the same tenant.|