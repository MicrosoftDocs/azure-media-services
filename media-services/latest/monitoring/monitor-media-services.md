---
title: Monitoring Media Services
description: When you have applications and business processes relying on Azure resources, you want to monitor those resources for their availability, performance, and operation. This article describes the monitoring data generated by Media Services and how you can use the features of Azure Monitor to analyze and alert on this data.
author: IngridAtMicrosoft
ms.author: inhenkel
manager: femilia
ms.topic: how-to
ms.service: media-services
ms.date: 02/09/2023
---

# Monitor Media Services

When you have applications and business processes relying on Azure resources, you want to monitor those resources for their availability, performance, and operation. This article describes the monitoring data generated by Media Services and how you can use the features of Azure Monitor to analyze and alert on this data.

## Azure Monitor

Media Services creates monitoring data using [Azure Monitor](/azure/azure-monitor/overview), which is a full stack monitoring service in Azure that provides a complete set of features to monitor your Azure resources in addition to resources in other clouds and on-premises.

Start with reading the article [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource), which describes the following concepts:

- What is Azure Monitor?
- Costs associated with monitoring
- Monitoring data collected in Azure
- Configuring data collection
- Standard tools in Azure for analyzing and alerting on monitoring data

## Media Services monitoring data

Media Services collects the same kinds of monitoring data as other Azure resources that are described in [Monitoring data from Azure resources](/azure/azure-monitor/essentials/monitor-azure-resource#monitoring-data).

All data collected by Azure Monitor fits into one of two fundamental types: metrics and logs. With these two types you can:

- Visualize and analyze the metrics data using Metrics Explorer.
- Monitor Media Services diagnostic logs and create alerts and notifications for them.
- You can send or stream logs to:
  - Azure Storage
  - Azure Event Hubs
  - Log Analytics
  - Use third-party services

## Collection and routing

*Platform metrics* and the *Activity log* are collected and stored automatically, but can be routed to other locations by using a diagnostic setting.

*Resource Logs* are **not** collected and stored until you create a diagnostic setting and route them to one or more locations.

See the article [Create diagnostic setting to collect platform logs and metrics in Azure](/azure/azure-monitor/essentials/diagnostic-settings) for the detailed process of creating a diagnostic setting.

## Media Services metrics

Media Services metrics are collected at regular intervals whether or not the value changes.

### Metric types

Metrics available for Media Services are:

- [Media Services account metrics, including Key Delivery](/azure/azure-monitor/essentials/metrics-supported#microsoftmediamediaservices)
- [Live event metrics](/azure/azure-monitor/essentials/metrics-supported#microsoftmediamediaservicesliveevents)
- [Streaming endpoint metrics](/azure/azure-monitor/essentials/metrics-supported#microsoftmediamediaservicesstreamingendpoints)

### Analyzing metrics

You can analyze metrics for Media Services along with metrics from other Azure services using Metrics Explorer. See [Getting started with Azure Metrics Explorer](/azure/azure-monitor/essentials/metrics-getting-started) for details on using this tool.

## Media Services logs

### Activity logs

The [Activity log](/azure/azure-monitor/essentials/activity-log) is a platform log that provides insight into subscription-level events. You can view it independently or route it to Azure Monitor Logs, where you can do much more complex queries using Log Analytics.

### Resource logs

Resource logs provide rich and frequent data about the operation of an Azure resource. For more information, see [How to collect and consume log data from your Azure resources](/azure/azure-monitor/essentials/platform-logs-overview).

Media Services supports the following resource logs:
[Microsoft.Media/mediaservices](/azure/azure-monitor/essentials/resource-logs-categories#microsoftmediamediaservices)

### Media Services diagnostic logs

Some things that you can examine with diagnostic logs are:

- The number of licenses delivered by DRM type
- The number of licenses delivered by policy
- The latency on key delivery requests
- The number of unauthorized license requests from clients

## Analyzing logs

Data in Azure Monitor Logs is stored in tables where each table has its own set of unique properties.

All resource logs in Azure Monitor have the same fields followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/azure/azure-monitor/essentials/resource-logs-schema#top-level-common-schema).

## Alerts

Azure Monitor alerts proactively notify you when important conditions are found in your monitoring data. They allow you to identify and address issues in your system. You can set alerts on metrics, logs, and the activity log. For more information, see [Azure Monitor Alerts overview](/azure/azure-monitor/alerts/alerts-overview).

## Schemas

For detailed description of the top-level diagnostic logs schema, see [Supported services, schemas, and categories for Azure Diagnostic Logs](/azure/azure-monitor/essentials/resource-logs-schema).

### Media Account Health

| **Name** | **Description** |
| ------- | -------------- |
|  TimeGenerated  |  The timestamp (UTC) of when the event was generated. |
|  OperationName  |  The name of the operation that triggered the event. |
|  Level  |  Message level. Possible values are Informational, Warning, Error, Critical and Verbose. |
|  Location  |  Location of the service sending the log. |
|  EventCode  |  The event code. |
|  EventMessage  |  The event status message. |

### Key Delivery

| **Name** | **Description** |
| ------- | -------------- |
|  TimeGenerated  |  The timestamp (UTC) of when the event was generated. |
|  OperationName  |  The name of the operation that triggered the event. |
|  OperationVersion  |  Azure Media Services operation version. |
|  ResultType  |  Azure Media Services operation result type. |
|  ResultSignature  |  Azure Media Services operation result signature. |
|  DurationMs  |  Azure Media Services operation duration in milliseconds. |
|  Level  |  Message level. Possible values are Informational, Warning, Error, Critical and Verbose. |
|  Location  |  Location of the service sending the log. |
|  RequestId  |  Id of the request. |
|  KeyType  |  Could be one of the following values: Clear (no encryption), FairPlay, PlayReady, or Widevine. |
|  KeyId  |  The ID of the requested key. |
|  TokenType  |  The token type. |
|  PolicyName  |  The Azure Resource Manager name of the policy. |
|  StatusMessage  |  The status message. |

#### Sample key delivery log

```json
{
    "time": "2019-01-11T17:59:10.4908614Z",
    "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-0000000000/RESOURCEGROUPS/SBKEY/PROVIDERS/MICROSOFT.MEDIA/MEDIASERVICES/SBDNSTEST",
    "operationName": "MICROSOFT.MEDIA/MEDIASERVICES/CONTENTKEYS/READ",
    "operationVersion": "1.0",
    "category": "KeyDeliveryRequests",
    "resultType": "Succeeded",
    "resultSignature": "OK",
    "durationMs": 315,
    "identity": {
        "authorization": {
            "issuer": "http://testacs",
            "audience": "urn:test"
        },
        "claims": {
            "urn:microsoft:azure:mediaservices:contentkeyidentifier": "3321e646-78d0-4896-84ec-c7b98eddfca5",
            "iss": "http://testacs",
            "aud": "urn:test",
            "exp": "1547233138"
        }
    },
    "level": "Informational",
    "location": "uswestcentral",
    "properties": {
        "requestId": "b0243468-d8e5-4edf-a48b-d408e1661050",
        "keyType": "Clear",
        "keyId": "3321e646-78d0-4896-84ec-c7b98eddfca5",
        "policyName": "56a70229-82d0-4174-82bc-e9d3b14e5dbf",
        "tokenType": "JWT",
        "statusMessage": "OK"
    }
}
```

### Live Events

| **Name** | **Description** |
| ------- | -------------- |
|  TimeGenerated  |  The timestamp (UTC) when the event was generated. |
|  OperationName  |  The name of the operation that triggered the event. |
|  Level  |  Message level. Possible values are Informational, Warning, Error, Critical and Verbose. |
|  Location  |  Location of the service sending the event. |
|  Properties  |  Operation details. |

#### Sample live event log

```json
[
    {
        "TimeGenerated": "2022-10-11T06:02:13.4730825Z",
        "OperationName": "LIVEEVENTS/INGESTBEGIN",
        "Level": "Informational",
        "Location": "westcentralus",
        "Properties": {"liveEventName":"CONTOSOLIVE","streamName":"1234","remoteIP":"10.0.0.xxx","remotePort":"35091"}
    },
    {
        "TimeGenerated": "2022-10-11T06:02:19.8229491Z",
        "OperationName": "LIVEEVENTS/STREAMINFO",
        "Level": "Informational",
        "Location": "westcentralus",
        "Properties": {"liveEventName":"CONTOSOLIVE","remoteIP":"10.0.0.xxx","remotePort":"35091","trackName":"audio_160000","trackType":"audio","bitrate":160000,"timestamp":66,"timescale":1000,"resolution":"n/a"}
    },
    {
        "TimeGenerated": "2022-10-11T06:04:41.1375866Z",
        "OperationName": "LIVEEVENTS/INGESTEND",
        "Level": "Informational",
        "Location": "westcentralus",
        "Properties": {"liveEventName":"CONTOSOLIVE","streamName":"1234","remoteIP":"10.0.0.xxx","remotePort":"35091","resultCode":"MPE_CLIENT_TERMINATED_SESSION"}
    },
    {
        "TimeGenerated": "2022-10-11T06:07:01.0446756Z",
        "OperationName": "LIVEEVENTS/INGESTDISCONTINUITY",
        "Level": "Warning",
        "Location": "westcentralus",
        "Properties": {"liveEventName":"CONTOSOLIVE","trackName":"audio","timestamp":156777,"discontinuityGap":12605}
    }
]
```

### Streaming Endpoints

| **Name** | **Description** |
| ------- | -------------- |
|  TimeGenerated  |  The timestamp (UTC) when the event was generated. |
|  OperationName  |  The name of the operation that triggered the event. |
|  OperationVersion  |  Azure Media Services operation version. |
|  Level  |  Message level. Possible values are Informational, Warning, Error, Critical and Verbose. |
|  Location  |  Location of the service sending the event. |
|  ClientIP  |  IP address of the client. |
|  URL  |  The streaming URL from Azure Media Services. |
|  Status  |  Status code of the request. |

#### Sample streaming endpoint log

```json
[
    {
        "time": "2022-09-30T07:40:06.1524833Z",
        "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000001/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.MEDIA/MEDIASERVICES/CONTOSOMEDIA/STREAMINGENDPOINTS/DEFAULT",
        "operationName": "MICROSOFT.MEDIA/MEDIASERVICES/STREAMINGENDPOINTS/GET",
        "category": "StreamingEndpointRequests",
        "level": "Informational",
        "location": "uswc1",
        "properties": {
            "ClientIP": "10.0.0.1",
            "URL": "https://cdn--contosomedia-uswc.streaming.media.azure.net:443/00000000-0000-0000-0000-000000000000/contoso.ism/QualityLevels(127999)/Fragments(aac_eng_2_127999_2_1=20053333,format=mpd-time-csf)",
            "Status": "200"
        },
        "operationVersion": "1.0"
    }
]
```

## How-tos

- [Route Media Services metrics to storage](monitor-metrics-save-to-storage-how-to.md)
- [Audit Media Services control plane logs](monitor-log-analytics-workspaces-how-to.md)
- [Autoscaling premium streaming endpoints](../streaming-endpoint-autoscaling-how-to.md)
- [Create an Azure Monitor dashboard and alerts](monitor-create-dashboard-alerts-how-to.md)
