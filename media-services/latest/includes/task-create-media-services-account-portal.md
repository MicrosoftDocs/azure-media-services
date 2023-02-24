---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 02/24/2023
ms.author: inhenkel

---

<!-- Use the portal to create a media services account. -->

### Create a Media Services account with the portal

1. Sign in at the [Azure portal](https://portal.azure.com/).
1. Select **+Create a resource**.
1. In the search field, enter "Media Services" and select **Enter**. Search results will appear including a card for Media Services.
1. Select the **Media Services** card. The Media Services detail screen will appear.
1. Select **Create**. The Create a Media Services account screen will appear.
1. In the **Create a Media Services account** section enter required values.

    | Name | Description |
    | ---|---|
    |**Account Name**|Enter the name of the new Media Services account. A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.|
    |**Subscription**|If you have more than one subscription, select one from the list of Azure subscriptions that you have access to.|
    |**Resource Group**|Select the new or existing resource. A resource group is a collection of resources that share lifecycle, permissions, and policies. Learn more [here](/azure/azure-resource-manager/management/overview#resource-groups).|
    |**Location**|Select the geographic region that will be used to store the media and metadata records for your Media Services account. This  region will be used to process and stream your media. Only the available Media Services regions appear in the drop-down list box. |
    |**Storage Account**|Select a storage account to provide blob storage of the media content from your Media Services account. You can select an existing storage account in the same geographic region as your Media Services account, or you can create a new storage account. A new storage account is created in the same region. The rules for storage account names are the same as for Media Services accounts.<br/><br/>You must have one **Primary** storage account and you can have any number of **Secondary** storage accounts associated with your Media Services account. You can use the Azure portal to add secondary storage accounts. For more information, see [Azure Storage accounts with Azure Media Services accounts](../storage-account-concept.md).<br/><br/>The Media Services account and all associated storage accounts must be in the same Azure subscription. It is strongly recommended to use storage accounts in the same location as the Media Services account to avoid additional latency and data egress costs.|
    | **Advanced settings** | Select a previously created user managed identity from the dropdown list or create a new user managed identity by selecting the link. |

    > [!IMPORTANT]
    > All **new** Media Services accounts require a user-managed identity. Previously created accounts that have a system-managed identity have not changed.

1. Select the checkbox next to "I have all the rights to use the content/file, and agree that it will be handled per the Online Services Terms and the Microsoft Privacy Statement." to confirm and continue.
1. Click **Review + create** or add tags with the **Next:Tags** button.
1. Click **Create** on the following screen. Deployment will begin.
