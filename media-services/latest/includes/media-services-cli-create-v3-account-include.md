---
title: include file
description: include file
author: Juliako
ms.service: media-services
ms.topic: include
ms.date: 05/01/2019
ms.author: juliako
---

## Create a Media Services account

You first need to create a Media Services account. This section shows what you need for the account creation using the Azure CLI.

### Create a resource group

Create a resource group using the following command. An Azure resource group is a logical container into which resources like Azure Media Services accounts and the associated Storage accounts are deployed and managed.

You can substitute `amsResourceGroup` with your value.

```azurecli
az group create --name amsResourceGroup --location westus2
```

### Create a storage account


