---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 03/17/2022
ms.author: inhenkel
---

### Create a live event in the portal

1. Navigate to the Media Services account you want to work with.
1. Select **Live streaming** from the menu.
1. Select **+ Add live event**. The Create live event screen will appear.
1. In the **Live event name** field, enter a name for the live event.
1. You can optionally add a description in the **Description** field.
1. Select one of the following radio buttons from the Live event type selections:
    1. **Standard pass-through**. Use this event type when you want basic streaming and live transcriptions (optional).
    1. **Basic pass-through**.  Use this event type when you have input assets that have multiple tracks and you don't want to encode or use live transcriptions.
    1. **Standard encoding**. Use this event type when you have one video input stream and one audio input stream. You can stream up to 720p.
    1. **Premium encoding**.  Use this event type when you have one video input stream and one audio input stream, and you want multi-bitrate output at 1080p.
1. Select either the **RTMP** or **Smooth streaming ingest** radio button to tell the live event what protocol the contribution encoder will send.
1. Notice the Sample input URL under the Static hostname prefix selections.
1. Select one of the following radio button from the Static hostname prefix selections. You will see the Sample input URL change depending on your selection.
    1. **None**. The input URL will have a random 128 bit hex string prepended to the URL.
    1. **Use live event name**. The input URL will have the live event name prepended to the URL.
    1. **Use custom name**. The custom name field will appear.
        1. Enter the name you want to use in the **Custom hostname prefix** field. The input URL will have custom name prefix you enter prepended to the URL.
1. You can either choose to start the live event automatically once it is created or you can start the live event later. Select either the **Yes** or **No** radio button.
    >[!WARNING] If you start the live event once it has been created, your billing for the live event will begin.
1. At this point you can either select the **Review + create** or **Next: Advanced >** button.
1. Select the checkbox next to the *I have all the rights to use the content/file, and agree that it will be handled per the Online Services Terms  and the Microsoft Privacy Statement*.
1. Select **Create** to create the live event.

### Advanced: Security and latency

#### Restrict streaming to the input URL

To restrict input access to the live event, select the **Yes** radio button from the Restrict input access selections. The IP Address and Subnet prefix length fields will appear. Enter the IP address that you want to allow to stream to the live event.

#### Restrict access to the preview

To restrict access to the preview of the live event, select the **Yes** radio button from the Restrict preview access selections. The IP Address and Subnet prefix length fields will appear. Enter the IP address that you want to allow to view the live event preview.

### Reduce latency

To reduce the latency of a live event, select the **Yes** radio button for Low latency mode. 

You can also set the input key frame interval by entering the value in seconds in the **Input key frame interval** field.

### Enable live transcription

1. Enable live transcription by selecting the **Yes** radio button next to Enable live transcription. The **Language** dropdown list will appear.
1. Select a language from the **Language** dropdown list.

#### Tags

You can also add tags to the live event by selecting the **Tags** tab.
