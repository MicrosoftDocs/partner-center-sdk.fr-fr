---
title: Ressources de profil
description: Décrit le comportement des profils d’un fournisseur de solutions Cloud.
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9bd3f5322de7fae9a919e4bcfdd747a6bbc89e80
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82119175"
---
# <a name="profile-resources"></a>Ressources de profil

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit le comportement des profils d’un fournisseur de solutions Cloud.

## <a name="billingprofile"></a>BillingProfile

Décrit le profil de facturation d’un partenaire.

| Propriété            | Type                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | string                                                         | Nom de la société de facturation.                                   |
| address             | [Adresse](utility-resources.md#address)                       | Adresse de facturation de l’entreprise ou de l’organisation. |
| primaryContact      | [Contact](utility-resources.md#contact)                       | Contact principal de l’entreprise ou de l’organisation.        |
| purchaseOrderNumber | string                                                         | Numéro de bon de commande de la société ou de l’organisation.        |
| taxI               | string                                                         | L’ID de taxe de la société ou de l’organisation.                       |
| billingCurrency     | string                                                         | Devise utilisée par la société ou l’organisation.           |
| profileType         | string                                                         | Type de profil du partenaire.                                   |
| liens               | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.            |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Décrit le profil d’entreprise juridique d’un partenaire.

| Propriété               | Type                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | string                                                         | Nom de la société légale.                                                                                                                                              |
| address                | [Adresse](utility-resources.md#address)                       | Adresse de la société ou de l’organisation.                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | Contact principal de l’entreprise ou de l’organisation.                                                                                                                 |
| companyApproverAddress | [Adresse](utility-resources.md#address)                       | Adresse de l’approbateur de l’entreprise.                                                                                                                                        |
| companyApproverEmail   | string                                                         | E-mail de l’approbateur de l’entreprise.                                                                                                                                          |
| vettingStatus          | string                                                         | État d’instruction. Cette valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | string                                                         | Sous-état d’instruction. Cette valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | string                                                         | Type de profil du partenaire.                                                                                                                                            |
| liens                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.                                                                                                                     |
| attributs             | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Décrit le profil de Microsoft Partner Network d’un partenaire.

| Propriété    | Type                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | Nom de la société ou de l’organisation.                     |
| mpnId       | string                                                         | ID de Microsoft Partner Network.                     |
| profileType | string                                                         | Type de profil du partenaire.                             |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.      |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil. |

## <a name="organizationprofile"></a>OrganizationProfile

Décrit le profil d’organisation d’un partenaire.

| Propriété       | Type                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | string                                                         | ID de l’organisation.                                                 |
| companyName    | string                                                         | Nom de la société ou de l’organisation.                               |
| defaultAddress | [Adresse](utility-resources.md#address)                       | Adresse par défaut de la société ou de l’organisation.                    |
| tenantId       | string                                                         | Identificateur du locataire.                                                 |
| domaine         | string                                                         | Domaine de l’entreprise ou de l’organisation.                                  |
| email          | string                                                         | Obtient ou définit l’abonnement parent.                                  |
| langage       | string                                                         | Langue par défaut pour la communication.                              |
| culture        | string                                                         | Culture préférée pour la communication et la devise, par exemple « en-US ». |
| profileType    | string                                                         | Type de profil du partenaire.                                              |
| liens          | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.                       |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                  |

## <a name="supportprofile"></a>SupportProfile

Décrit le profil de support d’un partenaire.

| Propriété    | Type                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| email       | string                                                         | Adresse e-mail associée au profil.        |
| telephone   | string                                                         | Numéro de téléphone associé au profil.         |
| site Web     | string                                                         | Le site Web de support.                                  |
| profileType | string                                                         | Type de profil du partenaire.                             |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.      |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil. |

