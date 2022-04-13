---
title: Stream a Microsoft Teams meeting
description: This article describes how to set up Microsoft Teams with Media Services to stream a Teams meeting to an external audience.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 3/16/2022
ms.author: inhenkel
---

# Stream a Microsoft Teams meeting

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article describes how to set up Microsoft Teams with Media Services to stream a Teams meeting to an external audience.

## Prerequisites

>[!IMPORTANT]
> By default, the RTMP out feature is disabled in all Microsoft Teams tenants. The administrators of your MS Teams tenant must either enable it globally or for a select set of users. See [Stream Teams meetings](https://docs.microsoft.com/microsoftteams/stream-teams-meetings). If this is not enabled for you, contact your Teams administrator.

1. Create a [Media Services account](account-create-how-to.md).
1. Create a [live event](live-event-create-how-to.md?tabs=portal).
1. Either [create a new streaming endpoint](streaming-endpoint-create-how-to.md?tabs=portal) or use the default streaming endpoint that is created when you create your Media Services account.
1. Start the streaming endpoint by selecting **Start**.

## Start the live event and get the ingest URL

1. If you didn't start the live event when you created it. Start it by navigating to the new live event, then select **Start**.
1. Once the live event has started, select either **RTMP** or **RTMPS** from the input protocol selections.
1. Copy the **Input URL** below the ingest protocol selections.

Keep this tab open in your browser because you'll come back to it in a later step.

## Add the Custom Streaming app to your Teams meeting

You can only add the app if your Teams administrator has given you the appropriate permissions.

1. Start a Teams meeting.
1. Either from the menu bar or More options, select **Add an app**. Apps that you have permission to use in Teams will appear.
1. Select the **Custom Streaming app** from the list.  The Custom Streaming app details will appear.
1. Select **Add**. The Custom STreaming app start screen will appear.
1. Select **Save**. The Custom Streaming app setting screen will appear. If you don't have streaming permissions, you'll get a message to contact your IT administrator.
1. Paste the Input URL into the **Stream URL** field.
1. Enter any string into the **Stream key** field.
1. Select **Start streaming**.

## See your stream

Go back to the live event page in your browser.  You should see the Teams meeting streaming in the player.

## Create a streaming locator

1. From the live event screen, select **Create output**. The Create an output screen will appear.
1. Select the **Create a streaming locator** tab.
1. For this example, just leave all of the default settings as they are, then select **Create**.
1. Copy the **HLS URL**.

## Test your stream

1. With your browser, open the [Azure Media Player demo page](https://ampdemo.azureedge.net/) in a new tab.
1. Paste the HLS URL into the **URL** field.
1. Select **Update** player. Your live event will begin streaming in the player.
