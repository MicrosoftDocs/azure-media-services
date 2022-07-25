---
title: Stream a Microsoft Teams meeting
description: This article describes how to set up Microsoft Teams with Media Services to stream a Teams meeting to an external audience.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 7/14/2022
ms.author: inhenkel
---

# Stream a Microsoft Teams meeting

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article describes how to set up Microsoft Teams with Media Services to stream a Teams meeting to an external audience.

## Prerequisites

>[!IMPORTANT]
> By default, the RTMP out feature is disabled in all Microsoft Teams tenants. The administrators of your MS Teams tenant must either enable it globally or for a select set of users. See [Stream Teams meetings](/microsoftteams/stream-teams-meetings). If this is not enabled for you, contact your Teams administrator.

1. Create a [Media Services account](account-create-how-to.md).
1. Create a [live event](live-event-create-how-to.md?tabs=portal) using either a Standard transcoding (720p) live event or a pass-through event. Teams Custom Streaming RTMP output is in beta and currently only supports 720p 30fps output, therefore you should avoid using a Premium transcoding live event for 1080p.
1. Either [create a new streaming endpoint](streaming-endpoint-create-how-to.md?tabs=portal) or use the default streaming endpoint that is created when you create your Media Services account.
1. Start the streaming endpoint by selecting **Start**.

## Start the live event and get the ingest URL

1. If you didn't start the live event when you created it. Start it by navigating to the new live event, then select **Start**.  Make sure to use a Standard encoding live event (720p) or a pass-through live event (Basic or Standard).
1. Once the live event has started, select either **RTMP** or **RTMPS** from the input protocol selections.
1. Copy the **Input URL** below the ingest protocol selections.

Keep this tab open in your browser because you'll come back to it in a later step.

## Add the Custom Streaming app to your Teams meeting

You can only add the app if your Teams administrator has given you the appropriate permissions.

1. Start a Teams meeting.
1. Either from the menu bar or More options, select **Add an app**. A list of apps for Teams will appear.
1. Select the **Custom Streaming app** from the list.  The Custom Streaming app details will appear.
1. Select **Add**. The Custom Streaming app start screen will appear.
1. Select **Save**. The Custom Streaming app setting screen will appear. If you don't have streaming permissions, you'll get a message to contact your IT administrator.
1. Paste the Input URL into the **Stream URL** field.
1. Enter any string into the **Stream key** field.
1. Select **Start streaming**.

## See your stream

Go back to the live event page in your browser.  You should see the Teams meeting streaming in the player.

## Create a live output and streaming locator

To archive your live event to an AMS asset, create a live output on the live event page in the Azure portal. 

1. From the live event screen, select **Create output**. The Create an output screen will appear.
1. Set the output name, archive length, asset name, and storage account location.
1. Select the **Add streaming locator** tab to create a new streaming locator and publish the live output with a time-shift window set to your archive length.  At this point you can choose to use a streaming policy to encrypt the asset with DRM or AES-128, as well as choose a manifest filter and expiration date for the locator.
1. For this example, just leave all of the default settings as they are, then select **Create**. 
1. Copy the HLS or DASH manifest links into any player application that supports the HLS or DASH streaming formats, such as Azure Media Player, Shaka Player, HLS.js, Video.js, Dash.js, ExoPlayer or other commercial player applications.


## Test your stream in  Azure Media Player

1. With your browser, open the [Azure Media Player demo page](https://ampdemo.azureedge.net/) in a new tab.
1. Paste the HLS URL into the **URL** field.
1. Select **Update** player. Your live event will begin streaming in the player.

## Stop your stream and use other features of Media Services and Video Indexer

Once you are done with your event, you can stop the live output, followed by the live event.
Your live event will be archived into the Media Services asset that you created during the steps above to create the live output.  This asset can now be used for on-demand playback using the same URL that you tested above in the Azure Media Player. The URL does not change unless you delete the locator and create another one. Assets can also have several locators attached with different settings, such as a time based filter to trim the start and end off a live event to remove unwanted content.  

The asset you generated from Teams can now be used in any encoding workflows in Azure Media Services, or sent to the Video Indexer service for analytics. All of the features of both Media Services and Video Indexer are available for use on the archived live event asset from Teams.
