---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
title: Create a transform with the portal
---

### Create a transform with the portal

1. Navigate to the Media Service account you want to work with.
1. Select **Transforms + jobs**.
1. Select **Add transform**. The Add transform screen will appear.
1. Enter a transform name in the **Transform name** field.
1. Optionally, add a description in the **Description** field.
1. Select a transform type from the **Transform type** dropdown list. You can select from one of the following types:
    1. *Encoding* Use a built-in Standard Encoder preset to encode video or audio.
    1. *Copy* Copy video and/or audio stream into an asset that can be streamed.
    1. *Video and audio analyzer* Extract video and/or audio insights from the input media.
    1. *Audio transcription* Apply a set of audio analysis operations such as speech-to-text transcription
    1. *Face detection* Detect occurrences of faces in video timestamps and outputs a JSON format file. The asset must contain a video file.
1. Select a category from the **Built-in preset category** dropdown list. The **Built-in preset** dropdown menu selections will change depending on what you select.
    1. *HEVC (H.265)* Generate video and audio output using the HEVC (H.265) codec presets.
    1. *H.264* Generate video and audio output using the H.264 codec presets.
    1. *Audio only* Generate audio only
1. Select the preset you want to use from the **Built-in preset** dropdown list. *ContentAwareEncoding* is the recommended preset.
1. Select an optimization from the **Performance optimization** dropdown list. You can select from *Balance optimized*, *Speed optimized*, or *Quality optimized*.
1. Select **Add**.
