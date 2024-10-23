---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 02/09/2023
ms.author: inhenkel
title: View caption streams in the manifest
---

## View the caption streams in the manifest

View the manifest to see the track changes in the manifest file.

1. You should already be on the output asset screen.
1. Select the **storage container link**.  The storage container name starts with the "asset-" prefix. The storage container screen will appear.
1. Select the `.ism` file from the file list. The blob screen will appear.
1. Select **Edit**.
1. Look for the following XML above the `</switch>` element, changing the VTT file names to the ones you've uploaded.

```xml
    <textstream src="sample.cmft" systemBitrate="52" systemLanguage="en-us">
        <param name="systemLanguage" value="en-us" valuetype="data" />
        <param name="outputFlag" value="3" valuetype="data" />
        <param name="systemBitrate" value="52" valuetype="data" />
        <param name="transcriptsrc" value="en-us.vtt" valuetype="data" />
        <param name="textIsDefault" value="TRUE" valuetype="data" />
        <param name="textHlsCharacteristic" value="public.accessibility.transcribes-spoken-dialog" valuetype="data" />
        <param name="trackID" value="1" valuetype="data" />
        <param name="trackName" value="subt_en-us" valuetype="data" />
        <param name="textDisplayName" value="English" valuetype="data" />
        <param name="armId" value="English" valuetype="data" />
    </textstream>
    <textstream src="es-es.cmft" systemBitrate="50333" systemLanguage="">
        <param name="systemLanguage" value="" valuetype="data" />
        <param name="outputFlag" value="3" valuetype="data" />
        <param name="systemBitrate" value="0" valuetype="data" />
        <param name="transcriptsrc" value="es-es.vtt" valuetype="data" />
        <param name="textHlsCharacteristic" value="public.accessibility.transcribes-spoken-dialog" valuetype="data" />
        <param name="trackID" value="1" valuetype="data" />
        <param name="trackName" value="subt" valuetype="data" />
        <param name="textDisplayName" value="Español" valuetype="data" />
        <param name="armId" value="Spanish" valuetype="data" />
    </textstream>
```
