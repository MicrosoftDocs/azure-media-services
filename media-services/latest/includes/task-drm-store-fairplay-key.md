---
author: johndeu
ms.service: media-services 
ms.topic: include
ms.date: 03/15/2022
ms.author: johndeu
---

## Storage of the FairPlay Private Key (.pfx) in Azure Key Vault

The private key (.pfx) that you receive from Apple should be treated as a secure certificate and can be stored in the Azure Key Vault.

To store the private key in the Key Vault, you need to first convert it into a base64 encoded text file.

- The .pfx certificate file should first be converted to base 64 text file by the admin
- Once converted, this file can be stored in Azure DevOps Services as a secure text file. 
- The string can then be stored in Azure KeyVault manually, or as part of a deployment/build script for your solution. An example of storing the FairPlay private certificate in Azure KeyVault can be seen in the [Gridwich project sample code](https://github.com/mspnp/gridwich/blob/main/infrastructure/azure-pipelines/templates/steps/azcli-last-steps-template.yml#L30)

#### Example CLI script to copy  base64 encoded private key file to the Azure KeyVault:

```bash
set -eu
echo key vault : $SHARED_KV_NAME
echo "Copying FairPlay certificate to key vault as secret"
az keyvault secret set --vault-name $SHARED_KV_NAME -n ams-fairPlay-certificate-b64 -f $(FairPlayCertificate.secureFilePath) --output none
```