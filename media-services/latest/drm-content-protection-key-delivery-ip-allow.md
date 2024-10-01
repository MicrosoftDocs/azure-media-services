---
title: Restrict access to DRM license and AES key delivery using IP allowlists
description: Learn how to restrict access to DRM and AES Keys by using IP allowlists.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 01/09/2023
ms.author: inhenkel
---
# Restrict access to DRM license and AES key delivery using IP allowlists

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

When securing media with the [content protection](./drm-content-protection-concept.md) and DRM features of Media Services, you could encounter scenarios where you need to limit the delivery of licenses or key requests to to a specific IP range of client devices on your network. To restrict content playback and delivery of keys, you can use the IP allowlist for Key Delivery.

In addition, you can also use the allowlist to completely block all public internet access to Key Delivery traffic and only allow traffic from your private network endpoints.

The IP allowlist for Key Delivery restricts the delivery of both DRM licenses and AES-128 keys to clients within the supplied IP allowlist range.

Media Services supports IPv6 for streaming. The Media Services Live Event, Streaming Endpoint, and key delivery services can be used by clients over both IPv4 and IPv6.

## Setting the allowlist for key delivery

The settings for the Key Delivery IP allowlist are on the Media Services account resource. When creating a new Media Services account, you can restrict the allowed IP ranges through the **KeyDelivery** property on the [Media Services account resource.](/rest/api/media/mediaservices/create-or-update)

The **defaultAction** property can be set to "Allow" or "Deny" to control delivery of licenses and keys to clients in the allowlist range.

The **ipAllowList** property is an array of single IPv4 or IPv6 address and/or ranges using [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation).

## Setting the allowlist in the portal

The Azure portal provides a method for configuring and updating the IP allowlist for key delivery.  Navigate to your Media Services account and access the **Key delivery** menu under **Settings**.

## Streaming endpoints IPv6 support

When a Streaming Endpoint is configured to use a CDN, IP address support is configured in the CDN provider settings.

For Streaming Endpoints that do not use a CDN, by default, Streaming Endpoints accept requests from any IPv4 address. To enable all IPv4 and IPv6 addresses, create allow both IPv4 and IPv6 in the IP allow list:

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Media/mediaservices/{accountName}/streamingEndpoints/se1?api-version=2020-05-01
Authorization: Bearer {{getArmToken.response.body.access_token}}
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "accessControl": {
      "ip": {
        "allow": [
          {
            "name": "Allow all IPv6 addresses",
            "address": "::",
            "subnetPrefixLength": 0
          },
          {
            "name": "Allow all IPv4 addresses",
            "address": "0.0.0.0",
            "subnetPrefixLength": 0
          }
        ]
      }
    },
    "cdnEnabled": false
  },
 "location": "{resourceLocation}"
}
```

The IP allow list for a Streaming Endpoint may also include specific IPv6 addresses or ranges.

## Live Events IPv6 support

By default, Live Events accept content from any IPv4 address. To allow any IPv4 or IPv6 address, allow both IPv4 and IPv6 addresses in the IP allow list:

The IP allow list for a Live Event may also include specific IPv6 addresses or ranges.
Key Delivery IPv6 support
By default, content key requests are accepted from any IPv4 or IPv6 address. The Key Delivery IP allow list may be used to restrict the IP addresses that may connect to key delivery endpoints.

The IP allow list may contain:

- IPv4 addresses
- IPv4 CIDR ranges
- IPv6 addresses
- IPv6 CIDR ranges

The following example sets the IP allow list for key delivery:

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Media/mediaservices/{mediaAccountName}?api-version=2021-11-01

{
  "properties": {
    "storageAccounts": [
      {
        "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"
      }
    ],
    "keyDelivery": {
      "accessControl": {
        "defaultAction": "Deny",
        "ipAllowList": [ "10.0.0.0/16", "2001:1234:1234::4567/32", "2001:1235::"]
      }
    },
  },
  "location": "westus"
}
```

For this example, the request from the following addresses will be accepted:

- IPv6 addresses between 2001:1234:1234:0000:0000:0000:0000:4567 and 2001:1234:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF,
- IPv6 address 2001:1235:0000:0000:0000:0000:0000:0000
- IPv4 addresses between 10.0.0.0 and 10.0.255.255

Additional examples:

- To allow requests from any IP address, set the “defaultAction” of the “accessControl” block to “Allow” (and do not specify an “ipAllowList)
- To allow all IPv4 addresses and block all IPv6 addresses, set the IP allow list to [ "0.0.0.0/0" ]
- To allow all IPv6 addresses and block all IPv6 addresses, set the IP allow list to [ "::/0" ]

[!INCLUDE [media-services-community](includes/media-services-community.md)]
