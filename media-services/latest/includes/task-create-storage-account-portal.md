---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/03/2022
ms.author: inhenkel
---

### Create an Azure Storage account with the portal

To create a storage account, you must first create a resource group within a location (region) if it doesn't already exist.

[!INCLUDE [task-create-resource-group-portal](task-create-resource-group-portal.md)]

### Create the storage account

1. Navigate to the resource group you want to work with.
1. Select **+ Create** to create a new resource.
1. Search for *Storage account* in the search bar and select *Storage account*.
1. Select the **Create** button. The Create a storage account screen will appear.
1. Under Project details, select the subscription you want to work with from the **Subscription** dropdown list.
1. Select the resource group you want to work with in the **Resource group** dropdown list.
1. Under Instance details, enter the storage account a name in the **Storage account name** field.
1. Select a region (location) for your storage account from the **Region** dropdown list.
1. Select either the **Standard** radio button or the **Premium** radio button from the Performance selections.
1. Select the redundancy type you want from the **Redundancy** dropdown list.
1. Select the **Next:Advanced >** button.
1. Select the **Security**, **Data Lake Storage Gen2**, and **Blob storage** and **Azure files** settings according to your needs.
1. Select the **Next:Networking >** button.
1. Select the **Network connectivity**, and **Network routing** settings according to your needs.
1. Select the **Next: Data protection >** button.
1. Select the **Recovery**, **Tracking**, and **Access control** settings according to your needs.
1. Select the **Next: Encryption >** button.
1. Select the **Encryption type**, **Enable support for customer-managed keys**, and **Enable infrastructure encryption** according to your needs.
1. Select the **Next: Tags >** button.
1. Add tags to your storage account if you need to create more metadata about your storage account.
1. Select the **Next: Review + create >** button.
1. Review the settings for your storage account.
1. Select the **Create** button. The storage account will start deploying.
1. Once the storage account has been deployed, you can review its properties by selecting the **Go to resource** button.
