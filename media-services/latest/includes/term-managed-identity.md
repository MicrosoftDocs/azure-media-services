---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 03/25/2022
ms.author: inhenkel
title: Managed Identity
---

**Managed identity** - Managed identities provide an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. There are two types of managed identities:

- **System-assigned**. Some Azure services allow you to enable a managed identity directly on a service instance. When you enable a system-assigned managed identity, an identity is created in Azure AD. The identity is tied to the lifecycle of that service instance. When the resource is deleted, Azure automatically deletes the identity for you. By design, only that Azure resource can use this identity to request tokens from Azure AD.
- **User-assigned**. You may also create a managed identity as a standalone Azure resource. You can create a user-assigned managed identity and assign it to one or more instances of an Azure service. For user-assigned managed identities, the identity is managed separately from the resources that use it.
