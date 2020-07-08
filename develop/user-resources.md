---
title: Ressources utilisateur
description: Décrit un utilisateur de l’espace partenaires, ses informations personnelles et de compte, ainsi que les autorisations dont il dispose dans l’espace partenaires.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093546"
---
# <a name="user-resources"></a>Ressources utilisateur

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit un utilisateur de l’espace partenaires, ses informations personnelles et de compte, ainsi que les autorisations dont il dispose dans l’espace partenaires.

## <a name="user"></a>Utilisateur

Décrit un utilisateur individuel.

| Propriété              | Type                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                         | Identificateur de l’utilisateur.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Identificateur du principal de l’utilisateur.                                                                                                                                                                                             |
| firstName             | string                                                         | Prénom de l’utilisateur.                                                                                                                                                                                                |
| lastName              | string                                                         | Nom de l’utilisateur.                                                                                                                                                                                                 |
| displayName           | string                                                         | Nom affiché de l’utilisateur.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Le profil de mot de passe de l’utilisateur.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | numéro de téléphone de l'utilisateur.                                                                                                                                                                                                   |
| lastDirectorySyncTime | Chaîne au format date/heure UTC                                 | La dernière fois que les informations de cet utilisateur ont été synchronisées entre Azure Active Directory et les Active Directory locales. Une valeur de date et d’heure apparaît uniquement si Azure AD Connect synchronisation est activée. Dans le cas contraire, la valeur est null. |
| userDomainType        | string                                                         | Le type de domaine utilisateur : « None », « Managed » ou « Federated ».                                                                                                                                                                   |
| state                 | string                                                         | État de l’utilisateur : « actif », « inactif » (pour un utilisateur supprimé).                                                                                                                                                          |
| softDeletionTime      | Chaîne au format date/heure UTC                                 | Représente le début de la période de trente jours après laquelle les données associées à un utilisateur supprimé sont définitivement supprimées et, par conséquent, irrécupérables.                                                                          |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens vers les ressources.                                                                                                                                                                                                        |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Décrit un utilisateur client.

| Propriété              | Type                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | Emplacement où l’utilisateur a l’intention d’utiliser la licence.                                                                                                                                                                    |
| id                    | string                                                         | Identificateur de l’utilisateur.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Identificateur du principal de l’utilisateur.                                                                                                                                                                                             |
| firstName             | string                                                         | Prénom de l’utilisateur.                                                                                                                                                                                                |
| lastName              | string                                                         | Nom de l’utilisateur.                                                                                                                                                                                                 |
| displayName           | string                                                         | Nom affiché de l’utilisateur.                                                                                                                                                                                            |
| ImmutableID           | string                                                         | ID immuable de l’utilisateur.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Le profil de mot de passe de l’utilisateur.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | numéro de téléphone de l'utilisateur.                                                                                                                                                                                                   |
| lastDirectorySyncTime | Chaîne au format date/heure UTC                                 | La dernière fois que les informations de cet utilisateur ont été synchronisées entre Azure Active Directory et les Active Directory locales. Une valeur de date et d’heure apparaît uniquement si Azure AD Connect synchronisation est activée. Dans le cas contraire, la valeur est null. |
| userDomainType        | string                                                         | Le type de domaine utilisateur : « None », « Managed » ou « Federated ».                                                                                                                                                                   |
| state                 | string                                                         | État de l’utilisateur : « actif », « inactif » (pour un utilisateur supprimé).                                                                                                                                                          |
| softDeletionTime      | Chaîne au format date/heure UTC                                 | Représente le début de la période de trente jours après laquelle les données associées à un utilisateur supprimé sont définitivement supprimées et, par conséquent, irrécupérables.                                                                          |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens vers les ressources.                                                                                                                                                                                                        |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Décrit les informations d’identification de connexion d’un utilisateur.

| Propriété | Type                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | string                                             | Nom de l'utilisateur.                |
| mot de passe | [SecureString](utility-resources.md#securestring) | Mot de passe stocké en toute sécurité de l’utilisateur. |

## <a name="usermember"></a>UserMember

Décrit les informations sur les membres d’un utilisateur.

| Propriété          | Type                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | string                                                         | Nom affiché pour l’utilisateur.   |
| userPrincipalName | string                                                         | Nom d’utilisateur principal.    |
| roleId            | string                                                         | Identificateur du rôle de l’utilisateur. |
| id                | string                                                         | Identificateur du membre.      |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.           |

