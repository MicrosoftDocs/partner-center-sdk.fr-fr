---
title: Ressources de facturation
description: Plusieurs ressources liées aux factures sont disponibles par le biais des API de l’espace partenaires. Ces ressources sont liées aux détails des factures et des articles.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd2caefe4ae18c81a31083d084f1e87da1288dd9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095125"
---
# <a name="invoice-resources"></a>Ressources de facturation

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les ressources liées aux factures suivantes sont disponibles via les API de l’espace partenaires.

## <a name="invoice"></a>Facture

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| id | string | Identificateur de la facture. |
| invoiceDate | chaîne au format date-heure UTC | Date à laquelle la facture a été générée. |
| billingPeriodStartDate | chaîne au format date-heure UTC | Date de début de la période de facturation en heure UTC. |
| billingPeriodEndDate | chaîne au format date-heure UTC   | Date de fin de la période de facturation en heure UTC. |
| totalCharges | nombre | Total des frais. Comprend les frais liés aux transactions et les ajustements éventuels.     |
| paidAmount | nombre  | Montant payé par le partenaire. Négatif si un paiement a été reçu.  |
| currencyCode | string  | Code qui indique la devise utilisée pour tous les montants et totaux des factures. |
| currencySymbol  | string | Symbole monétaire utilisé pour tous les montants et totaux des factures. |
| pdfDownloadLink | string  | Un lien pour télécharger la facture au format PDF. Ce lien n’est pas renvoyé dans les résultats de la recherche et est rempli uniquement si la facture est accessible par ID. Ce lien expire automatiquement dans 30 minutes. |
| invoiceDetails  | Tableau d’objets [InvoiceDetail](#invoicedetail)  | Détails de la facture.  |
| changement      | Tableau d’objets de [facture](#invoice)   | Les modifications apportées à cette facture.  |
| documentType    | string | Type de document de la facture : « note de crédit », « facture ». |
| amendsOf        | string | Numéro de référence du document dont ce document est un amendement.  |
| invoiceType     | string  | Type de facture : « périodique », « une \_ fois ».   |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)  | Liens vers les ressources.  |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.  |

## <a name="invoicedetail"></a>InvoiceDetail

Une facture contient une collection d’articles facturés, et chaque élément est représenté par une ressource InvoiceDetail.

| Propriété            | Type                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | Type de détail de la facture : « aucun », « \_ éléments de ligne d’utilisation \_ », « éléments de ligne de facturation \_ \_ ». |
| billingProvider     | string                                                         | Fournisseur de facturation : « None », « Office », « Azure » ou « Azure \_ Data \_ Market ».         |
| liens               | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens vers les ressources.                                                               |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Chaque facture individuelle au sein d’une facture est représentée sous la forme d’un InvoiceLineItem.

| Propriété            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | Type de ligne de facturation : « aucun », « éléments de \_ ligne d’utilisation \_ », « \_ éléments de ligne de facturation \_ ». |
| billingProvider     | string                                                         | Fournisseur de facturation : « None », « Office », « Azure » ou « Azure \_ Data \_ Market ».            |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Décrit un résumé du solde et des frais totaux d’une facture.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | nombre                                                         | Solde de la facture. Il s’agit de la quantité totale de factures non payées. |
| currencyCode             | string                                                         | Code qui indique la devise utilisée pour le montant du solde.       |
| currencySymbol           | string                                                         | Symbole monétaire utilisé.                                             |
| accountingDate           | chaîne au format date-heure UTC                                 | Date de la dernière mise à jour du montant du solde.                         |
| firstInvoiceCreationDate | chaîne au format date-heure UTC                                 | Date à laquelle la première facture du client a été créée.              |
| lastPaymentDate          | chaîne au format date-heure UTC                                 | Date du dernier paiement.                                         |
| lastPaymentAmount        | nombre                                                         | Montant du dernier paiement.                                       |
| latestInvoiceDate        | chaîne au format date-heure UTC                                 | Date à laquelle la dernière facture du client a été créée.               |
| details                  | Tableau d’objets [InvoiceSummaryDetail](#invoicesummarydetail) | Détails du résumé de la facture.                                           |
| liens                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Liens vers les ressources.                                                   |
| attributs               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Représente un résumé des détails individuels d’un type de facture (par exemple, périodique, une \_ fois).

| Propriété            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | string                                                         | Type de facture : « périodique », « une \_ fois ».                                       |
| summary             | Objet [InvoiceSummary](#invoicesummary)                       | Résumé de la facture par type de facture.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Représente une collection de type [InvoiceSummary](#invoicesummary) qui contient les détails individuels d’un type de facture par devise.

| Propriété            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | Tableau d’objets [InvoiceSummary](#invoicesummary)             | Résumé de la facture par type de facture par devise.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Représente un élément de facturation de facture pour les abonnements basés sur une licence.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| proportion                   | string                                                         | Obtient ou définit la quantité totale. Montant total = prix unitaire * quantité.  |
| attributs               | string                                                         | Obtient les attributs.                                                  |
| billingCycleType         | string                                                         | Obtient ou définit le type de cycle de facturation.                                  |
| billingProvider          | string                                                         | Obtient le fournisseur de facturation.                                            |
| chargeEndDate            | chaîne au format date-heure UTC                                 | Obtient ou définit la date de fin des frais.                             |
| chargeStartDate          | chaîne au format date-heure UTC                                 | Obtient ou définit la date de début des frais.                           |
| chargeType               | string                                                         | Obtient ou définit le type de frais.                                      |
| currency                 | string                                                         | Obtient ou définit la devise utilisée pour cet élément de ligne.                    |
| customerId               | string                                                         | Obtient ou définit l’identificateur unique du client dans la plateforme de facturation Microsoft.  |
| customerName             | chaîne au format date-heure UTC                                 | Obtient ou définit le nom du client.                                       |
| domainName               | string                                                         | Obtient ou définit le nom de domaine.                                             |
| durableOfferId           | string                                                         | Obtient ou définit l’identificateur unique de l’offre durable.                     |
| invoiceLineItemType      | string                                                         | Obtient le type de l’élément de ligne de facture.                                   |
| mpnId                    | nombre                                                         | Obtient ou définit l’ID MPN associé à cet élément de ligne. Pour les revendeurs directs, il s’agit de l’ID MPN du revendeur. Pour les revendeurs indirects, il s’agit de l’ID MPN de la valeur ajoutée revendeur (VAR).                                   |
| offerId                  | string                                                         | Obtient ou définit l’identificateur unique de l’offre.                             |
| offerName                | string                                                         | Obtient ou définit le nom de l’offre.                                          |
| orderId                  | string                                                         | Obtient ou définit l’identificateur unique de l’ordre.                             |
| Partenaire                | string                                                         | Obtient ou définit l’ID du locataire Azure Active Directory partenaire.            |
| quantité                 | nombre                                                         | Obtient ou définit le nombre d’unités associées à cet élément de ligne.      |
| subscriptionDescription  | string                                                         | Obtient ou définit la description de l’abonnement.                            |
| subscriptionEndDate      | chaîne au format date-heure UTC                                 | Obtient ou définit la date à laquelle l’abonnement expire.                      |
| subscriptionId           | string                                                         | Obtient ou définit l’identificateur unique de l’abonnement.                      |
| subscriptionName         | string                                                         | Obtient ou définit le nom de l’abonnement.                                   |
| subscriptionStartDate    | chaîne au format date-heure UTC                                 | Obtient ou définit la date de début de l’abonnement.                   |
| sous                 | nombre                                                         | Obtient ou définit le montant après la remise.                               |
| syndicationPartnerSubscriptionNumber | string                                             | Obtient ou définit le numéro d’abonnement du partenaire de syndication.             |
| tax                      | nombre                                                         | Obtient ou définit les taxes facturées.                                       |
| tier2MpnId               | nombre                                                         | Obtient ou définit l’ID MPN du partenaire de niveau 2 associé à cet élément de ligne. |
| totalForCustomer         | nombre                                                         | Obtient ou définit le montant total après la remise et la taxe.                 |
| totalOtherDiscount       | nombre                                                         | Obtient ou définit la remise associée à cet achat.              |
| unitPrice                | nombre                                                         | Obtient ou définit le prix unitaire.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Représente un élément de facturation de facture pour les abonnements basés sur l’utilisation.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| attributs               | string                                                         | Obtient les attributs.                                                  |
| billingCycleType         | string                                                         | Obtient ou définit le type de cycle de facturation.                                  |
| billingProvider          | string                                                         | Obtient le fournisseur de facturation.                                            |
| chargeEndDate            | chaîne au format date-heure UTC                                 | Obtient ou définit la date de fin des frais.                             |
| chargeStartDate          | chaîne au format date-heure UTC                                 | Obtient ou définit la date de début des frais.                           |
| chargeType               | string                                                         | Obtient ou définit le type de frais.                                      |
| consumedQuantity         | nombre                                                         | Obtient ou définit le nombre total d’unités consommées.                                |
| consumptionDiscount      | string                                                         | Obtient ou définit la remise sur la consommation.                             |
| consumptionPrice         | string                                                         | Obtient ou définit le prix de la quantité consommée.                          |
| currency                 | string                                                         | Obtient ou définit la devise associée aux prix.                 |
| customerName             | string                                                         | Obtient ou définit le nom du client.                                       |
| customerId               | string                                                         | Obtient ou définit l’identificateur unique du client.                          |
| detailLineItemId         | nombre                                                         | Obtient ou définit l’ID d’élément de ligne de détail. Identifie de façon unique les éléments de ligne pour les cas où le calcul est différent pour les unités consommées. Exemple : total consommé = 1338, 1024 est facturé avec un taux, 314 est facturé avec un taux différent.        |
| domainName               | string                                                         | Obtient ou définit le nom de domaine.                                             |
| includedQuantity         | nombre                                                         | Obtient ou définit les unités incluses dans l’ordre.                         |
| invoiceLineItemType      | string                                                         | Obtient le type de l’élément de ligne de facture.                                   |
| invoiceNumber            | string                                                         | Obtient ou définit le numéro de la facture.                                      |
| listPrice                | nombre                                                         | Obtient ou définit le prix de chaque unité.                                  |
| mpnId                    | nombre                                                         | Obtient ou définit l’ID MPN associé à cet élément de ligne. Pour les revendeurs directs, il s’agit de l’ID MPN du revendeur. Pour les revendeurs indirects, il s’agit de l’ID MPN de la valeur ajoutée revendeur (VAR).                                   |
| orderId                  | string                                                         | Obtient ou définit l’identificateur unique de l’ordre.                             |
| Divisé par overagequantity          | nombre                                                         | Obtient ou définit la quantité consommée au-dessus de l’utilisation autorisée.               |
| partnerBillableAccountId | string                                                         | Obtient ou définit l’ID de compte facturable du partenaire.                         |
| Partenaire                | string                                                         | Obtient ou définit l’ID du locataire Azure Active Directory partenaire.            |
| partnerName              | string                                                         | Obtient ou définit le nom du partenaire.                                      |
| postTaxEffectiveRate     | nombre                                                         | Obtient ou définit le tarif effectif après taxes.                         |
| postTaxTotal             | nombre                                                         | Obtient ou définit le total des frais après taxe. Frais tarif + montant des taxes |
| preTaxCharges            | nombre                                                         | Obtient ou définit le prix facturé avant les taxes.                          |
| preTaxEffectiveRate      | nombre                                                         | Obtient ou définit le prix effectif avant les taxes.                        |
| region                   | string                                                         | Obtient ou définit la région associée à l’instance de ressource.        |
| resourceGuid             | string                                                         | Obtient ou définit l’identificateur de ressource.                                 |
| resourceName             | string                                                         | Obtient ou définit le nom de ressource. Exemple : base de données (Go/mois).         |
| serviceName              | string                                                         | Obtient ou définit le nom du service. Exemple : Azure Data Service.           |
| serviceType              | string                                                         | Obtient ou définit le type de service. Exemple : Azure SQL Azure DB.           |
| sku                      | string                                                         | Obtient ou définit la référence SKU du service.                                         |
| subscriptionDescription  | string                                                         | Obtient ou définit la description de l’abonnement.                            |
| subscriptionId           | string                                                         | Obtient ou définit l’identificateur unique de l’abonnement.                      |
| subscriptionName         | string                                                         | Obtient ou définit le nom de l’abonnement.                                   |
| taxAmount                | nombre                                                         | Obtient ou définit le montant des taxes facturées.                               |
| tier2MpnId               | nombre                                                         | Obtient ou définit l’ID MPN du partenaire de niveau 2 associé à cet élément de ligne. |
| unité                     | string                                                         | Obtient ou définit l’unité de mesure pour l’utilisation d’Azure.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Représente les opérations disponibles sur une instruction de facture dans application/pdf.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent avec contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Représente un élément de facturation de facture pour les abonnements basés sur une licence.

| Propriété | Type | Description |
| --- | --- | --- |
| PartnerId | string | Obtient ou définit l’ID de locataire du partenaire. |
| CustomerId | string | Obtient ou définit l’ID du locataire client. |
| CustomerName | string | Obtient ou définit le nom du client. |
| CustomerDomainName | string | Obtient ou définit le nom de domaine du client. |
| CustomerCountry | string | Obtient ou définit le pays du client. |
| InvoiceNumber | string | Obtient ou définit le numéro de la facture. |
| MpnId | string | Obtient ou définit l’ID MPN associé à cet élément de ligne. |
| ResellerMpnId | int | Obtient ou définit l’identificateur unique de l’ordre. |
| OrderDate | DateTime | Obtient ou définit la date de création de l’ordre. |
| ProductId | string | Obtient ou définit l’identificateur unique du produit. |
| SkuId | string | Obtient ou définit l’identificateur unique de la référence (SKU). |
| AvailabilityId | string | Obtient ou définit l’identificateur unique de disponibilité. |
| ProductName | string | Obtient ou définit le nom du produit. |
| SkuName | string | Obtient ou définit le nom de la référence (SKU). |
| ChargeType | string | Obtient ou définit le type de frais. |
| UnitPrice | Décimal | Obtient ou définit le prix unitaire. |
| EffectiveUnitPrice | Décimal | Obtient ou définit le prix unitaire effectif. |
| Unité | string | Obtient ou définit le type d’unité. |
| Quantité | int | Obtient ou définit le nombre d’unités associées à cet élément de ligne. |
| Sous-total | Décimal | Obtient ou définit le montant après la remise. |
| TaxTotal | Décimal | Obtient ou définit les taxes facturées. |
| TotalForCustomer | Décimal | Obtient ou définit le montant total après la remise et la taxe. |
| Devise | string | Obtient ou définit la devise utilisée pour cet élément de ligne. |
| PublisherName | string | Obtient ou définit le nom de l’éditeur associé à cet achat. |
| PublisherId | string | Obtient ou définit l’ID d’éditeur associé à cet achat. |
| SubscriptionDescription | string | Obtient ou définit la description de l’abonnement associée à cet achat. |
| SubscriptionId | string | Obtient ou définit l’ID d’abonnement associé à cet achat. |
| ChargeStartDate | DateTime | Obtient ou définit la date de début de la facturation associée à cet achat. |
| ChargeEndDate | DateTime | Obtient ou définit la date de fin de frais associée à cet achat. |
| TermAndBillingCycle | string | Obtient ou définit le terme et le cycle de facturation associés à cet achat. |
| AlternateId | string | Obtient ou définit l’ID de remplacement (ID de devis). |
| PriceAdjustmentDescription | string | Obtient ou définit la description de l’ajustement de prix. |
| DiscountDetails | string |  **Déconseillé**. Obtient ou définit les détails de la remise associés à cet achat. |
| PricingCurrency | string | Obtient ou définit le code de la devise de tarification. |
| PCToBCExchangeRate | Décimal | Obtient ou définit la devise de tarification au taux de change de la devise de facturation. |
| PCToBCExchangeRateDate | DateTime | Obtient ou définit la date du taux de change à laquelle la devise de tarification du taux de change de la devise de facturation a été déterminée. |
| BillableQuantity | Décimal | Obtient ou définit les unités achetées. Pour chaque colonne de conception nommée **BillableQuantity**. |
| MeterDescription | string | Obtient ou définit la description du compteur pour l’élément de ligne de consommation. |
| ReservationOrderId | string | Obtient ou définit l’identificateur d’ordre de réservation pour un achat Azure RI. |
| BillingFrequency | string | Obtient ou définit la fréquence de facturation. |
| InvoiceLineItemType | InvoiceLineItemType | Retourne le type de l’élément de ligne de facture. |
| BillingProvider | BillingProvider | Retourne le fournisseur de facturation. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Représente les Articles de ligne de rapprochement non facturés pour une utilisation quotidienne.

| Propriété | Type | Description |
| --- | --- | --- |
| PartnerId | string | Obtient ou définit l’ID de locataire du partenaire. |
| PartnerName | string | Obtient ou définit le nom du partenaire. |
| CustomerId | string | Obtient ou définit l’ID de locataire du client auquel appartient l’utilisation. |
| CustomerName | string | Obtient ou définit le nom de la société cliente à laquelle l’utilisation appartient. |
| CustomerDomainName | string | Obtient ou définit le nom de domaine du client auquel appartient l’utilisation. |
| InvoiceNumber | string | Obtient ou définit l’ID de la facture à laquelle l’utilisation appartient. |
| ProductId | string | Obtient ou définit l’identificateur unique du produit. |
| SkuId | string | Obtient ou définit l’identificateur unique de la référence (SKU). |
| AvailabilityId | string | Obtient ou définit l’identificateur unique de disponibilité. |
| SkuName | string | Obtient ou définit le nom de la référence (SKU) pour le service. |
| ProductName | string | Obtient ou définit le nom du produit. |
| PublisherName | string | Obtient ou définit le nom de l’éditeur. |
| PublisherId | string | Obtient ou définit l’ID du serveur de publication. |
| SubscriptionId | string | Obtient ou définit l'ID d'abonnement. |
| SubscriptionDescription | string | Obtient ou définit la description de l’abonnement. |
| ChargeStartDate | DateTime | Obtient ou définit la date de début des frais. |
| ChargeEndDate | DateTime | Obtient ou définit la date de fin de la facturation. |
| UsageDate | DateTime | Obtient ou définit la date d’utilisation. |
| MeterType | string | Obtient ou définit le type de compteur. |
| MeterCategory | string | Obtient ou définit la catégorie du compteur. |
| MeterId | string | Obtient ou définit l’ID de compteur (GUID). |
| MeterSubCategory | string | Obtient ou définit la sous-catégorie du compteur. |
| MeterName | string | Obtient ou définit le nom du compteur. |
| MeterRegion | string | Obtient ou définit la région du compteur. |
| UnitOfMeasure | string | Obtient ou définit l’unité de mesure. |
| ResourceLocation | string | Obtient ou définit l’emplacement de la ressource. |
| ConsumedService | string | Obtient ou définit le nom du service consommé. |
| ResourceGroup | string | Obtient ou définit le nom du groupe de ressources. |
| URI | string | Obtient ou définit l’URI de l’instance de ressource sur le sujet de l’utilisation. |
| Étiquettes | string | Obtient ou définit les balises ajoutées par le client. |
| AdditionalInfo | string | Obtient ou définit les métadonnées spécifiques au service. Par exemple, le type d’image d’une machine virtuelle. |
| ServiceInfo1 | string | Obtient ou définit les métadonnées de service Azure internes. |
| ServiceInfo2 | string | Obtient ou définit les informations de service, par exemple, un type d’image pour un ordinateur virtuel et un nom de fournisseur de services Internet pour ExpressRoute. |
| CustomerCountry | string | Obtient ou définit le pays du client. |
| MpnId | string | Obtient ou définit l’ID MPN associé à cet élément de ligne. |
| ResellerMpnId | string | Obtient ou définit l’ID MPN du revendeur du niveau 2 associé à cet élément de ligne. |
| ChargeType | string | Obtient ou définit le type de frais. |
| UnitPrice | Décimal | Obtient ou définit le prix unitaire. |
| Quantité | Décimal | Obtient ou définit la quantité d’utilisation. |
| Unité | string | Obtient ou définit le type d’unité (par exemple, 1 heure). |
| BillingPreTaxTotal | Décimal | Obtient ou définit le coût total ou le coût total avant les taxes dans la devise locale du client ou de la devise de facturation. |
| BillingCurrency | string | Obtient ou définit la devise ISO dans laquelle le compteur est facturé en devise locale du client ou de la devise de facturation. |
| PricingPreTaxTotal | Décimal | Obtient ou définit le coût total ou le coût total avant les taxes dans la devise USD ou le catalogue utilisé pour l’évaluation. |
| PricingCurrency | string | Obtient ou définit la devise ISO dans laquelle le compteur est facturé dans la devise USD ou dans le catalogue utilisé pour l’évaluation. |
| EntitlementId | string | Obtient ou définit l’ID du droit (abonnement Azure). |
| EntitlementDescription | string | Obtient ou définit la description du droit (abonnement Azure). |
| PCToBCExchangeRate | string | Obtient ou définit la devise de tarification au taux de change de la devise de facturation. |
| PCToBCExchangeRateDate | DateTime | Obtient ou définit la devise de tarification à la date du taux de change de la devise de facturation. |
| EffectiveUnitPrice | Décimal | Obtient ou définit le prix unitaire effectif. |
| RateOfPartnerEarnedCredit | Décimal | Obtient ou définit le taux de crédit gagné du partenaire. |
| hasPartnerEarnedCredit | bool | Obtient ou définit le crédit gagné du partenaire appliqué. |
| InvoiceLineItemType | InvoiceLineItemType | Retourne le type de l’élément de ligne de facture. |
| BillingProvider | BillingProvider | Retourne le fournisseur de facturation. |
