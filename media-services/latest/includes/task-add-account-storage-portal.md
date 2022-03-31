---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/08/2022
ms.author: inhenkel
---

### Add a storage account to a Media Services account with the portal

Before you add a storage account to a Media Services account, if the storage account doesn't already exist, [create a new storage account](../storage-create-how-to.md).

>[!NOTE]
> If you just created a storage account, it will take a few minutes before it shows up in the list of storage accounts. Also if you are adding role assignments for managed identity, it may take a few minutes for the changes to take effect.

1. Navigate to the media services account you want to work with.
1. Select **Storage accounts** from the menu.
1. Select Select **+ Storage account**. The choose storage account screen will appear.
1. If you are using managed identities, see notes above on using managed identities and storage accounts to make sure you have the correct role assigned.
1. Select the storage account you want to add to your Media Services account from the list. The storage account will appear on under Storage accounts.
    >[!WARNING]
    > If you created a storage account in a different location (region) from your Media Services account, it will not show up in the list.  Media Services accounts and storage accounts must be in the same region.
1. Select **Save**.

#### Errors when attaching storage accounts in the portal

If you receive an error stating that the portal is "unable to access the storage account *{{storage-account-name}}* with the access token, it is likely that you are assigning a storage account with a managed identity that does not have the Storage Blob Contributor role assignment.

[!INCLUDE [task-add-managed-identity-portal](task-add-managed-identity-portal.md)]
