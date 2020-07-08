---
title: Ressources des coûts de service
description: Décrit les ressources associées aux services achetés par un client.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0236329d93d8ddc9019a15fb67a81a3af3e7620
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098495"
---
# <a name="service-costs-resources"></a>Ressources des coûts de service

**S’applique à :**

- Espace partenaires

Décrit les ressources associées aux services achetés par un client.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** contient un résumé qui agrège tous les services achetés par le client spécifié pendant la période de facturation.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| details | Tableau d’objets [ServiceCostsSummaryDetail](#servicecostssummarydetail) | Liste détaillée du résumé du coût du service, distingué par le type de facture.|
| liens | [ResourceLinks](utility-resources.md#resourcelinks) | Liens vers les ressources. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. |

> [!IMPORTANT]
> **Les champs du tableau suivant sont déconseillés.** Pour récupérer des résumés des coûts des services récurrents et ponctuels, utilisez le champ **Détails** à la place. Le champ **Détails** est décrit dans le tableau précédent. Reportez-vous aux valeurs de données correspondantes du champ **Détails** , mais pas aux champs de niveau racine.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| billingStartDate | Date | Début de la période de facturation. |
| billingEndDate | Date | Fin de la période de facturation. |
| pretaxTotal | double | Total de tous les coûts pour le client. |
| tax  | double | Taxe totale imputée sur tous les articles achetés par le client. |
| afterTaxTotal | double | Coût total net pour tous les articles achetés par le client. |
| currencyCode | string | Représente la devise utilisée pour les coûts. |
| currencySymbol | string | Symbole monétaire utilisé pour les coûts. |
| customerId | string | ID du client effectuant l’achat. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** décrit un récapitulatif des coûts de service qui agrège tous les services achetés par le client spécifié pendant la période de facturation (à partir de factures périodiques ou ponctuelles).

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| invoiceType | string | InvoiceType que le résumé du coût du service a été généré. |
| summary | [ServiceCostsSummary](#servicecostssummary) | Résumé du coût du service agrégé par un client sous un type de facture. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** décrit un seul élément acheté par le client.

> [!IMPORTANT]
> Les propriétés suivantes *s’appliquent uniquement aux éléments de ligne de* coût du service où le produit est un *achat unique*: **ProductID**, **ProductName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **PublisherName**, **termAndBillingCycle**, **discountDetails**. Ces propriétés *ne s’appliquent pas aux Articles de ligne de* service où le produit est un *achat périodique*. Par exemple, ces propriétés *ne s’appliquent pas* aux Office 365 et Azure basés sur des abonnements.

| Propriété                 | Type                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | chaîne au format date-heure UTC | Date de début des frais.                                       |
| endDate                  | chaîne au format date-heure UTC | Date de fin des frais.                                         |
| subscriptionFriendlyName | string                         | Nom convivial de l’abonnement.                              |
| subscriptionId           | string                         | Identificateur de l’abonnement.                                         |
| orderId                  | string                         | Identificateur de l’ordre.                                                |
| offerId                  | string                         | Identificateur de l’offre.                                                |
| offerName                | string                         | Nom de l’offre.                                                      |
| resellerMPNId            | string                         | Utilisé uniquement dans les scénarios de partenaires à deux niveaux. Fait référence à l’identificateur MPN. |
| chargeType               | string                         | Type de frais associé.                                          |
| quantité                 | nombre                         | Quantité d’unités utilisées ou achetées.                             |
| unitPrice                | nombre                         | Prix unitaire.                                                  |
| pretaxTotal              | nombre                         | Total des frais pour cet article avant les taxes.                         |
| tax                      | nombre                         | Montant total des frais de taxe engagés pour cet article.                         |
| afterTaxTotal            | nombre                         | Coût total net de cet article.                                    |
| currencyCode             | string                         | Représente la devise utilisée pour les coûts.                          |
| currencySymbol           | string                         | Symbole monétaire utilisé pour les coûts.                              |
| customerId               | string                         | ID du client effectuant l’achat.                          |
| customerName             | string                         | Nom du client qui effectue l’achat.                        |
| invoiceNumber            | string                         | Numéro de la facture à laquelle cet article appartient.                   |
| productId                | string                         | Identificateur du produit.                                              |
| skuId                    | string                         | Identificateur de référence (SKU).                                                  |
| availabilityId           | string                         | Identificateur de disponibilité.                                         |
| ProductName              | string                         | Nom du produit.                                                    |
| skuName                  | string                         | Nom de la référence (SKU).                                                        |
| publisherName            | string                         | Nom de l’éditeur.                                                  |
| publisherId              | string                         | Identificateur de l’éditeur.                                            |
| termAndBillingCycle      | string                         | Le terme et le cycle de facturation.                                          |
| discountDetails          | string                         | Détails de la remise.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Propriété             | Type                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Lien](utility-resources.md#link) | URI pour récupérer les éléments de ligne. |
| self                 | [Lien](utility-resources.md#link) | URI auto.                       |
