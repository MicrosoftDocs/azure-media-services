---
title: Role-based access control for Media Services accounts
description: This article discusses Azure role-based access control (Azure RBAC) for Azure Media Services accounts.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 3/16/2022
ms.author: inhenkel
---

# Azure role-based access control (Azure RBAC) for Media Services accounts

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Currently, Azure Media Services does not define any custom roles specific to the service. To get full access to the Media Services account, customers can use the built-in roles of **Owner** or **Contributor**. The main difference between these roles is: the **Owner** can control who has access to a resource and the **Contributor** cannot. The built-in **Reader** role can also be used but the user or application will only have read access to the Media Services APIs.

## Design principles

One of the key design principles of the v3 API is to make the API more secure. v3 APIs do not return secrets or credentials on **Get** or **List** operations. The keys are always null, empty, or sanitized from the response. The user needs to call a separate action method to get secrets or credentials. The **Reader** role cannot call operations like Asset.ListContainerSas, StreamingLocator.ListContentKeys, ContentKeyPolicies.GetPolicyPropertiesWithSecrets. Having separate actions enables you to set more granular Azure RBAC security permissions in a custom role if desired.

To list the operations Media Services supports, do:

```csharp
foreach (Microsoft.Azure.Management.Media.Models.Operation a in client.Operations.List())
{
    Console.WriteLine($"{a.Name} - {a.Display.Operation} - {a.Display.Description}");
}
```

The [built-in role definitions](/azure/role-based-access-control/built-in-roles) article tells you exactly what the role grants.

See the following articles for more information:

- [Classic subscription administrator roles, Azure roles, and Azure AD roles](/azure/role-based-access-controle/rbac-and-directory-admin-roles)
- [What is Azure role-based access control (Azure RBAC)?](/azure/role-based-access-controle/overview)
- [Add or remove Azure role assignments using the REST API](/azure/role-based-access-controle/role-assignments-rest)
- [Media Services resource provider operations](/azure/role-based-access-control/resource-provider-operations#microsoftmedia)
