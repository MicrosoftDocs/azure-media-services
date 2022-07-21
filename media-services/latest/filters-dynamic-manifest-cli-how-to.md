---
title: Use CLI to create filters with Azure Media Services
description: This article shows how to use CLI to create filters with Azure Media Services v3.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 7/21/2022
ms.author: inhenkel
---
# Creating filters with CLI

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

When delivering your content to customers (streaming Live events or Video on Demand), your client might need more flexibility than what's described in the default asset's manifest file. Azure Media Services enables you to define account filters and asset filters for your content.

For detailed description of this feature and scenarios where it is used, see [Dynamic Manifests](filters-dynamic-manifest-concept.md) and [Filters](filters-concept.md).

This topic shows how to configure a filter for a Video on-Demand asset and use CLI for Media Services v3 to create [Account Filters](/cli/azure/ams/account-filter) and [Asset Filters](/cli/azure/ams/asset-filter).

> [!NOTE]
> Make sure to review [presentationTimeRange](filters-concept.md#presentationtimerange).

## Prerequisites

- [Create a Media Services account](./account-create-how-to.md). Make sure to remember the resource group name and the Media Services account name.

## Define a filter

The following example defines the track selection conditions that are added to the final manifest. This filter includes any audio tracks that are EC-3 and any video tracks that have bitrate in the 0-1000000 range.

> [!TIP]
> If you plan to define **Filters** in REST, notice that you need to include the "Properties" wrapper JSON object.  

```json
[
    {
        "trackSelections": [
            {
                "property": "Type",
                "value": "Audio",
                "operation": "Equal"
            },
            {
                "property": "FourCC",
                "value": "EC-3",
                "operation": "NotEqual"
            }
        ]
    },
    {
        "trackSelections": [
            {
                "property": "Type",
                "value": "Video",
                "operation": "Equal"
            },
            {
                "property": "Bitrate",
                "value": "0-1000000",
                "operation": "Equal"
            }
        ]
    }
]
```

## Create account filters

The following [az ams account-filter](/cli/azure/ams/account-filter) command creates an account filter with filter track selections that were [defined earlier](#define-a-filter).

The command allows you to pass an optional `--tracks` parameter that contains JSON representing the track selections.  Use @{file} to load JSON from a file. If you are using the Azure CLI locally, specify the whole file path:

```azurecli
az ams account-filter create -a amsAccount -g resourceGroup -n filterName --tracks @tracks.json
```

Also, see [JSON examples for filters](/rest/api/media/accountfilters/createorupdate#create-an-account-filter).

## Create asset filters

The following [az ams asset-filter](/cli/azure/ams/asset-filter) command creates an asset filter with filter track selections that were [defined earlier](#define-a-filter). 

```azurecli
az ams asset-filter create -a amsAccount -g resourceGroup -n filterName --asset-name assetName --tracks @tracks.json
```

Also, see [JSON examples for filters](/rest/api/media/assetfilters/createorupdate#create-an-asset-filter).

## Associate filters with Streaming Locator

### Filter your HLS or DASH manifests on creation a Streaming Locator

Media Services allows you to create a Streaming Locator that is pre-filtered by passing in a collection of filters in the filter property on the streaming locator entity. This allows you to pre-filter all manifests on the streaming locator.  The original manifest is no longer available through this streaming locator, and only the filtered response will be accessible to clients requesting the URLs for DASH or HLS from the filtered streaming locator.  
This is helpful in situations where you want to only publish a portion of an asset, and prevent users from gaining access to the full original manifest for the asset by manipulating the query string of the HLS or DASH manifest URL. We recommend that you use this feature if you want to apply filters but do not want to expose the filter names in the URL for customers to manipulate on their own.

You can specify a list of [asset or account filters](filters-concept.md) on your [Streaming Locator](/rest/api/media/streaminglocators/create#request-body). The [Dynamic Packager](encode-dynamic-packaging-concept.md) applies this list of filters together with those your client specifies in the URL. This combination generates a [Dynamic Manifest](filters-dynamic-manifest-concept.md), which is based on filters in the URL + filters you specify on the Streaming Locator.

### Updating filters

Filters and streaming locators can be updates on the fly, but keep in mind that it can take up to 10 seconds for any updates to update on the front-end web servers, and there can be issues with downstream CDN caching of the content if you are updating the same **Streaming Locator** that has been published and used in production already.

It isn't recommended to update the definition of filters associated with an actively published **Streaming Locator**, especially when CDN is enabled. Streaming servers and CDNs can have internal caches that may result in stale cached data to be returned.

If the filter definition needs to be changed consider creating a new filter and adding it to the **Streaming Locator** URL or publishing a uniquely new **Streaming Locator** that references the updated filter directly.

### Use the CLI to create a filtered Streaming Locator
The following CLI code shows how to create a Streaming Locator and specify `filters`. This is an optional property that takes a space-separated list of asset filter names and/or account filter names.

```azurecli
az ams streaming-locator create -a amsAccount -g resourceGroup -n streamingLocatorName \
                                --asset-name assetName \                               
                                --streaming-policy-name policyName \
                                --filters filterName1 filterName2
                                
```

## Stream using filters

Once you define filters, your clients could use them in the streaming URL. Filters could be applied to adaptive bitrate streaming protocols: Apple HTTP Live Streaming (HLS), MPEG-DASH, and Smooth Streaming.

The following table shows some examples of URLs with filters:

|Protocol|Example|
|---|---|
|HLS|`https://amsv3account-usw22.streaming.media.azure.net/fecebb23-46f6-490d-8b70-203e86b0df58/bigbuckbunny.ism/manifest(format=m3u8-aapl,filter=myAccountFilter)`|
|MPEG DASH|`https://amsv3account-usw22.streaming.media.azure.net/fecebb23-46f6-490d-8b70-203e86b0df58/bigbuckbunny.ism/manifest(format=mpd-time-csf,filter=myAssetFilter)`|
|Smooth Streaming|`https://amsv3account-usw22.streaming.media.azure.net/fecebb23-46f6-490d-8b70-203e86b0df58/bigbuckbunny.ism/manifest(filter=myAssetFilter)`|

## Next step

[Stream videos](stream-files-tutorial-with-api.md)

## See also

[Azure CLI](/cli/azure/ams)
