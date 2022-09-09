---
title: Encoding speed and performance
description:
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 09/08/2022
ms.author: inhenkel
---

# Encoding speed and performance

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Encoding complexities are encoder settings optimized for different video attributes. There are three complexities that the Standard Encoder supports:

- Speed Optimized: The encoder uses settings that are optimized for faster encoding. Quality is sacrificed to decrease encoding time.
- Balanced Optimized: The encoder uses settings that achieve a balance between speed and quality.
- Quality Optimized: The encoder uses settings that are optimized to produce higher quality output at the expense of slower overall encoding time.

## Codec Support

Media Services currently supports two output codecs, H.264 for HEVC (H.265). Each codec supports all three encoding complexities. The API offers options to set the desired encoding complexity. If not set, the encoder chooses its own encoding settings with a default of "balanced".

## Set complexity for a transform output

Use PresetConfigurations when defining an encoding transform output, and set the complexity to "speed", "quality", or "balanced".

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
                "Complexity" : "balanced"
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
    "description": "Transform output for speed complexity",
    "outputs": [
        {
        "preset": {
            "@odata.type": "#Microsoft.Media.StandardEncoderPreset",
            "Complexity" : "balanced"
        }
      }
    ]
  }
}
```

## Pricing

- H.264 Basic mode (speed optimized) is priced at a different tier than balanced or quality optimized with a 0.5 multiplier per resolution. See the Media Services pricing page for details on Encoding pricing.
- H.264 Basic mode (speed optimized) pricing does NOT apply to Content Aware Encoding. The Content Aware Encoding preset is a 2-pass solution, and if its Complexity is set to “speed,” the preset outputs will be speed optimized, but will be charged the same as the balanced or quality optimized complexities.
- The pricing for H.264 and H.264 Basic mode is agnostic to frame rates. <= 30 frames/sec, >30 frames/sec and <60 frames/sec, and >60 frames/sec and <=120 frames/sec are all charged at the same price for the H.264 codec. They are charged at different prices for the HEVC (H.265) codec.

| **Definition** | **Speed**  | **Balanced**          | **Quality**            |
| :------------: | :--------: | :-------------------: | :--------------------: |
|                | <= 30 fps  | 30 fps < and > 60 fps | 60 fps < and > 120 fps |
| SD             | $0.0075    | $0.015                | $0.015                 |
| HD             | $0.015     | $0.03                 | $0.03                  |
| 4K             | $0.03      | $0.06                 | $0.06                  |


