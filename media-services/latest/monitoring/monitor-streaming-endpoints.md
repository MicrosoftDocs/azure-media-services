---
title: Monitor streaming endpoints
description: There are monitoring metrics available for Media Services streaming endpoints. Monitoring metrics assist you in keeping track of the health of your streaming endpoints so you can act when your streaming endpoints aren’t performing as expected. This article discusses metrics for streaming endpoints and the reasons to use them.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 07/27/2022
ms.author: inhenkel
---

# Monitor streaming endpoints

There are monitoring metrics available for Media Services streaming endpoints. Monitoring metrics assist you in keeping track of the health of your streaming endpoints so you can act when your streaming endpoints aren’t performing as expected. This article discusses metrics for streaming endpoints and the reasons to use them.

> [!TIP]
> When you create a support ticket, include the data you gathered from monitoring these metrics in the description. This will assist us in understanding your issue more quickly and help you solve problems in less time.

## Metrics available for streaming endpoints

- Average CPU usage over time.
- Average egress over time which can be filtered by format.
- Average, minimum, and maximum egress bandwidth over time.
- Average, minimum, success end to end latency over time.
- The number of requests filtered by HTTP status code, error code or format over time.

## Reasons to monitor streaming endpoints

There are three main reasons to monitor streaming endpoints, knowing when to:

- Upgrade to premium streaming endpoints
- Scale streaming endpoints
- Contact support

## When to upgrade to premium streaming endpoints

There are two reasons you might want to consider upgrading to premium streaming
endpoints

- **When your streaming endpoint’s egress consistently hits or gets close to the egress limit.** Standard streaming endpoints have an egress limit of 600 Mbps and it isn’t possible to scale a standard streaming endpoint with more streaming units.
- **When the CPU for your standard streaming endpoint consistently hits or gets close to the CPU usage limit.** When a streaming unit’s CPU usage gets to 80%, Media Services will begin throttling requests because it is overloaded. You will start to see performance issues.

To determine if you need to upgrade to a premium streaming endpoint, monitor the average egress or CPU usage of your streaming endpoints over a period of time, for example, a month. If your streaming endpoint stays close to either limit over that time, you might want to upgrade. Alternatively, you can set an alert for this condition and decide to upgrade based on how many alerts you received.

See [Create an Azure Monitor dashboard and alerts](monitor-create-dashboard-alerts-how-to.md)

## When to scale premium streaming endpoints

As stated earlier, when the CPU usage of a premium streaming endpoint reaches 80%, Media Services begins throttling it, and you will see performance issues.

The egress limit of a premium streaming endpoint is 200 Mbps. If you are consistently getting close to the limit, then you should scale the premium streaming endpoint.

You may want to scale your endpoints up or down depending on demand. For example, if you are using Media Services with your intranet and you know that you will see less traffic on the weekend and more during the weekday, you would scale the premium streaming endpoint to only what is necessary for those time periods. In this case, use the average, minimum, and maximum egress bandwidth metrics to determine when you need more or fewer streaming units.

You can either [set an alert](link to how to) for when the average CPU usage for your streaming endpoint gets close to this percentage so you can manually scale the streaming units to meet your needs, or you can use [Azure autoscaling](../streaming-endpoint-autoscaling-how-to.md) to dynamically scale your premium streaming endpoints for you.

## When to contact support

Monitoring application requests can reveal patterns that point to issues with the way you have configured your application to use Media Services including the way you have encoded your assets, latency problems due to network configuration, and issues with the CDN, among other things.

You can use the following filters for requests:

- The average number of success end to end latency requests over time.
- The minimum and maximum number of success end to end latency requests over time.
- The number of requests that result in an HTTP status code over time.
- The number of requests that result in an error code over time.
- The number of requests for an output format over time.

If you are seeing the number of requests for a filter sporadically, the problem will probably resolve itself. However, if you see a lot of the same types of problem metrics, then open a support ticket.

For example, if you see a large number of 503 HTTPS status codes, then either the CDN or the client can’t reach the streaming endpoint origin. A 404 error would indicate that you have published your assets incorrectly.

## How-tos, tutorials and samples

[Autoscaling premium streaming endpoints](../streaming-endpoint-autoscaling-how-to.md)
[Create an Azure Monitor dashboard and alerts](monitor-create-dashboard-alerts-how-to.md)