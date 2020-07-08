---
title: Vitrine web des clients fournisseurs de solutions cloud
description: Cet exemple de code de site Web montre un magasin en ligne opérationnel permettant aux clients d’acheter des abonnements aux produits Microsoft.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094334"
---
# <a name="csp-customer-web-storefront"></a>Vitrine web des clients fournisseurs de solutions cloud

**S’applique à :**

- Espace partenaires

> [!NOTE]
> Cet exemple d’application s’applique uniquement à l’instance globale de l’espace partenaires. Elle ne s’applique pas à l’espace partenaires pour Microsoft Cloud Allemagne ni au centre partenaires pour Microsoft Cloud pour le gouvernement des États-Unis.

La [vitrine espace partenaires](https://github.com/Microsoft/Partner-Center-Storefront) est un **exemple de site Web** pour un magasin en ligne que les clients peuvent utiliser pour acheter des abonnements aux produits Microsoft. Vous pouvez modifier cet **exemple de code** pour votre usage personnel pour [configurer les offres](#configure-offers), [Ajouter une personnalisation](#configure-branding) et [Ajouter un moyen de paiement](#configure-payment-types).

## <a name="sample-code"></a>Exemple de code

Téléchargez l’exemple de code de la boutique de l' [espace partenaires](https://github.com/Microsoft/Partner-Center-Storefront) à partir de github.

## <a name="configure-authentication"></a>configurer l’authentification ;

Avant de générer l’application, mettez à jour les valeurs suivantes dans le fichier Web.config pour refléter les informations d’authentification Azure AD que vous avez créées dans l’authentification de l' [espace partenaires](partner-center-authentication.md). Vous devez utiliser les paramètres de votre compte sandbox d’intégration lors du développement anticipé ou pour les tests en production (Conseil).

- **partnerCenter. applicationId**
- **partnerCenter. Applicationsecret :**
- **partnerCenter. domaine**
- **Webportal. clientId**
- **Webportal. clientSecret**
- **webportage. domaine**
- **Webportal. azureStorageConnectionString**

## <a name="configure-offers"></a>Configurer des offres

Vous pouvez configurer l’ensemble des offres (**MicrosoftOffer**) dans **OfferCatalogViewModel**.

## <a name="configure-branding"></a>Configurer la personnalisation

Cet exemple de site Web effectue le suivi des informations de la société et de la personnalisation suivantes dans *BrandingConfiguration.cs* et *PortalBranding.cs*:

- Nom de l'organisation
- Logo de l’Organisation
- Image d'en-tête
- Accord de confidentialité
- E-mail de contact
- Numéro de téléphone du contact
- E-mail de support
- Numéro de téléphone du support

### <a name="configure-payment-types"></a>Configurer les types de paiement

L’application utilise actuellement une passerelle PayPal, implémentée dans *PayPalGateway.cs*.