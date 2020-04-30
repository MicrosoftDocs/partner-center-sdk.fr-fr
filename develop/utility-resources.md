---
title: Ressources d’utilitaire
description: L’API REST de l’espace partenaires contient de nombreuses ressources qui décrivent des modèles de données à usage général utilisés dans le kit de développement logiciel (SDK).
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0451caae82ec29423ca8c40691d68c9eb2233cc8
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82119285"
---
# <a name="utility-resources"></a>Ressources d’utilitaire

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’API REST de l’espace partenaires contient de nombreuses ressources qui décrivent des modèles de données à usage général utilisés dans le kit de développement logiciel (SDK).

## <a name="address"></a>Adresse

Adresse à utiliser pour le client ou pour les profils de partenaires. Pour plus d’informations sur les formats et les propriétés pris en charge dans les différents pays/régions, consultez [obtenir des règles de mise en forme des adresses par marché](get-market-specific-validation-data.md).

| Propriété     | Type   | Longueur (min, max) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | La première ligne de l’adresse.                                                                   |
| AddressLine2 | string | (0, 200)          | Deuxième ligne de l’adresse. Cette propriété est facultative.                                       |
| City         | string | n/a               | La ville.                                                                                        |
| State        | string | (0, 2)            | État.                                                                                       |
| PostalCode   | string | n/a               | Code postal.                                                                     |
| Country      | string | (2, 2)            | Pays ou région au format de code pays ISO.                                                   |
| Région       | string | n/a               | Région                                                                                      |
| FirstName    | string | (1, 50)           | Prénom d’un contact au niveau de la société ou de l’organisation du client.                              |
| LastName     | string | (1, 50)           | Nom d’un contact au niveau de la société ou de l’organisation du client.                               |
| PhoneNumber  | string | n/a               | Numéro de téléphone d’un contact au niveau de l’entreprise ou de l’entreprise du client. Cette propriété est facultative. |

## <a name="contact"></a>Contact

Décrit les informations de contact d’une personne spécifique.

| Propriété    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | Prénom du contact.    |
| LastName    | string | Nom du contact.     |
| E-mail       | string | adresse e-mail du contact. |
| PhoneNumber | string | Numéro de téléphone du contact.  |

## <a name="fieldfilter"></a>FieldFilter

Décrit un filtre qui peut être appliqué aux résultats de la recherche.

| Propriété | Type   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Opérateur | string | L’opérateur de filtre : « égal à », «\_différent de », « supérieur\_à », « supérieur\_\_ou\_égal à », « inférieur\_à », « inférieur\_à\_ou\_égal à », « sous-chaîne », « et », « ou », « commence\_par « », «\_ne\_commence pas par ». |

## <a name="fileinfo"></a>FileInfo

Représente un fichier externe chargé dans l’espace partenaires.

| Propriété                 | Type   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Commentaire                  | string | Commentaire associé au chargement du fichier.    |
| FileExtension            | string | Extension de fichier.                           |
| FileNameWithoutExtension | string | Nom du fichier, extension non inclus. |
| FileSize                 | long   | Taille du fichier.                         |
| Id                       | string | ID unique du chargement du fichier.            |

## <a name="link"></a>Lien

Contient un lien URI et des informations associées.

| Propriété | Type                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | URI.                           |
| Méthode   | string                 | Méthode représentée par l’URI. |
| headers  | Tableau de KeyValuePair | En-têtes pour le lien.          |

## <a name="passwordprofile"></a>PasswordProfile

Décrit un mot de passe spécifique et si ce mot de passe doit être modifié.

>[!NOTE]
>Non pris en charge dans l’espace partenaires géré par 21Vianet.

| Propriété            | Type                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Mot de passe            | [SecureString](#securestring) | Mot de passe.                                                          |
| ForceChangePassword | boolean                       | Détermine si le mot de passe doit être modifié de force lors de la prochaine connexion. |

## <a name="resourcelinks"></a>ResourceLinks

Contient une liste de liens pour une ressource.

| Propriété   | Type                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Lien](#link)                             | URI auto.                                      |
| Suivant       | [Lien](#link)                             | Page suivante des éléments.                            |
| Previous   | [Lien](#link)                             | Page d’éléments précédente.                        |
| Attributs | [ResourceAttributes](#resourceattributes) | Attributs de métadonnées correspondant à l’utilisateur. |

## <a name="resourceattributes"></a>ResourceAttributes

Contient des métadonnées d’attribut pour une ressource.

| Propriété   | Type   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | string | ETag, également appelé version de l’objet. |
| ObjectType | string | Type de l’objet de la ressource de base.    |

## <a name="securestring"></a>SecureString

Stocke des informations sécurisées, telles qu’un mot de passe.

| Propriété | Type | Description                       |
|----------|------|-----------------------------------|
| Longueur   | int  | Longueur de la chaîne sécurisée. |

## <a name="validationcode"></a>ValidationCode

Représente le code de validation Cloud de la communauté gouvernementale d’un partenaire.

| Propriété         | Type         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Identificateur du partenaire                                                       |
| OrganizationName | string       | Nom de l’organisation fourni pendant le processus de validation             |
| ValidationId     | int          | Identificateur unique pour la validation                                       |
| MaxCreates       | entier Nullable | Nombre maximal de clients autorisés à créer avec ce code de validation    |
| RemainingCreates | entier Nullable | Le client restant crée sous cet ID de validation                      |
| ETag             | string       | Version spécifique de cette ressource. Change quand la ressource est modifiée. |
