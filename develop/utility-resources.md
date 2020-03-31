---
title: Ressources de l’utilitaire
description: L’API REST de l’espace partenaires contient de nombreuses ressources qui décrivent des modèles de données à usage général utilisés dans le kit de développement logiciel (SDK).
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 50f60dd17faca5f71e309bcc5c656a8ea3c4cf61
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414342"
---
# <a name="utility-resources"></a>Ressources de l’utilitaire


**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’API REST de l’espace partenaires contient de nombreuses ressources qui décrivent des modèles de données à usage général utilisés dans le kit de développement logiciel (SDK).


## <a name="span-idaddressspan-idaddressaddress"></a>Adresse <span id="ADDRESS"/><span id="address"/>

Adresse à utiliser pour le client ou pour les profils de partenaires. Pour plus d’informations sur les formats et les propriétés pris en charge dans les différents pays/régions, consultez [obtenir des règles de mise en forme des adresses par marché](get-market-specific-validation-data.md).

| Propriété     | Type   | Longueur (min, max) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | chaîne | (1, 200)          | Première ligne de l’adresse.                                                                   |
| AddressLine2 | chaîne | (0, 200)          | Deuxième ligne de l’adresse. Cette propriété est facultative.                                       |
| Ville         | chaîne | Non applicable               | Ville.                                                                                        |
| État        | chaîne | (0, 2)            | État.                                                                                       |
| PostalCode   | chaîne | Non applicable               | Code postal.                                                                     |
| Country      | chaîne | (2, 2)            | Pays/région au format de code pays ISO.                                                   |
| Région       | chaîne | Non applicable               | Région                                                                                      |
| Prénom    | chaîne | (1, 50)           | Prénom d’un contact au niveau de la société ou de l’organisation du client.                              |
| LastName     | chaîne | (1, 50)           | Nom d’un contact au niveau de la société ou de l’organisation du client.                               |
| PhoneNumber  | chaîne | Non applicable               | Numéro de téléphone d’un contact au niveau de l’entreprise ou de l’entreprise du client. Cette propriété est facultative. |
 

## <a name="span-idcontactspan-idcontactspan-idcontactcontact"></a><span id="Contact"/><span id="contact"/><span id="CONTACT"/>contact

Décrit les informations de contact d’une personne spécifique.

| Propriété    | Type   | Description                  |
|-------------|--------|------------------------------|
| Prénom   | chaîne | prénom du contact.    |
| LastName    | chaîne | nom du contact.     |
| E-mail       | chaîne | Adresse e-mail du contact. |
| PhoneNumber | chaîne | numéro de téléphone du contact.  |
 

## <a name="span-idfieldfilterspan-idfieldfilterspan-idfieldfilterfieldfilter"></a><span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

Décrit un filtre qui peut être appliqué aux résultats de la recherche.

| Propriété | Type   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Opérateur | chaîne | L’opérateur de filtre : « égal à », « non\_égal », « supérieur\_à », « supérieur\_que\_ou\_égal », « moins\_que « », « moins\_que\_» ou « égal à », « sous-chaîne », « » et «, » ou « , » démarre\_avec « , » et non\_«».\_\_ |
 

## <a name="span-idfileinfospan-idfileinfospan-idfileinfofileinfo"></a><span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

Représente un fichier externe chargé dans l’espace partenaires.

| Propriété                 | Type   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Commentaire                  | chaîne | Commentaire associé au chargement du fichier.    |
| FileExtension            | chaîne | Extension de fichier.                           |
| FileNameWithoutExtension | chaîne | Nom du fichier, extension non inclus. |
| FileSize                 | long   | Taille du fichier.                         |
| ID                       | chaîne | ID unique du chargement du fichier.            |
 

## <a name="span-idlinkspan-idlinkspan-idlinklink"></a><span id="Link"/><span id="link"/><span id="LINK"/>lien

Contient un lien URI et des informations associées.

| Propriété | Type                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | chaîne                 | URI.                           |
| Méthode   | chaîne                 | Méthode représentée par l’URI. |
| En-têtes  | Tableau de KeyValuePair | En-têtes pour le lien.          |
 

## <a name="span-idpasswordprofilespan-idpasswordprofilespan-idpasswordprofilepasswordprofile"></a><span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

Décrit un mot de passe spécifique et si ce mot de passe doit être modifié.

>[!NOTE]
>Non pris en charge dans l’espace partenaires géré par 21Vianet.

| Propriété            | Type                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Password            | [SecureString](#securestring) | Mot de passe.                                                          |
| ForceChangePassword | booléen                       | Détermine si le mot de passe doit être modifié de force lors de la prochaine connexion. |
 

## <a name="span-idresourcelinksspan-idresourcelinksspan-idresourcelinksresourcelinks"></a><span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

Contient une liste de liens pour une ressource.

| Propriété   | Type                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self (Auto)       | [Lien](#link)                             | URI auto.                                      |
| Suivant       | [Lien](#link)                             | Page suivante des éléments.                            |
| Précédent   | [Lien](#link)                             | Page d’éléments précédente.                        |
| Attributs | [ResourceAttributes](#resourceattributes) | Attributs de métadonnées correspondant à l’utilisateur. |
 

## <a name="span-idresourceattributesspan-idresourceattributesspan-idresourceattributesresourceattributes"></a><span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

Contient des métadonnées d’attribut pour une ressource.

| Propriété   | Type   | Description                                 |
|------------|--------|---------------------------------------------|
| ETag       | chaîne | ETag, également appelé version de l’objet. |
| ObjectType | chaîne | Type de l’objet de la ressource de base.    |
 

## <a name="span-idsecurestringspan-idsecurestringspan-idsecurestringsecurestring"></a><span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

Stocke des informations sécurisées, telles qu’un mot de passe.

| Propriété | Type | Description                       |
|----------|------|-----------------------------------|
| Length   | int  | Longueur de la chaîne sécurisée. |


## <a name="span-idvalidationcodespan-idvalidationcodespan-idvalidationcodevalidationcode"></a><span id="ValidationCode"/><span id="validationcode"/><span id="VALIDATIONCODE"/>ValidationCode

Représente le code de validation Cloud de la communauté gouvernementale d’un partenaire.

| Propriété         | Type         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Identificateur du partenaire                                                       |
| OrganizationName | chaîne       | Nom de l’organisation fourni pendant le processus de validation             |
| ValidationId     | int          | Identificateur unique pour la validation                                       |
| MaxCreates       | entier Nullable | Nombre maximal de clients autorisés à créer avec ce code de validation    |
| RemainingCreates | entier Nullable | Le client restant crée sous cet ID de validation                      |
| ETag             | chaîne       | Version spécifique de cette ressource. Change quand la ressource est modifiée. |
