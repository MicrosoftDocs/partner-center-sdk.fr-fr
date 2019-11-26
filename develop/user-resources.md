---
title: User resources
description: Describes an individual Partner Center user, their personal and account information, and the permissions they have within Partner Center.
ms.assetid: A2DEDDAB-C4DA-4ECA-931F-2054AB005973
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: edce4bb1b13550445b49979dd59b2bce0486e7fd
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486259"
---
# <a name="user-resources"></a>User resources


**Applies To**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Describes an individual Partner Center user, their personal and account information, and the permissions they have within Partner Center.

## <a name="span-iduserspan-iduserspan-iduseruser"></a><span id="User"/><span id="user"/><span id="USER"/>User


Describes an individual user.

| Propriété              | Tapez                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | chaîne                                                         | The user identifier.                                                                                                                                                                                                       |
| userPrincipalName     | chaîne                                                         | The user principal identifier.                                                                                                                                                                                             |
| firstName             | chaîne                                                         | The first name of the user.                                                                                                                                                                                                |
| lastName              | chaîne                                                         | The last name of the user.                                                                                                                                                                                                 |
| displayName           | chaîne                                                         | The displayed name of the user.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | The user's password profile.                                                                                                                                                                                               |
| phoneNumber           | chaîne                                                         | The user's phone number.                                                                                                                                                                                                   |
| lastDirectorySyncTime | string in UTC date time format                                 | The last time that information for this user was synced between Azure Active Directory and on-premises Active Directory. A date time value only appears if Azure AD Connect sync is enabled. Otherwise, the value is null. |
| userDomainType        | chaîne                                                         | The user domain type: "none", "managed," or "federated".                                                                                                                                                                   |
| state                 | chaîne                                                         | The state of the user: "active", "inactive" (for a deleted user).                                                                                                                                                          |
| softDeletionTime      | string in UTC date time format                                 | Represents the start of the thirty day period after which data associated with a deleted user is permanently deleted and therefore unrecoverable.                                                                          |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                                        |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                                                   |

 

## <a name="span-idcustomeruserspan-idcustomeruserspan-idcustomerusercustomeruser"></a><span id="CustomerUser"/><span id="customeruser"/><span id="CUSTOMERUSER"/>CustomerUser


Describes a customer user.

| Propriété              | Tapez                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | chaîne                                                         | The location where the user intends to use the license.                                                                                                                                                                    |
| id                    | chaîne                                                         | The user identifier.                                                                                                                                                                                                       |
| userPrincipalName     | chaîne                                                         | The user principal identifier.                                                                                                                                                                                             |
| firstName             | chaîne                                                         | The first name of the user.                                                                                                                                                                                                |
| lastName              | chaîne                                                         | The last name of the user.                                                                                                                                                                                                 |
| displayName           | chaîne                                                         | The displayed name of the user.                                                                                                                                                                                            |
| immutableId           | chaîne                                                         | The immutable id of the user.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | The user's password profile.                                                                                                                                                                                               |
| phoneNumber           | chaîne                                                         | The user's phone number.                                                                                                                                                                                                   |
| lastDirectorySyncTime | string in UTC date time format                                 | The last time that information for this user was synced between Azure Active Directory and on-premises Active Directory. A date time value only appears if Azure AD Connect sync is enabled. Otherwise, the value is null. |
| userDomainType        | chaîne                                                         | The user domain type: "none", "managed," or "federated".                                                                                                                                                                   |
| state                 | chaîne                                                         | The state of the user: "active", "inactive" (for a deleted user).                                                                                                                                                          |
| softDeletionTime      | string in UTC date time format                                 | Represents the start of the thirty day period after which data associated with a deleted user is permanently deleted and therefore unrecoverable.                                                                          |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                                        |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                                                   |

 

## <a name="span-idusercredentialsspan-idusercredentialsspan-idusercredentialsusercredentials"></a><span id="UserCredentials"/><span id="usercredentials"/><span id="USERCREDENTIALS"/>UserCredentials


Describes a user's login credentials.

| Propriété | Tapez                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | chaîne                                             | Le nom de l'utilisateur.                |
| password | [SecureString](utility-resources.md#securestring) | The user's securely stored password. |

 

## <a name="span-idusermemberspan-idusermemberspan-idusermemberusermember"></a><span id="UserMember"/><span id="usermember"/><span id="USERMEMBER"/>UserMember


Describes a user's member information.

| Propriété          | Tapez                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | chaîne                                                         | The displayed name for the user.   |
| userPrincipalName | chaîne                                                         | The name of the user principal.    |
| roleId            | chaîne                                                         | The identifier of the user's role. |
| id                | chaîne                                                         | The identifier of the member.      |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.           |

 

 

 




