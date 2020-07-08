---
title: Ressources client
description: Ressources client qui représentent un client ou un revendeur.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: edfde5a11d22460f30f2fc39a27341ce28eed9c1
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094305"
---
# <a name="customer-resources"></a>Ressources client

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

## <a name="customer"></a>Customer

La ressource **client** représente un client ou un revendeur. En règle générale, une ressource client peut être une personne, un employé ou une organisation qui souhaite faire des affaires avec Microsoft et les revendeurs de Microsoft. Les clients disposent également d’un profil d’entreprise et d’un profil de facturation.

>[!NOTE]
>La ressource **client** a une limite de 500 de demandes par minute et par identificateur de locataire.

| Propriété              | Type                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                           | ID du client.                                                                                                                             |
| commerceId            | string                                                           | ID de commerce.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Informations supplémentaires sur l’entreprise ou l’organisation.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Informations supplémentaires utilisées pour la facturation.                                                                                                     |
| relationshipToPartner | string                                                           | Définit le programme de licence que le partenaire utilise pour ce client : « None », « Reseller », « Advisor », « syndication » ou « support Microsoft \_ ». |
| allowDelegatedAccess  | boolean                                                          | Si le client a reçu des privilèges d’administrateur délégué par ce client. Cette propriété est disponible uniquement lors de l’obtention d’un client par son ID, et non par liste.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Informations d'identification de l'utilisateur.                                                                                                                        |
| customDomains         | tableau de chaînes                                                 | Liste des domaines personnalisés d’un client.                                                                                                        |
| associatedPartnerId   | string                                                           | Revendeur indirect associé à ce compte client. Cette valeur ne peut être définie que par des partenaires CSP indirects.                              |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Liens de ressources contenus dans le profil.                                                                                             |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Attributs de métadonnées correspondant au profil.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

La ressource **CustomerCompanyProfile** est un complément d’informations sur la société ou l’organisation.

| Propriété    | Type                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | string                                                         | Identificateur de locataire du client pour Azure AD. Elle est également appelée MicrosoftID. |
| domaine      | string                                                         | Nom du client, tel que contoso.onmicrosoft.com.                             |
| companyName | string                                                         | Nom de la société ou de l’organisation.                                          |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressources contenus dans le profil.                                  |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                             |

## <a name="customerbillingprofile"></a>CustomerBillingProfile

La ressource **CustomerBillingProfile** est un complément d’information utilisé pour la facturation du client.

| Propriété       | Type                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | string                                                         | Identificateur du profil.                                                                                                                                |
| firstName      | string                                                         | Prénom du contact de facturation de la société du client. Il s’agit de la personne à laquelle les factures et autres communications de facturation sont dirigées. |
| lastName       | string                                                         | Nom du contact de facturation.                                                                                                                  |
| email          | string                                                         | Adresse de messagerie du contact de facturation                                                                                                                    |
| culture        | string                                                         | La culture par défaut pour la communication et la monnaie, par exemple « en-US ».                                                                               |
| langage       | string                                                         | Leur langue par défaut pour la communication.                                                                                                            |
| companyName    | string                                                         | Nom de la société ou de l’organisation.                                                                                                               |
| defaultAddress | [Adresse](utility-resources.md#address)                       | Adresse à laquelle les factures sont envoyées, où le contact de facturation travaille.                                                                                   |
| liens          | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressources contenus dans le profil.                                                                                                       |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

La ressource **CustomerRelationshipRequest** contient l’URL utilisée par le client pour établir une relation de revendeur avec un partenaire.

| Propriété   | Type                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | string                                                         | URL utilisée par le client pour établir une relation avec un partenaire. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à la demande de relation.       |