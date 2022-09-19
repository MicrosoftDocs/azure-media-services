---
title: Encoding speed and performance
description: Encoding complexities are encoder settings optimized for different video attributes. There are three complexities that the Standard Encoder supports Speed Optimized - The encoder uses settings that are optimized for faster encoding. Quality is sacrificed to decrease encoding time. Balanced Optimized - The encoder uses settings that achieve a balance between speed and quality and Quality Optimized -The encoder uses settings that are optimized to produce higher quality output at the expense of slower overall encoding time.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 09/08/2022
ms.author: inhenkel
---

# Encoding speed and performance

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Encoding complexities are encoder settings optimized for different video attributes. There are three complexities that the Standard Encoder supports:

- **Speed Optimized** The encoder uses settings that are optimized for faster encoding. Quality is sacrificed to decrease encoding time.
- **Balanced Optimized** The encoder uses settings that achieve a balance between speed and quality.
- **Quality Optimized** The encoder uses settings that are optimized to produce higher quality output at the expense of slower overall encoding time.

The API offers options to set the desired encoding complexity. If not set, the encoder chooses its own encoding settings with a default of "balanced".

## Set complexity for a transform output

For a built-in preset, use `PresetConfigurations` when defining an encoding transform output, and set the complexity to "speed", "quality", or "balanced".

```rest

{
  "properties": {
    "description": "Transform output for balanced complexity",
    "outputs": [
        {
        "preset": {
            "@odata.type": "#Microsoft.Media.BuiltInStandardEncoderPreset",
            "presetName": "AdaptiveStreaming",
            "PresetConfigurations":[
                "Complexity": "balanced"
            ]
        }
      }
    ]
  }
}
```

For a custom preset, set you don't need to use PresetConfigurations.  Simply set the complexity parameter.

```
{
  "properties": {
    "description": "Transform output for balanced complexity",
    "outputs": [
        {
        "preset": {
            "@odata.type": "#Microsoft.Media.StandardEncoderPreset",
            "Complexity": "balanced"
        }
      }
    ]
  }
}
```

## H.264 Basic Mode

H.264 Basic Mode is a separate encoding pricing tier. It includes all encoding outputs that are 1-pass, speed optimized, and use the H.264 codec. Balanced and quality optimized encoding outputs are priced the same as the standard H.264 codec. To receive H.264 Basic Mode pricing, set the Complexity to “speed.” See the [Media Services pricing page](https://azure.microsoft.com/pricing/details/media-services/) for details.

> [!NOTE]
> Note: H.264 Basic Mode pricing tier does NOT include [Content-Aware Encoding](/azure/media-services/latest/encode-content-aware-concept). The Content-Aware Encoding preset is a 2-pass solution, with the first pass pre-analyzing the input content and using the results to determine the optimal number of layers, bitrate, and resolutions. If the Content-Aware Encoding preset is set to the “speed” complexity, the preset output will still be speed-optimized but will be charged at the “balanced” and “quality” H.264 codec pricing.
