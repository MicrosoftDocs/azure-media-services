---
title: Create a private endpoint for a Streaming Endpoint
description: This article shows you how to use a private endpoint for a Streaming Endpoint. You'll be creating a private endpoint resource which is a link between a virtual network and a streaming endpoint. This deployment creates a network interface IP address inside the virtual network. The private link allows you to connect the network interface in the private network to the streaming endpoint in the Media Services account. You'll also be creating DNS zones which pass the private IP addresses. Although a private link is used with the Azure products Private Link and Private Link service, the private link used for this exercise is simply the link between the resource and the private endpoint.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 06/08/2022
ms.author: inhenkel
---

# Create a private endpoint for a Streaming Endpoint

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows you how to use a private endpoint for a Media Services Streaming Endpoint. You'll be creating a private endpoint resource which is a link between a virtual network and a streaming endpoint. This deployment creates a network interface IP address inside the virtual network. The private link allows you to connect the network interface in the private network to the streaming endpoint in the Media Services account. You'll also be creating DNS zones which pass the private IP addresses.

Although a private link is used with the Azure products Private Link and Private Link service, the private link used for this exercise is simply the link between the resource and the private endpoint.

The virtual network created for this walk-though is just to assist with the example.

## Restricting access

Internet access to the endpoints in the Media Services account can be restricted in one of two ways:

- Restricting access to all resources within the Media Services account.
- Restricting access separately for each resource by using the IP allowlist.

Creating a private endpoint **DOES NOT** implicitly disable internet access to it.

>[!WARNING]
> Completing this exercise will incur costs.

## Prerequisites

### Create a resource group for this exercise

> [!IMPORTANT]
> It is important that you create all of the resources for this exercise in the same region.  Otherwise, the VNet and VM steps will not work. Decide which region you want to work with based on your subscription VM allowances. For example, your subscription may allow you to create a Windows Server 2019 VM in the West Europe region, but not in the US West 2 region.

### Create a VNet and a VM

Complete the [Quickstart: Create a private endpoint by using the Azure portal](/azure/private-link/create-private-endpoint-portal) to create the VNet and a VM for this exercise. In other words, don't delete the resources at the end.

<!-- Create a media services account -->
[!INCLUDE [create a media services account in the portal](./includes/task-create-media-services-account-portal.md)]

A default Streaming Endpoint (called *default*) is created when you create the account. Creating a User Managed Identity is also required during the setup process.

## Upload files

[!INCLUDE [Upload files with the portal](./includes/task-upload-file-to-asset-portal.md)]

## Create a transform, job and streaming locator

In order to stream media, the video you uploaded needs to be encoded. A transform is an encoding method for the video.

[!INCLUDE [task-create-transform-portal.md](includes/task-create-transform-portal.md)]

<!-- Create a job in the portal -->

To encode the video, you must create an encoding job, that uses the transform to encode the video.

[!INCLUDE [task-create-job-portal.md](./includes/task-create-job-portal.md)]

<!-- Create a streaming locator in the portal -->

[!INCLUDE [task-create-streaming-locator-portal.md](includes/task-create-streaming-locator-portal.md)]

## Start the streaming endpoint

1. Navigate to the Media Services account you created.
1. Select **Streaming endpoints** from the menu. The Streaming endpoints screen will appear.
1. Select the default Streaming endpoint that you created when you set up the Media Services account.  The default Streaming endpoint screen will appear.
1. Select **Start**. Start options will appear.
1. Select **None** from the CDN pricing tier dropdown list.
1. Select **Start**.  The Streaming endpoint will start running. The endpoint is still Internet facing.

## Get the streaming URL

Once you have started the streaming endpoint, you can get the streaming URLs for use with a media player.

1. In the streaming locators list for the asset you are working with, select **Show URLs**. The Streaming URLs sceen will appear.
1. Copy the HLS streaming URL into your clipboard.

## Test without an IP allow list or a private endpoint

Before creating a private endpoint, we will see how this works without it.

1. In a new browser window or tab on your development device, go to the [Azure Media Player demo](https://azuremediaplayerdemo.azurewebsites.net/) page.
1. Paste the URL into the URL field of the player interface.
1. Select Update.

Your video now streams to the Internet.  This is because we haven't yet locked down the IP addresses.

## Change the IP allow list for the streaming endpoint

1. In the portal, navigate to the default streaming endpoint for the Media Services account you are working with.
1. Select **Settings**. The Settings screen will appear.
1. Select the **Specified IP addresses** radio button.
1. In the **Name** field, enter a name for your addresses, such as *Allow none*.
1. In the **Addresses** field, enter *0.0.0.0*.
1. In the **Subnet Prefix Length** field, enter *32*.
1. Select **Save**.
1. **IMPORTANT!** Clear your browser cache. Otherwise you will be playing video fragments that are in the cache.
1. Refresh the Azure Media Player browser window. You should receive a streaming error.

## Create a private endpoint

Now you'll create a private endpoint for the streaming endpoint and be able to stream the video within the VNet, using the VM.

1. In the portal, navigate to the Media Services account you are working with.
1. Select **Networking** from the menu
1. Select the **private endpoint connections** tab.  The private endpoint connection screen will appear.
1. Select **Add a private endpoint**. The Create a private endpoint screen will appear.
1. In the **Name** field, give the private endpoint a name.
1. From the **Region** dropdown list, select the same region you have been working with (it may already be selected).
1. Select **Next: Resource**. The Resource screen will appear.

## Assign the private endpoint to the streaming resource type

1. From the **Connection methods** radio buttons, select the *Connect to an Azure resource in my directory* radio button.
1. From the **Resource type** dropdown list, select *Microsoft.Media/mediaservices*.
1. From the **Resource** dropdown list, select the Media Services account you created.
1. From the **Target sub-resource** dropdown list, select *streaming endpoint*.
1. Select **Next: Virtual Network**.

## Deploy the private endpoint to the virtual network

1. From the **Virtual network** dropdown list, select the virtual network you created earlier.
1. From the **Subnet** dropdown list, select the subnet your created earlier.
1. Select **Next: DNS**.

## Create the DNS zone

To use the streaming endpoint inside your virtual network, create private DNS zones. You can use the same DNS name and get back the private IP address of the streaming endpoint.

On this screen, the **Configuration name**, **Subscription**, **Resource group**, **Private DNS zone** should already be pre-populated.

- Leave all the settings as they are and select **Next: Tags**.
- Optionally, add tags, the select **Review + create**.
- Double-check your settings, then select **Create**.

## Test the streaming URL with the VM in the Vnet

1. Copy the URL from the Azure Media Player window on your desktop.
1. Connect to your VM using the bastion host as you did before in the quickstart.
1. Open a browser in your VM and paste the URL in the URL field.

You should see the video playing since the VM is part of the VNet.

## ARM template

You can use ARM templates to automate deployment. While the deployment is in progress, it's also creating an [Azure Resource Manager (ARM) template](/azure/azure-resource-manager/templates/overview). To see the template, select **Template** from the menu.

## Clean up resources

If you aren't planning to use the resources created in this exercise, simply delete the resource group. If you don't delete the resources, you will be continue to be billed for them.
