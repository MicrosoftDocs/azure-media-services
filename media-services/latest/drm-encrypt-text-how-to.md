---
title: How to encrypt captions using AES-128 Clear Key encryption
description: When enabling AES-128 clear key encryption, text tracks can be configured to be encrypted using a full "envelope" encryption technique that follows the same encryption pattern as the audio and video segments. These segments can then be decrypted by a client application after requesting the decryption key from the Media Services Key Delivery service using an authenticated JWT token. This method is supported by the Azure Media Player, but may not be supported on all devices and can require some client-side development work to make sure it succeeds on all platforms. This article shows you how to encrypt captions using AES-128 Clear Key encryption. It isn't necessary to do anything special with the text tracks. If you use AES-128 clear key encryption with the asset, the captions will also be encrypted.
ms.topic: how-to
ms.date: 02/21/2023
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-media-services
---

# How to encrypt captions using AES-128 Clear Key encryption

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

It isn't necessary to do anything special with the text tracks (captions, subtitles, etc.) to encrypt them. If you use AES-128 clear key encryption with the asset, the captions will also be encrypted.

## Prerequisites

- Read [Content protection with dynamic encryption and key delivery](drm-content-protection-concept.md).
- Understand an implementation of custom claims by reading [Claims-based identity and concepts in SharePoint](/sharepoint/dev/general-development/claims-based-identity-and-concepts-in-sharepoint)

## Step 1: Create a content key policy with AES Clear Key

You will choose token restriction for this example. Before you start working with these steps, open Notepad or other text editor to keep track of the values you will be creating as they will be used to generate a JWT.

1. Sign in to the Azure portal.
1. Navigate to the Media Services account you want to work with.
1. Select **Content key policies**. The *Content key policy* screen will appear.
1. Select **+ Add content key policy**. The Create content key policy screen will appear.
1. Enter a name for the policy in the **Content key policy** name field.
1. Enter a description in the **Description** field (optional).
1. In the *AES clear key section* under the *Choose encryption options section*, select **+ Add**. The *Add AES clear key policy option* screen will appear.
1. Enter a policy name in the **Policy option name** field.
1. Select the *Use token restriction* **Yes** radio button.
1. Select *JWT* from the **Token type** dropdown list.
1. Enter an issuer in the **Issuer** field. Copy and paste this value into your text editor.
1. Enter an audience in the **Audience** field. Copy and paste this value into your text editor.
1. Leave the **Primary verification key** field empty to generate a primary key.
1. Enter any custom claims you want to be applied to the policy. For more information about custom claims see [Claims-based identity and concepts in SharePoint](/sharepoint/dev/general-development/claims-based-identity-and-concepts-in-sharepoint).
1. Select **Add**. The content key policy will be added to the list of policies.
1. Select **Edit** next to the policy you just created from the list. The *Edit content key policy* screen will appear.
1. Select the **Edit** (pencil) icon next to the AES clear key you just created.
1. Copy and paste the primary verification key value from the Primary verification key into your text editor.

## Step 2: Generate a JWT with the AES Clear Key policy

You can use the [JWT Debugger](https://jwt.io/#debugger-io) to generate a JWT token. No matter what method you use to generate the JWT, the values that have to be in the payload are `issuer`, `audience` and `key`. Use the text editor where you have stored the values from the previous steps to create JSON similar to the following:

```json
{
    "issuer": "myissuer",
    "audience": "allthepeople",
    "key" : "yPkMjhX3AK3lPhbIR4+yGFIQU6QO/tRdKCkt4Thw/PZuhl53SkaaYqZURzqaLdWiShvrk3NRtAD9+0qd7kC0PA=="
}
```

1. If you are using JWT Debugger, the JWT will automatically update when you change the values in the payload.
1. Copy and paste the JWT into your text editor.

## Step 3: Create a streaming locator with Predefined_ClearKey and the content key policy

For the following steps, it is assumed that you have uploaded and encoded a media file which would have produced an output asset.

1. In the portal, navigate to the asset you want to work with.
1. Select **+ streaming locator**. The *Add streaming locator* screen will appear.
1. Enter a name for the streaming locator in the **Name** field.
1. Select *Predefined_ClearKey* from the **Streaming policy** dropdown list.
1. Select the content key policy you just created from the **Content key policy** dropdown list.
1. Set the expiration time.
1. For this example, don't select filters.
1. Leave the **streaming locator ID** field empty for the ID to be auto-generated.
1. Select **Add**. The new streaming locator will appear in the streaming locators list for the asset.

> [!TIP]
> Make sure your streaming endpoint is started. Otherwise, when you test with the player, nothing will be streaming to it.

## Set up the player client authentication

Instructions for setting up your player client are not included here. However, for this example we will use the [Azure Media Player (AMP)](https://azuremediaplayerdemo.azurewebsites.net/) client demo. You can learn more about setting up AMP for DRM [here](../azure-media-player/azure-media-player-protected-content.md).

You should already be on the Assets page in the portal.

1. Select **Show URLs** next to the streaming locator you just created.
1. Select the **copy** icon next to the streaming URL you want to use to copy it onto your clipboard.
1. Open the [AMP demo player](https://azuremediaplayerdemo.azurewebsites.net/) in your browser.
1. Select the **Advanced options** checkbox.
1. Paste the streaming URL into the **URL** field.
1. Select the **AES protection** checkbox.
1. Copy the JWT value from your text editor and paste it into the **AES Token** field.
1. Select **Update Player**. The content should start streaming.

[!INCLUDE [Warning on captions and encryption](./includes/warning-captions-encryption.md)]

[!INCLUDE [media-services-community](includes/media-services-community.md)]
