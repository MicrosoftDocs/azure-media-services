---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 04/21/2022
ms.author: inhenkel
title: Store Media Services metrics using the CLI
---

### Store Media Services metrics using the CLI

To enable storage of diagnostic logs in a Storage Account, you would run the following `az monitor diagnostic-settings` Azure CLI command:

```cloudshell-bash
az monitor diagnostic-settings create --name <diagnostic name> \
    --storage-account <name or ID of storage account> \
    --resource <target resource object ID> \
    --resource-group <storage account resource group> \
    --logs '[
    {
        "category": <category name>,
        "enabled": true,
        "retentionPolicy": {
            "days": <# days to retain>,
            "enabled": true
        }
    }]'
```
