---
title: Create an Azure Monitor dashboard and alerts
description: Once you have created charts for account, live event, or streaming endpoint metrics, you can pin them to a dashboard. You can create dashboards for multiple Media Services accounts under one subscription. Metrics charts are provided by Azure Monitor.
You can create alerts to let you know when a metric has reached or exceeded a threshold. For example, you can create an alert that lets you know when you are getting close to your asset quota, or when you have a spike in media requests. This article shows you how to create dashboards and set alerts for Media Services resources.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 07/27/2022
ms.author: inhenkel
---

# Create an Azure Monitor dashboard and alerts

Once you have created charts for account, live event, or streaming endpoint metrics, you can pin them to a dashboard. You can create dashboards for multiple Media Services accounts under one subscription. Metrics charts are provided by Azure Monitor.
You can create alerts to let you know when a metric has reached or exceeded a threshold. For example, you can create an alert that lets you know when you are getting close to your asset quota, or when you have a spike in media requests. This article shows you how to create dashboards and set alerts for Media Services resources.

## Create a blank dashboard

Before you start creating charts for your Media Service resources, create a blank dashboard.

1. In the Azure portal, select the menu at the top left of the screen.
1. Select **Dashboard** from the menu. Your default Azure dashboard will appear.
1. Select **+ New Dashboard** and then **Blank dashboard**.
1. Give your dashboard a name.
1. Select **Save**.

## Create an asset quota chart

Relevant metrics for encoding are:

**Asset count**, **asset quota**, **asset quota used percentage**, and **job quota**. You may want to watch these metrics when you are running encoding jobs to either ensure that you aren’t going over your current quota, or to keep track of this data over time, so you can plan for encoding capacity in the future.

For the below steps, you will start with a line chart. You can change this chart to an area chart, a bar chart, a scatter chart or a grid.

1. Navigate to the Media Services account you want to work with.
1. From the menu, select **Metrics**. The Metrics screen will appear. Media Services account scope and metric namespace should already be chosen.
1. Select **Asset quota used percentage** from the Metric list. The Y axis will change to a range from 0 to 100 percent.
1. Select a different time range from the list of time ranges above the chart. The X axis will change to the time range you selected.    **NOTE:** There are no filters for Media Services account metrics.
1. Select **Save to dashboard**, then select **Pin to dashboard**.
1. Select the **Private type** radio button.
1. Select the AMS dashboard you just created from the **Dashboard** list. You will see a notification that the chart was pinned to the dashboard.

## Create an asset quota alert

1. Select **New alert rule**. The Create an alert rule screen will appear.
1. Select the **Condition** tab if it isn’t already selected. The Select a signal screen will appear.
1. Select *Asset quota used percentage* from the list. A chart will appear.
1. Select the chart period you want to use.
1. For this example, you will send an alert when the number of assets in your account reaches 0% of your asset quota. Enter *0* in the Threshold value field. (The reason you are using 0% is because we want to test the alert.  If you don’t have a lot of assets in your Media Services account, the alert won’t get triggered.  You can change the percentage once you see that the alert works.)
1. Set the **Aggregation granularity period** to *1 hour* or an interval that suits your needs.
1. Set the **Frequency of evaluation** to the time period frequency you want the percentage to be checked.
1. Select **Done**.
1. Select the **Actions** tab.
1. Select **+ Create an action group**. The Create an action group screen will appear.
1. In the **Action group name** field, enter a name for the action group. The Display name field will auto-populate.
1. Select the **Notifications** tab.
1. Select *Email/SMS message/Push/Voice* from the **Notification** type list. The Email/SMS message/Push/Voice screen will appear.
1. Enter a name in the **Name** field for the notification type.
1. In the Email/SMS message/Push/Voice screen, select the **Email** checkbox and enter an email into the **Email** field.
1. Select **OK**.
1. Select **Review + create**.

You should receive an email within the hour indicating that your asset count is over 0% of the asset quota. Once you have received the email, you can edit the alert rule and change any of the conditions.  To change the conditions:

1. From the Azure portal main menu, select **Monitor**.
1. Select **Alerts**.
1. Select **Alert rules**.
1. Select the alert rule you created.
1. Under the **Condition** heading, select the **Condition** name. The Configure signal logic screen will appear.
1. Change the **Threshold value** from *0* to the percentage of the asset quota you prefer for the alert.

## Create a streaming endpoint chart

Relevant metrics for streaming endpoints are:

**CPU (for premium endpoints only)**, **egress**, **egress bandwidth**, **requests**, and **SuccessE2ELatency**. You can use these metrics to track the requests, as well as the size and rate of the data from your streaming endpoint. You can also use them to determine the latency between a request for media and its delivery.

1. Navigate to the Media Services account you want to work with.
1. Select **Streaming endpoints** from the menu.
1. Select the streaming endpoint that you want to work with from the streaming endpoint table.
1. From the menu, select **Metrics**. The Metrics screen will appear. The streaming endpoint scope and metric namespace should already be chosen.
1. Select the time period you want to monitor. The default is *Local time last 24 hours*.
1. Select the metric you want to work with such as *Egress*.
1. Select the aggregation type from the **Aggregation** dropdown. There may be only one to choose from such as Sum.
1. You can add filters or apply splitting on things such as *Output format*.
1. Select **Save to dashboard**, then select **Pin to dashboard**.
1. Select the **Private type** radio button.
1. Select the AMS dashboard you just created from the **Dashboard** list. You will see a notification that the chart was pinned to the dashboard.

## Set up a streaming endpoint alert

You can set up an alert to help you take action on standard streaming endpoints. The process is similar to creating an asset alert.

If you are using premium streaming endpoints, you can also set up [autoscaling](../streaming-endpoint-autoscaling-how-to.md).