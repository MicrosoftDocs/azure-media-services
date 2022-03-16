---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 03/08/2022
ms.author: inhenkel
---

### Set storage authentication in the portal

You can set the authentication type of storage accounts associated with a Media Services account in the portal.

1. Navigate to the Media Services account you want to work with.
1. Select **Storage accounts** from the menu. The Storage accounts screen will appear.
1. Select one of the radio buttons for the Storage authentication type
    1. System authentication
        1. Select the **System authentication** radio button. You don't need to do anything further.
    1. Managed identity authentication. When you select the Manged identity authentication radio button, the portal will look for managed identities already associated with the subscription. If there are no associated managed identities, you will be prompted to configure one. Select **Click here** to configure. The Identity screen will appear.
        1. User-assigned managed identity
            1. Select the **User-assigned** tab.
            1. Select **+ Attach**. The Select user assigned managed identity screen will appear.
            1. Select the subscription you want to work with. A list of user assigned managed identities associated with the chosen subscription will appear.
            1. Select the user assigned managed identity that you want to use from the list.
            1. Select the **Add** button.
        1. System-assigned managed identity
            1. Select the **System-assigned** tab.
                1. Select the **Yes** radio button to enable a system-assigned managed identity.
