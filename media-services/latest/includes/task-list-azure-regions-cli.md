---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 05/13/2021
ms.author: inhenkel
title: List azure regions
---

<!--List Azure regions CLI-->

Use this command to list the regions available for your account.

```azurecli
az account list-locations --query "[].{DisplayName:displayName, Name:name}" -o table
```
