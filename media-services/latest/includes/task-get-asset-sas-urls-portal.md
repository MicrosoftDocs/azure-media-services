---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
title: Create or get an asset's SAS URLs in the portal
---

### Create or get an asset's SAS URLs in the portal

1. Navigate to the Media Services account you want to work with.
1. Select **Assets** from the menu. The assets screen will appear.
1. Select the asset you want to work with.
1. Select the Storage container link. The assets container screen will appear.
1. Select **Shared access tokens** from the menu.
1. For the signing method, select either the **Account key** or **User delegation key** from the signing method selections.
1. If there is a stored access policy, and you want to use it, select the stored access policy from the **Stored access policy** dropdown list.
1. Select the type of permission you want from the **Permissions** dropdown list.
1. Give the SAS a start and expiry time and date.
1. If you would like to restrict access to the asset enter the IP addresses that will be allowed to access the asset in the **Allowed IP addresses** field.
1. Select either the **HTTPS** or **HPPTS and HTTP** radio button to set the allowed protocols on the asset.
1. Select the **Generate SAS token and URL** button.  The URLs will appear on the screen.
