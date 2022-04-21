---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 04/21/2022
ms.author: inhenkel
title: Store Media Services metrics using the portal
---

### Store Media Services metrics using the portal

1. Log in to the [Azure portal](https://portal.azure.com).
1. Navigate to the Media Services account you want to work with.
1. Select **Diagnostic Settings** under **Monitor**. Here you see a list of all resources in your subscription that produce monitoring data through Azure Monitor.
1. Select **Add diagnostic setting**. A resource diagnostic setting is a definition of *what* monitoring data should be routed from a particular resource and *where* that monitoring data should go.
1. In the section that appears, give your setting a **name** and check the box for **Archive to a storage account**.
1. Select the storage account to which you want to send logs and press **OK**.
1. Check all the boxes under **Log** and **Metric**. Depending on the resource type, you may only have one of these options. These checkboxes control what categories of log and metric data available for that resource type are sent to the destination you've selected, in this case, a storage account.
1. Set the **Retention (days)** slider to 30. This slider sets a number of days to retain the monitoring data in the storage account. Azure Monitor automatically deletes data older than the number of days specified. A retention of zero days stores the data indefinitely.
1. Select **Save**.

You may need to wait up to five minutes before the event appears in the storage account.

1. In the portal, navigate to the **Storage Accounts** section by finding it on the left-hand navigation bar.
1. Identify the storage account you created in the preceding section and click on it.
1. Select **Blobs**, then on the container labeled **insights-logs-keydeliveryrequests**. This is the container that has your logs in it. Monitoring data is broken out into containers by resource ID, then by date and time.
1. Navigate to the PT1H.json file by selecting a container for resource ID, date, and time.
1. Select the PT1H.json file and click **Download**.

 You can now view the JSON event that was stored in the storage account.
