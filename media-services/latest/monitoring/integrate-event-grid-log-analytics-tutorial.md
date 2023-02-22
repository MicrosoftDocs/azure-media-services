---
title: Store Media Services events in Azure Log Analytics
description: Azure Media Services v3 emits events on Azure Event Grid. You can subscribe to events in many ways and store them in data stores. In this tutorial, you will subscribe to Media Services events using a Log App Flow. The Logic App will be triggered for each event and store the body of the event in Azure Log Analytics. Once the events are in Azure Log Analytics, you can use other Azure services to create a dashboard, monitor, and alert on these events, though we won't be covering that in this tutorial.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: tutorial
ms.date: 02/21/2023
ms.author: inhenkel
---

# Tutorial: Store Azure Media Services events in Azure Log Analytics

## Azure Media Services Events

Azure Media Services v3 emits events on [Azure Event Grid](monitoring/media-services-event-schemas.md). You can subscribe to events in many ways and store them in data stores. In this tutorial, you will subscribe to Media Services events using a [Log App Flow](https://azure.microsoft.com/services/logic-apps/). The Logic App will be triggered for each event and store the body of the event in Azure Log Analytics. Once the events are in Azure Log Analytics, you can use other Azure services to create a dashboard, monitor, and alert on these events, though we won't be covering that in this tutorial.

You will learn how to:

> [!div class="checklist"]
> * Create a no code Logic App Flow
> * Subscribe to Azure Media Services event topics
> * Parse events and store to Azure Log Analytics
> * Query events from Azure Log Analytics

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## Prerequisites

* An Azure subscription.
* A [Media Services](account-create-how-to.md) account and resource group.
* A [Log Analytics](/azure/azure-monitor/logs/quick-create-workspace) workspace


## Subscribe to a Media Services event with Logic App

1. In the Azure portal, if you haven't done so already, create a [Log Analytics](/azure/azure-monitor/logs/quick-create-workspace) workspace. You'll need the Workspace ID and one of the keys, so keep that browser window open. Then, open the portal in another tab or window.
1. Navigate to Media Services account you want to work with.
1. Select **Events**. This will show all the methods for subscribing to Azure Media Services events.
1. Select the **Logic Apps** to create a Logic App. This will open the Logic App Designer where you can create the flow to capture the events and push them to Log Analytics.
1. Select **Sign in** for the Azure Event Grid connection.
1. Select the tenant (subscription) you want to work with. The sign-in screen will appear.
1. Sign-in to your Microsoft account.
1. Select **Sign in**. The Logic App will connect to the Azure Event Grid for that subscription.
1. Select **Continue**. The When a resource event occurs screen will appear.
1. Leave the value in the Subscription field as it is.
1. Select *Microsoft.Media.MediaServices* from the **Resource Type** dropdown list.
1. Select the **Event Type item**. There will be a list of all the events Azure Media Services emits. You can select the events you would like to track. You can add multiple event types. (Later, you will make a small change to the Logic App flow to store each event type in a separate Log Analytics Log and propagate the Event Type name to the Log Analytics Log name dynamically.)
1. Select **Save As**.
1. Give your Logic App a name.  The resource group is selected by default. Leave the other settings the way they are, then select **Create**.  You will be returned to the Azure home screen.

## Create an action

Now that you are subscribed to the event(s), create an action.

1. If the portal has taken you back to the home screen, navigate back to the Logic App you just created by searching All resources for the app name.
1. Select the app you want to work with.
1. Select **Logic app designer**. The designer screen will appear.
1. Select **+ New Step**.
1. Search for "Azure Log Analytics Data Collector" and then select it.
1. Go back to the tab or window for the Log Analytics Workspace.
1. Select **Agents**. This will show you the agent keys that have been generated.
1. Select the **down arrow** next to Log Analytics agent instructions.
1. Copy the **Workspace ID** value.
1. In the other browser tab or window, under the Azure Log Analytics Data Collector select **Send Data**, give your connection a name, then paste the *Workspace ID* in the **Workspace ID** field.
1. Return to the Workspace browser tab or window and copy the **Primary key** value.
1. In the other browser tab or window, paste the primary key value in the **Workspace Key** field.
1. Select **Create**. Now you will create the JSON request body and the Custom Log Name.
1. Select the **JSON Request body** field.  A link to **Add dynamic content** will appear.
1. Select **Add Dynamic content**.
1. Select **Topic**.
1. Select **Custom Log Name**. A link to **Add dynamic content** will appear.
1. Select **Topic**
1. Select **Code View** of the Logic App. Look for the Inputs and Log-Type lines.
1. Find the items under "actions".
1. Change the `body` value from `"@triggerBody()?['topic']"` to `"@{triggerBody()}"`. This is for parsing the entire message to Log Analytics.
1. Change the `Log-Type` from `"@triggerBody()?['topic']"` to `"@replace(triggerBody()?['eventType'],'.','')"`. (This will replace "." as these are not allowed in Log Analytics Log Names.)
1. Select **Save**.
1. To verify, select **Logic app designer**.
1. When you examine all the resources in the resource group, there will be a Logic App and two Logic App API connectors listed, one for the Events and one for Log Analytics. For more information about Event Grid system topics, read [Event Grid System Topics](/azure/event-grid/system-topics).

## Test

Once you have the Logic App created, create a live event and start a live stream with your on-premises live encoder. If you haven't set up a live event for Media Services before, try the OBS [Quickstart](live-event-obs-quickstart.md)

## Verify the events

With the live stream, Azure Media Services is emitting various events that are triggering the Logic App flow. To verify, navigate to the Logic App and determine if there are any triggers being fired by the events from Media Services.

1. Navigate to the Logic App Overview page, you should see "Run History" listing jobs that have completed successfully.
1. Select a successful job. The details of the job during runtime are shown.
1. Select **Send Data** to expand it. In this case, the `MicrosoftMediaLiveEventEncoderConnected` event shows that it was captured as well as the parsed body. This is what is pushed to the Azure Log Analytics Workspace.

## Verify the logs

1. Navigate to Log Analytics Workspace you created earlier.

1. Select **Logs**.
1. Close the Example queries popup.
1. There will be a Custom Logs listing. Select the down arrow to expand it. There you will see the event name `MicrosoftMediaLiveEventEncoderConnected`.
1. Select the event name to expand it.
1. When you select the "eye" icon, it will show a preview of the query result.
1. Select **See in query editor** and then select the item under **TimeGenerated UTC** listing to expand it and view the raw data.

## Delete resources

If you don't want to continue to use the resources you created during this tutorial, make sure you delete all of the resources in the resource group or you will continue to be charged.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
