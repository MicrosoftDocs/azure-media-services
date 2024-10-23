---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 05/13/2021
ms.author: inhenkel
title: Show properties of Media Services account in the CLI
---

<!--Show Media Services Managed Identity CLI-->

This command shows all of the properties of a Media Services account.

```cloudshell-bash
az ams account show --name <your-media-services-account-name> --resource-group <your-resource-group>
```

> [!NOTE]
> If you have assigned access roles to the Media Services account, this line will return `"storageAuthentication": "ManagedIdentity"`.

Example JSON response:

```json
{
  "encryption": {
    "keyVaultProperties": null,
    "type": "SystemKey"
  },
  "id": "/subscriptions/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/resourceGroups/your-resource-group-name/providers/Microsoft.Media/mediaservices/your-media-services-account",
  "identity": {
    "principalId": "ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0",
    "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
    "type": "SystemAssigned"  //Type will show "Managed Identity" if you have assigned a role to the Media Services account.
  },
  "location": "your-region",
  "mediaServiceId": "00000000-0000-0000-0000-000000000000",
  "name": "your-media-services-account",
  "resourceGroup": "your-resource-group-name",
  "storageAccounts": [
    {
      "id": "/subscriptions/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/resourceGroups/your-resource-group-name/providers/Microsoft.Storage/storageAccounts/your-storage-account-name",
      "resourceGroup": "your-resource-group-name",
      "type": "Primary"
    }
  ],
  "storageAuthentication": "System", //If you have assigned access roles to the account, this line will return storageAuthentication": "ManagedIdentity"
  "systemData": {
    "createdAt": "2021-05-14T21:25:12.3492071Z",
    "createdBy": "you@example.com",
    "createdByType": "User",
    "lastModifiedAt": "2021-05-14T21:25:12.3492071Z",
    "lastModifiedBy": "you@example.com",
    "lastModifiedByType": "User"
  },
  "tags": null,
  "type": "Microsoft.Media/mediaservices"
}
```
