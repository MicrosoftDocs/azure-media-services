---
author: IngridAtMicrosoft
ms.service: media-services 
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
---

### Create a content key policy in the portal

1. Navigate to the Media Services account you want to work with.
1. Select **Content key policy** from the menu. The Content key policies screen will appear.
1. Select **+ Add content key policy**. The Create content key policy screen will appear.
1. Enter a name in the **Content key policy name** field.
1. Optionally, give the content key policy a description in the **Description** field.

#### Digital rights management (DRM) settings

1. In the Digital rights management (DRM) section of the screen select one of the following from the **+ Add** dropdown list.
    1. **+ Add Widevine** to add a content key policy for Widevine. The Add a Widevine policy option screen will appear.
        1. Enter the policy option name in the **Policy option name** field.
        1. In the Restriction tab, select the **No** radio button if you want to allow access without a token.
        1. Select the **Yes** radio button if you want to use token restriction issued by a security token service (STS).
            1. Select the token type from the **TokenType** dropdown list.  Your options are JWT or SWT.
            1. Enter the issuer in the **Issuer** field.
            1. Enter the audience in the **Audience** field.
            1. Enter the primary verification key in the **Primary verification key** field. You can leave this empty to generate a primary key.
            1. You can also add custom claim name value pairs if you want in the **Name** and **Value** fields for Custom Claims.
        1. Select the license setting tab and enter the Widevine JSON for the license settings.  Alternatively, you can load a sample template and edit it by selecting **Load sample template**.
        1. Select the **Add** button.
    1. **+ Add FairPlay** to add a content key policy for FairPlay. The Add a FairPlay policy option screen will appear.
        1. Enter the policy option name in the **Policy option name** field.
        1. In the Restriction tab, select the **No** radio button if you want to allow access without a token.
        1. Select the **Yes** radio button if you want to use token restriction issued by a security token service (STS).
            1. Select the token type from the **TokenType** dropdown list.  Your options are JWT or SWT.
            1. Enter the issuer in the **Issuer** field.
            1. Enter the audience in the **Audience** field.
            1. Enter the primary verification key in the **Primary verification key** field. You can leave this empty to generate a primary key.
            1. You can also add custom claim name value pairs if you want in the **Name** and **Value** fields for Custom Claims.
        1. Select the **Apple requirements** tab.
            1. Select **Update** to upload a FairPlay certificate. (Known bug in the UI.)
            1. Drag and drop files your browse for files to upload the certificate.
            1. Enter the FairPlay certificate password.
            1. Enter the FairPlay secret key.
            1. Select the **Add** button.
    1. **+ Add PlayReady** to add a content key policy for PlayReady. The Add a PlayReady policy option screen will appear.
        1. Enter the policy option name in the **Policy option name** field.
        1. In the Restriction tab, select the **No** radio button if you want to allow access without a token.
        1. Select the **Yes** radio button if you want to use token restriction issued by a security token service (STS).
            1. Select the token type from the **TokenType** dropdown list.  Your options are JWT or SWT.
            1. Enter the issuer in the **Issuer** field.
            1. Enter the audience in the **Audience** field.
            1. Enter the primary verification key in the **Primary verification key** field. You can leave this empty to generate a primary key.
            1. You can also add custom claim name value pairs if you want in the **Name** and **Value** fields for Custom Claims.
        1. Select the **License settings** tab. From the License type selections:
            1. Select **Non-persistent**, if you want the license held only in memorey while the player uses the license, and not stored.  It is for online playback only.
            1. Select **Persistent**, if you want to save the license on the client and use it for offline playback.
                1. You can set the start time, end time, first play expiration, and grace period.

### AES clear key settings

1. In the AES clear key section of the screen, select **+ Add**. The Add AES clear key policy option screen will appear.
1. Enter a policy option name in the **Policy option name** field.
1. Under Token requirements, select the **No** radio button if you want to allow access without a token.
1. Select the **Yes** radio button if you want to use token restriction issued by a security token service (STS).
    1. Select the token type from the **TokenType** dropdown list.  Your options are JWT or SWT.
    1. Enter the issuer in the **Issuer** field.
    1. Enter the audience in the **Audience** field.
    1. Enter the primary verification key in the **Primary verification key** field. You can leave this empty to generate a primary key.
    1. You can also add custom claim name value pairs if you want in the **Name** and **Value** fields for Custom Claims.
