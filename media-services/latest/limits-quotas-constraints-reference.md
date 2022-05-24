---
title: Quotas and limits in Azure Media Services
description: This topic describes quotas and limits in Microsoft Azure Media Services.
author: jiayali-ms
ms.service: media-services
ms.topic: reference
ms.date: 03/22/2022
ms.author: inhenkel
---

<!-- If you update limits in this topic, make sure to also update /azure/azure-resource-manager/management/azure-subscription-service-limits#media-services-limits -->

# Azure Media Services quotas and limits

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article lists some of the most common Media Services limits, which are also sometimes called quotas.

> [!NOTE]
> For resources that aren't fixed, open a support ticket to ask for an increase in the quotas. Don't create additional Azure Media Services accounts in an attempt to obtain higher limits.

## Account limits

| Resource | Default Limit |
| --- | --- |
| Media Services accounts in a single subscription | 100 (fixed) |

## Asset limits

| Resource | Default Limit |
| --- | --- |
| Assets per Media Services account | 1,000,000|

## Storage limits

Azure Storage block blog limits apply to storage accounts used with Media Services.  See [Azure Blob Storage limits](/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-blob-storage-limits).

These limits include the total stored data storage size of the files that you upload for encoding and the file sizes of the encoded files.  The limit for file size for encoding is a different limit. See [File size for encoding](#file-size-for-encoding-limit).

### Storage account limit

You can have up to 100 storage accounts. All storage accounts must be in the same Azure subscription.

## File size for encoding limit

An individual file that you upload to be encoded should be no larger than 260 GB.

## Jobs (encoding & analyzing) limits

| Resource | Default Limit |
| --- | --- |
| Jobs per Media Services account | 500,000 <sup>(3)</sup> (fixed)|
| Job inputs per job | 50  (fixed)|
| Job outputs per job | 20 (fixed) |
| Transforms per Media Services account | 100  (fixed)|
| Transform outputs in a transform | 20 (fixed) |
| Files per job input|10 (fixed)|

<sup>3</sup> This number includes queued, finished, active, and canceled jobs. It does not include deleted jobs.

Any job record in your account older than 90 days will be automatically deleted, even if the total number of records is below the maximum quota.

## Live streaming limits

| Resource | Default Limit |
| --- | --- |
| Live events <sup>(4)</sup> per Media Services account |5|
| Live outputs per live event |3 <sup>(5)</sup> |
| Max live output duration | [Size of the DVR window](live-event-cloud-dvr-time-how-to.md) |

<sup>4</sup> For detailed information about live event limits, see [Live Event types comparison and limits](live-event-types-comparison-reference.md). Depending on your streaming use case and regional datacenter of choice, AMS is able to accommodate more than 5 live events per Media Services account. Please file a support request to increase your account quota.

<sup>5</sup> Live outputs start on creation and stop when deleted.

## Packaging & delivery limits

| Resource | Default Limit |
| --- | --- |
| Streaming endpoints (stopped or running) per Media Services account | 2 |
| Premium streaming units | 10 |
| Dynamic manifest filters |100|
| Streaming policies | 100 <sup>(6)</sup> per Media Services account <br/> 3 per streaming locator |
| Unique streaming locators associated with one asset at one time | 100<sup>(7)</sup> (fixed) |

<sup>6</sup> When using a custom streaming policy, design a limited set of policies for your Media Service account, and re-use them for your streaming locators whenever the same encryption options and protocols are needed. You should not be creating a new streaming policy for each streaming locator.

<sup>7</sup> Streaming locators are not designed for managing per-user access control. To give different access rights to individual users, use Digital Rights Management (DRM) solutions.

## Protection limits

| Resource | Default Limit |
| --- | --- |
| Options per Content Key Policy |30 |
| Licenses per month for each of the DRM types on Media Services key delivery service per account|1,000,000|

## Support ticket

For resources that are not fixed, you may ask for the quotas to be raised, by opening a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest). Include detailed information in the request on the desired quota changes, use-case scenarios, and regions required. <br/>Do **not** create additional Azure Media Services accounts in an attempt to obtain higher limits.
