---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/30/2022
ms.author: inhenkel
title: Delete an assets with Python
---

### Delete an asset with Python


1. Create an .env file to keep your credentials. A [sample.env](https://github.com/Azure-Samples/media-services-v3-python/blob/main/sample.env) file is available in the Media Services Python samples.

2. Import the necessary modules.

:::code language="python" source="~/../media-services-v3-python/all/assets.py" id="AssetImports":::

3. Get and instantiate environment variables from the .env file.

:::code language="python" source="~/../media-services-v3-python/all/assets.py" id="EnvironmentVariables":::

4. Create a Media Services client and authenticate

:::code language="python" source="~/../media-services-v3-python/all/assets.py" id="CreateAMSClient":::

5. Create an asset
:::code language="python" source="~/../media-services-v3-python/all/assets.py" id="DeleteAsset":::