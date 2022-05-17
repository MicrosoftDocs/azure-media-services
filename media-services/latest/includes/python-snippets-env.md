---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/25/2022
ms.author: inhenkel
title: Python snippets env message
---

The functions in the Python code snippets assume that you have:

1. Imported the necessary modules. These are shown for each Media Services entity.
2. Created and edited an .env file that contains your authentication values. You can get a [sample.env](https://github.com/Azure-Samples/media-services-v3-python/blob/main/sample.env) file from Media Services Python samples.
3. Read and instantiated environment variables by using load_env() as below. Depending on what you are doing, you may or may not need some of the variables.
4. Created a Media Services client as below.