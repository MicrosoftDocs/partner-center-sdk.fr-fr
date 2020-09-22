---
title: Ressources de profil
description: Décrit le comportement des profils d’un fournisseur de solutions Cloud.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef14eb0307dae0d58dc9903a867ec3bee4ebb323
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925823"
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
| vettingStatus          | string                                                         | État d’instruction. Cette valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans [**VettingStatus**/dotnet/API/Microsoft.Store.partnercenter.Models.Partners.vettingstatus).           |
| vettingSubStatus       | string                                                         | Sous-état d’instruction. Cette valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans [**VettingSubStatus**/dotnet/API/Microsoft.Store.partnercenter.Models.Partners.vettingsubstatus). |
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

