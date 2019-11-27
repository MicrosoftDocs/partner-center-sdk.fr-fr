---
title: Ressources des coûts de service
description: Décrit les ressources associées aux services achetés par un client.
ms.assetid: 2916B7F3-06D5-4DC1-A137-CD8270258CDB
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a7d08c740e0a338e1c8b09908b346257f60fe444
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488079"
---
# <a name="service-costs-resources"></a>Ressources des coûts de service

S’applique à :

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
| BillingStartDate | date | Début de la période de facturation. |
| billingEndDate | date | Fin de la période de facturation. |
| pretaxTotal | Double | Total de tous les coûts pour le client. |
| TTC  | Double | Taxe totale imputée sur tous les articles achetés par le client. |
| afterTaxTotal | Double | Coût total net pour tous les articles achetés par le client. |
| currencyCode | chaîne | Représente la devise utilisée pour les coûts. |
| currencySymbol | chaîne | Symbole monétaire utilisé pour les coûts. |
| customerId | chaîne | ID du client effectuant l’achat. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** décrit un récapitulatif des coûts de service qui agrège tous les services achetés par le client spécifié pendant la période de facturation (à partir de factures périodiques ou ponctuelles).

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| invoiceType | chaîne | InvoiceType que le résumé du coût du service a été généré. |
| Tête | [ServiceCostsSummary](#servicecostssummary) | Résumé du coût du service agrégé par un client sous un type de facture. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** décrit un seul élément acheté par le client.

> [!IMPORTANT]
> Les propriétés suivantes *s’appliquent uniquement aux éléments de ligne de* coût du service où le produit est un *achat unique*: **ProductID**, **ProductName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **PublisherName**, **termAndBillingCycle**, **discountDetails**. Ces propriétés *ne s’appliquent pas aux Articles de ligne de* service où le produit est un *achat périodique*. Par exemple, ces propriétés *ne s’appliquent pas* aux Office 365 et Azure basés sur des abonnements.

| Propriété                 | Type                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | chaîne au format date-heure UTC | Date de début des frais.                                       |
| endDate                  | chaîne au format date-heure UTC | Date de fin des frais.                                         |
| subscriptionFriendlyName | chaîne                         | Nom convivial de l’abonnement.                              |
| subscriptionId           | chaîne                         | Identificateur d’abonnement.                                         |
| orderId                  | chaîne                         | Identificateur de l’ordre.                                                |
| offerId                  | chaîne                         | Identificateur de l’offre.                                                |
| offerName                | chaîne                         | Nom de l’offre.                                                      |
| resellerMPNId            | chaîne                         | Utilisé uniquement dans les scénarios de partenaires à deux niveaux. Fait référence à l’identificateur MPN. |
| chargeType               | chaîne                         | Type de frais associé.                                          |
| quantity                 | nombre                         | Quantité d’unités utilisées ou achetées.                             |
| Prix                | nombre                         | Prix unitaire.                                                  |
| pretaxTotal              | nombre                         | Total des frais pour cet article avant les taxes.                         |
| TTC                      | nombre                         | Montant total des frais de taxe engagés pour cet article.                         |
| afterTaxTotal            | nombre                         | Coût total net de cet article.                                    |
| currencyCode             | chaîne                         | Représente la devise utilisée pour les coûts.                          |
| currencySymbol           | chaîne                         | Symbole monétaire utilisé pour les coûts.                              |
| customerId               | chaîne                         | ID du client effectuant l’achat.                          |
| Souhaite             | chaîne                         | Nom du client qui effectue l’achat.                        |
| invoiceNumber            | chaîne                         | Numéro de la facture à laquelle cet article appartient.                   |
| productId                | chaîne                         | Identificateur du produit.                                              |
| skuId                    | chaîne                         | Identificateur de référence (SKU).                                                  |
| availabilityId           | chaîne                         | Identificateur de disponibilité.                                         |
| productName              | chaîne                         | Nom du produit.                                                    |
| skuName                  | chaîne                         | Nom de la référence (SKU).                                                        |
| publisherName            | chaîne                         | Nom de l’éditeur.                                                  |
| PublisherId              | chaîne                         | Identificateur de l’éditeur.                                            |
| termAndBillingCycle      | chaîne                         | Le terme et le cycle de facturation.                                          |
| discountDetails          | chaîne                         | Détails de la remise.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Propriété             | Type                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Lien](utility-resources.md#link) | URI pour récupérer les éléments de ligne. |
| rythme                 | [Lien](utility-resources.md#link) | URI auto.                       |
