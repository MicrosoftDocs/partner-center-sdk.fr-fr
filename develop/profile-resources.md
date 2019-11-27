---
title: Ressources de profil
description: Décrit le comportement des profils d’un fournisseur de solutions Cloud.
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3449aeb3695a9f286f37668d3f0862dc7b5cfa9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486759"
---
# <a name="profile-resources"></a>Ressources de profil


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit le comportement des profils d’un fournisseur de solutions Cloud.

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>BillingProfile


Décrit le profil de facturation d’un partenaire.

| Propriété            | Type                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| Prennent         | chaîne                                                         | Nom de la société de facturation.                                   |
| adresse             | [-](utility-resources.md#address)                       | Adresse de facturation de l’entreprise ou de l’organisation. |
| PrimaryContact      | [Communiquer](utility-resources.md#contact)                       | Contact principal de l’entreprise ou de l’organisation.        |
| purchaseOrderNumber | chaîne                                                         | Numéro de bon de commande de la société ou de l’organisation.        |
| taxI               | chaîne                                                         | L’ID de taxe de la société ou de l’organisation.                       |
| billingCurrency     | chaîne                                                         | Devise utilisée par la société ou l’organisation.           |
| profileType         | chaîne                                                         | Type de profil du partenaire.                                   |
| liens               | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.            |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


Décrit le profil d’entreprise juridique d’un partenaire.

| Propriété               | Type                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Prennent            | chaîne                                                         | Nom de la société légale.                                                                                                                                              |
| adresse                | [-](utility-resources.md#address)                       | Adresse de la société ou de l’organisation.                                                                                                                          |
| PrimaryContact         | [Communiquer](utility-resources.md#contact)                       | Contact principal de l’entreprise ou de l’organisation.                                                                                                                 |
| companyApproverAddress | [-](utility-resources.md#address)                       | Adresse de l’approbateur de l’entreprise.                                                                                                                                        |
| companyApproverEmail   | chaîne                                                         | E-mail de l’approbateur de l’entreprise.                                                                                                                                          |
| vettingStatus          | chaîne                                                         | État d’instruction. Cette valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | chaîne                                                         | Sous-état d’instruction. Cette valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | chaîne                                                         | Type de profil du partenaire.                                                                                                                                            |
| liens                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.                                                                                                                     |
| attributs             | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


Décrit le profil de Microsoft Partner Network d’un partenaire.

| Propriété    | Type                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | chaîne                                                         | Nom de la société ou de l’organisation.                     |
| mpnId       | chaîne                                                         | ID de Microsoft Partner Network.                     |
| profileType | chaîne                                                         | Type de profil du partenaire.                             |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.      |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil. |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>OrganizationProfile


Décrit le profil d’organisation d’un partenaire.

| Propriété       | Type                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | chaîne                                                         | ID de l’organisation.                                                 |
| Prennent    | chaîne                                                         | Nom de la société ou de l’organisation.                               |
| defaultAddress | [-](utility-resources.md#address)                       | Adresse par défaut de la société ou de l’organisation.                    |
| tenantId       | chaîne                                                         | Identificateur du locataire.                                                 |
| domain         | chaîne                                                         | Domaine de l’entreprise ou de l’organisation.                                  |
| Messagerie          | chaîne                                                         | Obtient ou définit l’abonnement parent.                                  |
| language       | chaîne                                                         | Langue par défaut pour la communication.                              |
| Culturel        | chaîne                                                         | Culture préférée pour la communication et la devise, par exemple « en-US ». |
| profileType    | chaîne                                                         | Type de profil du partenaire.                                              |
| liens          | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.                       |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil.                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


Décrit le profil de support d’un partenaire.

| Propriété    | Type                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| Messagerie       | chaîne                                                         | Adresse e-mail associée au profil.        |
| téléphone   | chaîne                                                         | Numéro de téléphone associé au profil.         |
| site Web     | chaîne                                                         | Le site Web de support.                                  |
| profileType | chaîne                                                         | Type de profil du partenaire.                             |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant au profil.      |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant au profil. |

 

 

 




