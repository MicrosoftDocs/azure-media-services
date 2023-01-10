---
title: Quotas and limits in Azure Media Services
description: This topic describes quotas and limits in Microsoft Azure Media Services.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: reference
ms.date: 01/09/2023
ms.author: inhenkel
---

<!-- If you update limits in this topic, make sure to also update /azure/azure-resource-manager/management/azure-subscription-service-limits#media-services-limits -->

# Azure Media Services quotas and limits

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article lists some of the most common Media Services limits, which are also sometimes called quotas.

> [!NOTE]
> For resources that aren't fixed, open a support ticket to ask for an increase in the quotas. Don't create additional Azure Media Services accounts in an attempt to obtain higher limits.

## Account limits

| Resource | Default Limit | Per |
| --- | --- | ---|
| Media Services accounts | 100 (fixed) | Subscription |

## Asset limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Assets per Media Services account | 1,000,000| Media Services account |

## Storage limits

Azure Storage block blog limits apply to storage accounts used with Media Services.  See [Azure Blob Storage limits](/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-blob-storage-limits).

These limits include the total stored data storage size of the files that you upload for encoding and the file sizes of the encoded files.  The limit for file size for encoding is a different limit. See [File size for encoding](#file-size-for-encoding-limit).

### Storage account limit

You can have up to 100 storage accounts. All storage accounts must be in the same Azure subscription.

## File size for encoding limit

An individual file that you upload to be encoded should be no larger than 260 GB.

## Jobs and transforms (encoding & analyzing) limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Jobs | 500,000 <sup>(3)</sup> (fixed) | Media Services account <br/> in a 3 month sliding window |
| Input assets | 50  (fixed)| Job |
| Output assets | 20 (fixed) | Job |
| Videos | 100 <sup>(4)</sup> (fixed) | Job |
| Transforms | 100  (fixed) | Media Services account |
| Output encoding types | 20 (fixed) | Transform |
| Files |10 (fixed) | Input Asset |

<sup>3</sup> This number includes queued, finished, active, and canceled jobs. It does not include deleted jobs.

<sup>4</sup> There is an exception to this limit. The limit of 50 job inputs per job supersedes the limit of 100 clips per job. For example, if there are 51 job inputs and each job input contains 1 clip, then that will violate the limit of 50 job inputs per job, even though the clips per job limit has not been met.

Any job record in your account older than 90 days will be automatically deleted, even if the total number of records is below the maximum quota.

## Live streaming limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Live events <sup>(5)</sup> |5| Media Services account |
| Live outputs writing data to an output asset |3 <sup>(6)</sup> | Live Event |
| Max live output duration | [Size of the DVR window](live-event-cloud-dvr-time-how-to.md) | Live output |

<sup>5</sup> For detailed information about live event limits, see [Live Event types comparison and limits](live-event-types-comparison-reference.md). Depending on your streaming use case and regional data center of choice, AMS is able to accommodate more than 5 live events per Media Services account. Please file a support request to increase your account quota.

<sup>6</sup> Live outputs start on creation and stop when deleted.

## Timed metadata limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Total message body payload size | 256 kb max | Request |
| Requests | 2 | per second  |

## Packaging & delivery limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Streaming endpoints (stopped or running) | 2 | Media Services account |
| Premium streaming units | 50 | Streaming Endpoint |
| Dynamic manifest account filters | 100 | Media Services account |
| Dynamic manifest asset filters | 100 | Asset |
| Streaming policies | 100 <sup>(7)</sup> | Media Services account |
| Streaming policies | 3 | Streaming Locator |
| Unique streaming locators | 100<sup>(8)</sup> (fixed) | Asset |

<sup>7</sup> When using a custom streaming policy, design a limited set of policies for your Media Service account, and re-use them for your streaming locators whenever the same encryption options and protocols are needed. You should not be creating a new streaming policy for each streaming locator.

<sup>8</sup> Streaming locators are not designed for managing per-user access control. To give different access rights to individual users, use Digital Rights Management (DRM) solutions.

## Protection limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Optional claims  |30 | Content Key Policy |
| Licenses on Media Services key delivery service | 1,000,000 | Each type<br/>Month |

## Support ticket

For resources that are not fixed, you may ask for the quotas to be raised, by opening a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest). Include detailed information in the request on the desired quota changes, use-case scenarios, and regions required. <br/>Do **not** create additional Azure Media Services accounts in an attempt to obtain higher limits.

[!INCLUDE [media-services-community](includes/media-services-community.md)]
