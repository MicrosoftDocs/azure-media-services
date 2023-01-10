---
title: Autoscale Media Services premium streaming endpoints
description: This article discusses how you can autoscale the premium streaming endpoints in your Media Services account based on any available metrics for the streaming endpoint, or metrics for any related entities.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 01/09/2023
ms.author: inhenkel
---

# Autoscale Media Services premium streaming endpoints

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## Overview

You have a large, live streaming media event coming up but you’re not sure how
many streaming units you are going to need. Not planning for enough resources
can cause issues with playback quality at media delivery time.

Fortunately, you can autoscale the premium streaming endpoints in your Media
Services account based on any available metrics for the streaming endpoint, or
metrics for any related entities. A combination of these metrics can be used to
create the rule for autoscaling.

> [!NOTE]
> Custom autoscaling is only available for premium streaming endpoints. However, you can also easily switch from standard to premium endpoints without any interruptions in service.

Autoscaling a Media Services streaming endpoint is easy to do using Azure
Autoscale.

Some examples of metrics you may use for autoscaling are:

- The average CPU usage goes over 50% in the last 10 minutes.
- The average egress bandwidth goes over 200Mbps per streaming unit in the last 10 minutes.
- A high number of requests result in a particular error code, a 503 server unavailable status code, and output format in the last 30 minutes.

You can also autoscale based on the number of running live events.

## Set up autoscaling for a streaming endpoint in the Azure portal

### Set up a default condition

1. From the Azure home screen, select **Monitor** from the main menu, or select
    More services à and select the **Monitor** icon.
1. Select **Autoscale** from the menu. The Autoscale screen will open.
1. Select the subscription you want to work with from the **Subscription**
    dropdown list.
1. Select the resource group from the **Resource group** dropdown list.
1. Select *Media Services* from the **Resource type** dropdown list.
1. Select the premium streaming endpoint that you want to autoscale from the streaming endpoint list. The Autsocale setting screen will appear.
1. Select the **Configure** tab.
1. Select the **Custom autoscale** radio button.
1. The **Autoscale setting name** field will already be populated, but you can change it if you need to.
1. The **Resource group** dropdown list will have the resource group already
    selected.
1. Give the Default autoscaling condition a name, or not.
1. Choose either the:
    1. **Scale to a specific instance count** radio button.
        1. Enter the number of streaming instances you want in the **Instance
            count** field. If you make this choice, the streaming endpoints will
            scale to the set amount automatically or when none of the other
            conditions are present, if you created rules based on a metric.
    1. **Scale based on a metric** radio button.
        1. Select **Add a rule** from the warning message. The Scale rule
            screen appears. The metric source should already be selected.
        1. Select **Average, Minimum, Maximum, Sum, Last** or **Count** from the Time aggregation dropdown list.
        1. The Metric namespace should already be selected.
        1. Select **CPU usage, Egress, Egress bandwidth, Requests, or Success end to end latency** from the Metric name dropdown list.
        1. You can get more information about each metric by choosing a dimension. Dimensions available for some metrics are **Error Code, HTTP Status Code,** and **Output Format**. Select one or more of these based on what information you need.
        1. Select an operator from the **Operator** dropdown list. For example, if you want to autoscale when the CPU is greater than 70%, then choose **Greater than**.
        1. In the Action section, choose the action from the **Operation** dropdown list, enter the number of minutes in the **Cool down** field, and enter the number of instances to increase by in the **Instance count** field. For example, enter *Increase count by 1* and wait for *15 minutes* before checking again to see if the CPU usage is greater than 70%.
1. Select **Add**.
1. Enter values for the **Minimum**, **Maximum** and **Default** number of instances there should be for the premium streaming endpoint.

### Set up additional conditions

Demand for the streaming endpoint may go up or down during a range of time. If
you expect a surge in audience for upcoming live streaming events, you can set
up a time-based autoscale rule to allocate enough streaming units beforehand. Be
sure to allow 20 minutes for streaming units to be fully provisioned.

Follow the same steps as above but to schedule autoscaling, choose the **Time
zone**, the **Start date** and **End date** to apply the condition. You can also
schedule the condition during recurring time period by selecting **Repeat
specific days** radio button then selecting the days.

> [!NOTE]
> Be aware that the default condition is the one that will be applied when no other conditions have been met.

### Editing or deleting an autoscaling condition

To edit the condition, select the **pencil** icon.

To delete the condition either select the **trash can** icon in the header of
the condition area or select the **pencil** icon and select the **Delete**
button from the Scale rule screen.

## More information

For more information about autoscaling in Azure, see [Overview of autoscale in
Microsoft
Azure](/azure/azure-monitor/autoscale/autoscale-overview).

[!INCLUDE [media-services-community](includes/media-services-community.md)]
