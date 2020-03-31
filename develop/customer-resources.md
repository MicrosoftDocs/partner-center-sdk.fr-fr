---
title: Ressources client
description: Ressources client qui représentent un client ou un revendeur.
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 458c2a3d888cadb4d45dd059a3865c8f1f43cc2e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412280"
---
# <a name="customer-resources"></a>Ressources client

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

## <a name="customer"></a>Client

La ressource **client** représente un client ou un revendeur. En règle générale, une ressource client peut être une personne, un employé ou une organisation qui souhaite faire des affaires avec Microsoft et les revendeurs de Microsoft. Les clients disposent également d’un profil d’entreprise et d’un profil de facturation.

>[!NOTE]
>La ressource **client** a une limite de 500 de demandes par minute et par identificateur de locataire.

| Propriété              | Type                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | chaîne                                                           | ID client.                                                                                                                             |
| commerceId            | chaîne                                                           | ID de commerce.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Informations supplémentaires sur l’entreprise ou l’organisation.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Informations supplémentaires utilisées pour la facturation.                                                                                                     |
| relationshipToPartner | chaîne                                                           | Définit le programme de licence que le partenaire utilise pour ce client : « None », « Reseller », « Advisor », « syndication » ou « Microsoft\_support ». |
| allowDelegatedAccess  | booléen                                                          | Si le client a reçu des privilèges d’administrateur délégué par ce client. Cette propriété est disponible uniquement lors de l’obtention d’un client par son ID, et non par liste.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Informations d'identification de l'utilisateur.                                                                                                                        |
| customDomains         | tableau de chaînes                                                 | Liste des domaines personnalisés d’un client.                                                                                                        |
| associatedPartnerId   | chaîne                                                           | Revendeur indirect associé à ce compte client. Cette valeur ne peut être définie que par des partenaires CSP indirects.                              |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Liens de ressources contenus dans le profil.                                                                                             |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Attributs de métadonnées correspondant au profil.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

La ressource **CustomerCompanyProfile** est un complément d’informations sur la société ou l’organisation.

| Propriété    | Type                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | chaîne                                                         | Identificateur de locataire du client pour Azure AD. Elle est également appelée MicrosoftID. |
| domain      | chaîne                                                         | Nom du client, tel que contoso.onmicrosoft.com.                             |
| Prennent | chaîne                                                         | Nom de la société ou de l’organisation.                                          |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressources contenus dans le profil.                                  |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                             |

## <a name="customerbillingprofile"></a>CustomerBillingProfile

La ressource **CustomerBillingProfile** est un complément d’information utilisé pour la facturation du client.

| Propriété       | Type                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | chaîne                                                         | Identificateur du profil.                                                                                                                                |
| firstName      | chaîne                                                         | Prénom du contact de facturation de la société du client. Il s’agit de la personne à laquelle les factures et autres communications de facturation sont dirigées. |
| lastName       | chaîne                                                         | Nom du contact de facturation.                                                                                                                  |
| Messagerie          | chaîne                                                         | Adresse de messagerie du contact de facturation                                                                                                                    |
| culture        | chaîne                                                         | La culture par défaut pour la communication et la monnaie, par exemple « en-US ».                                                                               |
| language       | chaîne                                                         | Leur langue par défaut pour la communication.                                                                                                            |
| Prennent    | chaîne                                                         | Nom de la société ou de l’organisation.                                                                                                               |
| defaultAddress | [Address](utility-resources.md#address)                       | Adresse à laquelle les factures sont envoyées, où le contact de facturation travaille.                                                                                   |
| liens          | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressources contenus dans le profil.                                                                                                       |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

La ressource **CustomerRelationshipRequest** contient l’URL utilisée par le client pour établir une relation de revendeur avec un partenaire.

| Propriété   | Type                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | chaîne                                                         | URL utilisée par le client pour établir une relation avec un partenaire. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à la demande de relation.       |