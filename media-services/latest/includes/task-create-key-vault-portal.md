---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 02/24/2023
ms.author: inhenkel
title: Create a key vault with the portal
---

<!--Create a key vault in the portal-->

### Create a key vault with the portal

1. Enter *Key vault* into the main search field and select **Key Vault** when it appears in the search results.
1. Select **Create key vault**.  The Create key vault screen appears.
1. Select the **Resource group** you want to use or create a new one.
1. Entering a name into the **Key Vault name** field.
1. Select the region from the **Region** dropdown list.
1. Select a pricing tier from the **Pricing tier** dropdown list.
1. Enter the number of days in the **Days to retain deleted vaults** field.
1. Enable or disable purge protection using the **Purge protection** radio buttons.
1. Select **Next**. The access policy screen will appear.
1. Select either the **Vault access policy** or **Azure role-based access control** to give the user appropriate permissions.
1. Optional: Select one or more of the **Resource access** checkboxes.
1. Optional: Select the user in the **User** list if you want finer grained control of access.
1. Select **Next**. The Networking screen will appear.
1. Select or deselect the **Enable public access** checkbox. If you choose to disable public access:
    1. Select the **All networks** radio button to allow all public access, or select the **Selected networks** radio button to restrict network traffic to selected IPs.
    1. Select the **+ Add a virtual network** down arrow and select either **Add existing virtual networks** or **Add new virtual network**. In the first case, select the already created virtual network.  In the second case, the Create virtual network screen appears and you will use it to create a virtual network.
1. Select **Allow trusted Microsoft services to bypass this firewall** checkbox if you want to give access to other services.
1. Optional: Select **Create a private endpoint** if you would like to create a private endpoint for the key vault. The Create private endpoint screen will appear.
    1. Select the subscription you want to work with from the **Subscription** dropdown menu if it isn't already selected along with the resource group.
    1. Select a location (region) from the **Location** dropdown list.
    1. Enter a name for the private endpoint in the **Name** field.
    1. Select the already created virtual network from the **Virtual network** dropdown list.
    1. Select the subnet from the **Subnet** dropdown list.
    1. Select **Integrate with private DNS zone** toggle to toggle it between Yes or No.
    1. Select the zone from the **Private DNS zone** dropdown list.
1. Select **Review + create**. The portal will check for any issues with the setup.
1. Select **Create** to deploy the key vault.
