---
title: Create a private endpoint for a Streaming Endpoint
description: This article shows you how to use a private endpoint with a Streaming Endpoint. This deployment creates a network interface IP address inside the virtual network. The private endpoint allows you to connect the network interface in the private network to the streaming endpoint in the Media Services account. You'll also be creating DNS zones which pass the private IP addresses.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 06/07/2022
ms.author: inhenkel
---

# Create a private endpoint for a Streaming Endpoint

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

This article shows you how to use a private endpoint with a Streaming Endpoint. This deployment creates a network interface IP address inside the virtual network. The private endpoint allows you to connect the network interface in the private network to the streaming endpoint in the Media Services account. You'll also be creating DNS zones which pass the private IP addresses.

You'll be creating a private endpoint resource which is a link between a virtual network and a streaming endpoint. This deployment creates a network interface IP address inside the virtual network. The private link allows you to connect the network interface in the private network to the streaming endpoint in the Media Services account. You'll also be creating DNS zones which pass the private IP addresses.

The virtual network created for this walk-though is just to assist with the example.

- Read about how private endpoints can be applied to Media Services resources.
- Create a Web App using this tutorial: [Connect to a web app using an Azure Private Endpoint](/azure/private-link/tutorial-private-endpoint-webapp-portal). You will be using it to test the connection to the streaming endpoint.

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

## Create a transform and a job

In order to stream media, the video you uploaded needs to be encoded. A transform is an encoding method for the video.

[!INCLUDE [task-create-transform-portal.md](includes/task-create-transform-portal.md)]

## Create a Job

To encode the video, you must create an encoding job, that uses the transform to encode the video.

[!INCLUDE [task-create-job-portal.md](./includes/task-create-job-portal.md)]

## Start the streaming endpoint

1. Navigate to the Media Services account you created.
1. Select **Streaming endpoints** from the menu. The Streaming endpoints screen will appear.
1. Select the default Streaming endpoint that you created when you set up the Media Services account.  The default Streaming endpoint screen will appear.
1. Select **Start**. Start options will appear.
1. Select **None** from the CDN pricing tier dropdown list.
1. Select **Start**.  The Streaming endpoint will start running. The endpoint is still Internet facing.

## Create a private endpoint

1. Navigate back to your Media Services account.
1. Select **Networking** from the menu
1. Select the **private endpoint connections** tab.  The private endpoint connection screen will appear.
1. Select **Add a private endpoint**. The Create a private endpoint screen will appear.
1. In the **Name** field, give the private endpoint a name such as *privatelinkpe*.
1. From the **Region** dropdown list, select a region such as *West US 2*.
1. Select **Next: Resource**. The Resource screen will appear.

## Assign the private endpoint to a resource

1. From the **Connection methods** radio buttons, select the *Connect to an Azure resource in my directory* radio button.
1. From the **Resource type** dropdown list, select *Microsoft.Media/mediaservices*.
1. From the **Resource** dropdown list, select the Media Services account you created.
1. From the **Target sub-resource** dropdown list, select the Streaming endpoint you created.

## Deploy the private endpoint to the virtual network

1. From the **Virtual network** dropdown list, select the virtual network you created.
1. From the **Subnet** dropdown list, select the subnet you want to work with.
1. Stay on this screen.

## Create DNS zones to use with the private endpoint

> [!IMPORTANT]
> Creating a private endpoint **DOES NOT** implicitly disable internet access to it.

To use the streaming endpoint inside your virtual network, create private DNS zones. You can use the same DNS name and get back the private IP address of the streaming endpoint.

1. On the same screen, for the **media-azure-net** configuration, select the resource group you created from the **Resource group** dropdown list.
1. For the **privatelink-media-azure-net** configuration, select the same resource group from the **Resource group** dropdown list.
1. Select **Next: Tags**. If you want to add tags to your resources, do that here.
1. Select **Next: Review + create**. The Review + create screen will appear.
1. Review your settings and make sure they're correct.
1. Select **Create**. The private endpoint deployment screen appears.

While the deployment is in progress, it's also creating an [Azure Resource Manager (ARM) template](/azure/azure-resource-manager/templates/overview). You can use ARM templates to automate deployment. To see the template, select **Template** from the menu.

## Clean up resources

If you aren't planning to use the resources created in this exercise, simply delete the resource group. If you don't delete the resources, you will be charged for them.
