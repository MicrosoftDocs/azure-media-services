---
title: Reset your account credentials -CLI
description: Use the Azure CLI script to reset your account credentials and get the app.config settings back.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 01/09/2023
ms.author: inhenkel
---

# Azure CLI example: Reset the account credentials

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

The Azure CLI script in this article shows how to reset your account credentials and get the app.config settings back.

## Prerequisites

[Create a Media Services account](./account-create-how-to.md).

## Example script

```cloudshell-bash
# Update the following variables for your own settings:
resourceGroup=amsResourceGroup
amsAccountName=amsmediaaccountname

az ams account sp reset-credentials \
  --account-name $amsAccountName \
  --resource-group $resourceGroup
 ```

[!INCLUDE [media-services-community](includes/media-services-community.md)]
