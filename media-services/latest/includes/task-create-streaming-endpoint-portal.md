---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 03/17/2022
ms.author: inhenkel
---

### Create a streaming endpoint in the portal

1. Navigate to the Media Services account you want to work with.
1. Select **Streaming endpoints** from the menu.
1. Select **+ Streaming endpoint**. The Create a streaming endpoint screen will appear.
1. Enter a name into the **Streaming enpoint name** field.
1. Select a streaming endpoint type from the **Streaming endpoint types** selections:
    1. **Standard**. Select the Standard streaming endpoint if you expect egress bandwidth to be less than 600 Mbps, and you will not be using a CDN.
    1. **Premium**.  Select the Premium streaming endpoint if you expect egress bandwidth to be higher than 600 Mbps and you plant to use a CDN.
        1. Enter the number of streaming units for the Premium endpoint in the **Streaming units** field.
1. To automatically start the streaming endpoint after it is created, select the **Yes** radio button from the Start streaming endpoint after creation selections. Otherwise, select the **No** radio button.
    > [!WARNING]
    > When the streaming endpoint is started, billing begins.

You can configure the streaming endpoint after you have created it.  See the [Live event streaming best practices guide](../live-event-streaming-best-practices-guide.md) to help you decide the ratio of traffic the streaming endpoint and CDN will handle.
