---
title: Ressources utilisateur
description: Décrit un utilisateur de l’espace partenaires, ses informations personnelles et de compte, ainsi que les autorisations dont il dispose dans l’espace partenaires.
ms.assetid: A2DEDDAB-C4DA-4ECA-931F-2054AB005973
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d3ee186b56ab7553b21e5625579c2a00a50e4492
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414443"
---
# <a name="user-resources"></a>Ressources utilisateur


**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit un utilisateur de l’espace partenaires, ses informations personnelles et de compte, ainsi que les autorisations dont il dispose dans l’espace partenaires.

## <a name="span-iduserspan-iduserspan-iduseruser"></a><span id="User"/><span id="user"/><span id="USER"/>utilisateur


Décrit un utilisateur individuel.

| Propriété              | Type                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | chaîne                                                         | Identificateur de l’utilisateur.                                                                                                                                                                                                       |
| userPrincipalName     | chaîne                                                         | Identificateur du principal de l’utilisateur.                                                                                                                                                                                             |
| firstName             | chaîne                                                         | Prénom de l’utilisateur.                                                                                                                                                                                                |
| lastName              | chaîne                                                         | Nom de l’utilisateur.                                                                                                                                                                                                 |
| displayName           | chaîne                                                         | Nom affiché de l’utilisateur.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Le profil de mot de passe de l’utilisateur.                                                                                                                                                                                               |
| phoneNumber           | chaîne                                                         | numéro de téléphone de l'utilisateur.                                                                                                                                                                                                   |
| lastDirectorySyncTime | Chaîne au format date/heure UTC                                 | La dernière fois que les informations de cet utilisateur ont été synchronisées entre Azure Active Directory et les Active Directory locales. Une valeur de date et d’heure apparaît uniquement si Azure AD Connect synchronisation est activée. Dans le cas contraire, la valeur est null. |
| userDomainType        | chaîne                                                         | Le type de domaine utilisateur : « None », « Managed » ou « Federated ».                                                                                                                                                                   |
| state                 | chaîne                                                         | État de l’utilisateur : « actif », « inactif » (pour un utilisateur supprimé).                                                                                                                                                          |
| softDeletionTime      | Chaîne au format date/heure UTC                                 | Représente le début de la période de trente jours après laquelle les données associées à un utilisateur supprimé sont définitivement supprimées et, par conséquent, irrécupérables.                                                                          |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens vers les ressources.                                                                                                                                                                                                        |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                                                                                                   |

 

## <a name="span-idcustomeruserspan-idcustomeruserspan-idcustomerusercustomeruser"></a><span id="CustomerUser"/><span id="customeruser"/><span id="CUSTOMERUSER"/>CustomerUser


Décrit un utilisateur client.

| Propriété              | Type                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | chaîne                                                         | Emplacement où l’utilisateur a l’intention d’utiliser la licence.                                                                                                                                                                    |
| id                    | chaîne                                                         | Identificateur de l’utilisateur.                                                                                                                                                                                                       |
| userPrincipalName     | chaîne                                                         | Identificateur du principal de l’utilisateur.                                                                                                                                                                                             |
| firstName             | chaîne                                                         | Prénom de l’utilisateur.                                                                                                                                                                                                |
| lastName              | chaîne                                                         | Nom de l’utilisateur.                                                                                                                                                                                                 |
| displayName           | chaîne                                                         | Nom affiché de l’utilisateur.                                                                                                                                                                                            |
| immutableId           | chaîne                                                         | ID immuable de l’utilisateur.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Le profil de mot de passe de l’utilisateur.                                                                                                                                                                                               |
| phoneNumber           | chaîne                                                         | numéro de téléphone de l'utilisateur.                                                                                                                                                                                                   |
| lastDirectorySyncTime | Chaîne au format date/heure UTC                                 | La dernière fois que les informations de cet utilisateur ont été synchronisées entre Azure Active Directory et les Active Directory locales. Une valeur de date et d’heure apparaît uniquement si Azure AD Connect synchronisation est activée. Dans le cas contraire, la valeur est null. |
| userDomainType        | chaîne                                                         | Le type de domaine utilisateur : « None », « Managed » ou « Federated ».                                                                                                                                                                   |
| state                 | chaîne                                                         | État de l’utilisateur : « actif », « inactif » (pour un utilisateur supprimé).                                                                                                                                                          |
| softDeletionTime      | Chaîne au format date/heure UTC                                 | Représente le début de la période de trente jours après laquelle les données associées à un utilisateur supprimé sont définitivement supprimées et, par conséquent, irrécupérables.                                                                          |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens vers les ressources.                                                                                                                                                                                                        |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                                                                                                   |

 

## <a name="span-idusercredentialsspan-idusercredentialsspan-idusercredentialsusercredentials"></a><span id="UserCredentials"/><span id="usercredentials"/><span id="USERCREDENTIALS"/>UserCredentials


Décrit les informations d’identification de connexion d’un utilisateur.

| Propriété | Type                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | chaîne                                             | Le nom de l'utilisateur.                |
| mot de passe | [SecureString](utility-resources.md#securestring) | Mot de passe stocké en toute sécurité de l’utilisateur. |

 

## <a name="span-idusermemberspan-idusermemberspan-idusermemberusermember"></a><span id="UserMember"/><span id="usermember"/><span id="USERMEMBER"/>UserMember


Décrit les informations sur les membres d’un utilisateur.

| Propriété          | Type                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | chaîne                                                         | Nom affiché pour l’utilisateur.   |
| userPrincipalName | chaîne                                                         | Nom du principal d’utilisateur.    |
| roleId            | chaîne                                                         | Identificateur du rôle de l’utilisateur. |
| id                | chaîne                                                         | Identificateur du membre.      |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.           |

 

 

 




