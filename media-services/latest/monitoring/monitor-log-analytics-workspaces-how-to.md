---
title: Audit Media Services control plane logs
description: This article shows you how to audit Media Services control plane logs with Log Analytics Worskpaces.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 02/09/2023
ms.author: inhenkel
---

# Audit Media Services Control Plane logs

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

[Azure Monitor](/azure/azure-monitor/overview) enables you to monitor metrics that help you understand how your applications are performing.

This article shows you how to audit Media Services control plane logs with Log Analytics Worskpaces.

## Prerequisites

- [Create a Media Services account](../account-create-how-to.md).
- Review  [Monitor Media Services](monitor-media-services.md).
- Create a [Log Analytics Workspace](/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-portal)

## Enable diagnostic logs for control plane operations

You can enable diagnostic logs for control plane operations by using the Azure portal. After enabling, the diagnostic logs will record the operation as a pair of start and complete events with relevant details.

Use the following steps to enable logging on control plane operations:

1. Sign into the [Azure portal](https://portal.azure.com/).
1. Navigate to the Media Services account you want to work with.
1. Select **Diagnostic Settings** under Monitor.
1. Select **Add diagnostic setting**.
1. Enter a name in the **Diagnostic setting name** field.
1. Select the **Audit** and/or **AllLogs** checkbox. Alternatively, you can select the type of log you want. For example, you can check **Key Delivery Requests** or **Media Account Health Status**.
1. Select the **Send to Log Analytics workspace** checkbox.
1. The subscription for the Media Services account should already be selected in the **Subscription** dropdown list.
1. Select the workspace from the **Log Analtyics workspace** dropdown list. If there are no workspaces listed, [create one](/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-portal).
1. Select Save.

## View the control plane operations

After you turn on logging, you can use Kusto to query the logs using the Azure Monitor Workspace. The following is a basic example of querying the logs:

1. Sign into the [Azure portal](https://portal.azure.com/).
1. Select **Monitor** and then select the **Logs** pane. It opens a UI where you can easily run queries with that specific account in scope. Run the following query to view control plane logs:

```kusto
AzureDiagnostics
| where ResourceProvider=="MICROSOFT.MEDIASERVICES" and Category=="ControlPlaneRequests"
| where TimeGenerated >= ago(1h)
```

For more information about working with Log Analytics Workspaces, see [Log Analytics workspace overview](/azure/azure-monitor/logs/log-analytics-workspace-overview).
