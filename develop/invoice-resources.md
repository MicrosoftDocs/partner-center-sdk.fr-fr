---
title: Ressources de facturation
description: Plusieurs ressources liées aux factures sont disponibles par le biais des API de l’espace partenaires. Ces ressources sont liées aux détails des factures et des articles.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6540af51e462974592ec18d7dd9ede8517ba1725
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899796"
---
# <a name="invoice-resources"></a>Ressources de facturation

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les ressources liées aux factures suivantes sont disponibles via les API de l’espace partenaires.

## <a name="invoice"></a>Facturation

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| id | chaîne | Identificateur de la facture. |
| invoiceDate | chaîne au format date-heure UTC | Date à laquelle la facture a été générée. |
| billingPeriodStartDate | chaîne au format date-heure UTC | Date de début de la période de facturation en heure UTC. |
| billingPeriodEndDate | chaîne au format date-heure UTC   | Date de fin de la période de facturation en heure UTC. |
| totalCharges | nombre | Total des frais. Comprend les frais liés aux transactions et les ajustements éventuels.     |
| paidAmount | nombre  | Montant payé par le partenaire. Négatif si un paiement a été reçu.  |
| currencyCode | chaîne  | Code qui indique la devise utilisée pour tous les montants et totaux des factures. |
| currencySymbol  | chaîne | Symbole monétaire utilisé pour tous les montants et totaux des factures. |
| pdfDownloadLink | chaîne  | Un lien pour télécharger la facture au format PDF. Ce lien n’est pas renvoyé dans le cadre des résultats de la recherche et est rempli uniquement si la facture est accessible par ID. Ce lien expire automatiquement dans 30 minutes. |
| invoiceDetails  | Tableau d’objets [InvoiceDetail](#invoicedetail)  | Détails de la facture.  |
| changement      | Tableau d’objets de [facture](#invoice)   | Les modifications apportées à cette facture.  |
| documentType    | chaîne | Type de document de la facture : « note de crédit », « facture ». |
| amendsOf        | chaîne | Numéro de référence du document dont ce document est un amendement.  |
| invoiceType     | chaîne  | Type de facture : « périodique », « un\_heure ».   |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)  | Liens vers les ressources.  |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.  |

## <a name="invoicedetail"></a>InvoiceDetail

Une facture contient une collection d’articles facturés, et chaque élément est représenté par une ressource InvoiceDetail.

| Propriété            | Type                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | chaîne                                                         | Type de détail de la facture : « None », « usage\_Line\_Items », « Billing\_Line\_Items ». |
| billingProvider     | chaîne                                                         | Le fournisseur de facturation : « None », « Office », « Azure » ou « Azure\_Data\_Market ».         |
| liens               | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens vers les ressources.                                                               |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Chaque facture individuelle au sein d’une facture est représentée sous la forme d’un InvoiceLineItem.

| Propriété            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | chaîne                                                         | Type de ligne de facturation : « None », « usage\_Line\_Items », « facturation\_Line\_Items ». |
| billingProvider     | chaîne                                                         | Le fournisseur de facturation : « None », « Office », « Azure » ou « Azure\_Data\_Market ».            |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Décrit un résumé du solde et des frais totaux d’une facture.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | nombre                                                         | Solde de la facture. Il s’agit de la quantité totale de factures non payées. |
| currencyCode             | chaîne                                                         | Code qui indique la devise utilisée pour le montant du solde.       |
| currencySymbol           | chaîne                                                         | Symbole monétaire utilisé.                                             |
| accountingDate           | chaîne au format date-heure UTC                                 | Date de la dernière mise à jour du montant du solde.                         |
| firstInvoiceCreationDate | chaîne au format date-heure UTC                                 | Date à laquelle la première facture du client a été créée.              |
| lastPaymentDate          | chaîne au format date-heure UTC                                 | Date du dernier paiement.                                         |
| lastPaymentAmount        | nombre                                                         | Montant du dernier paiement.                                       |
| latestInvoiceDate        | chaîne au format date-heure UTC                                 | Date à laquelle la dernière facture du client a été créée.               |
| détails                  | Tableau d’objets [InvoiceSummaryDetail](#invoicesummarydetail) | Détails du résumé de la facture.                                           |
| liens                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Liens vers les ressources.                                                   |
| attributs               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Représente un résumé des détails individuels d’un type de facture (par exemple, périodique, une\_fois).

| Propriété            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | chaîne                                                         | Type de facture : « périodique », « un\_heure ».                                       |
| tête             | Objet [InvoiceSummary](#invoicesummary)                       | Résumé de la facture par type de facture.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Représente une collection de type [InvoiceSummary](#invoicesummary) qui contient les détails individuels d’un type de facture par devise.  

| Propriété            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | Tableau d’objets [InvoiceSummary](#invoicesummary)             | Résumé de la facture par type de facture par devise.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Représente un élément de facturation de facture pour les abonnements basés sur une licence.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| proportion                   | chaîne                                                         | Obtient ou définit la quantité totale. Montant total = prix unitaire * quantité.  |
| attributs               | chaîne                                                         | Obtient les attributs.                                                  |
| billingCycleType         | chaîne                                                         | Obtient ou définit le type de cycle de facturation.                                  |
| billingProvider          | chaîne                                                         | Obtient le fournisseur de facturation.                                            |
| chargeEndDate            | chaîne au format date-heure UTC                                 | Obtient ou définit la date de fin des frais.                             |
| chargeStartDate          | chaîne au format date-heure UTC                                 | Obtient ou définit la date de début des frais.                           |
| chargeType               | chaîne                                                         | Obtient ou définit le type de frais.                                      |
| devise                 | chaîne                                                         | Obtient ou définit la devise utilisée pour cet élément de ligne.                    |
| customerId               | chaîne                                                         | Obtient ou définit l’identificateur unique du client dans la plateforme de facturation Microsoft.  |
| customerName             | chaîne au format date-heure UTC                                 | Obtient ou définit le nom du client.                                       |
| NomDomaine               | chaîne                                                         | Obtient ou définit le nom de domaine.                                             |
| durableOfferId           | chaîne                                                         | Obtient ou définit l’identificateur unique de l’offre durable.                     |
| invoiceLineItemType      | chaîne                                                         | Obtient le type de l’élément de ligne de facture.                                   |
| mpnId                    | nombre                                                         | Obtient ou définit l’ID MPN associé à cet élément de ligne. Pour les revendeurs directs, il s’agit de l’ID MPN du revendeur. Pour les revendeurs indirects, il s’agit de l’ID MPN de la valeur ajoutée revendeur (VAR).                                   |
| offerId                  | chaîne                                                         | Obtient ou définit l’identificateur unique de l’offre.                             |
| offerName                | chaîne                                                         | Obtient ou définit le nom de l’offre.                                          |
| orderId                  | chaîne                                                         | Obtient ou définit l’identificateur unique de l’ordre.                             |
| Partenaire                | chaîne                                                         | Obtient ou définit l’ID du locataire Azure Active Directory partenaire.            |
| quantity                 | nombre                                                         | Obtient ou définit le nombre d’unités associées à cet élément de ligne.      |
| subscriptionDescription  | chaîne                                                         | Obtient ou définit la description de l’abonnement.                            |
| subscriptionEndDate      | chaîne au format date-heure UTC                                 | Obtient ou définit la date à laquelle l’abonnement expire.                      |
| subscriptionId           | chaîne                                                         | Obtient ou définit l’identificateur unique de l’abonnement.                      |
| subscriptionName         | chaîne                                                         | Obtient ou définit le nom de l’abonnement.                                   |
| subscriptionStartDate    | chaîne au format date-heure UTC                                 | Obtient ou définit la date de début de l’abonnement.                   |
| sous                 | nombre                                                         | Obtient ou définit le montant après la remise.                               |
| syndicationPartnerSubscriptionNumber | chaîne                                             | Obtient ou définit le numéro d’abonnement du partenaire de syndication.             |
| TTC                      | nombre                                                         | Obtient ou définit les taxes facturées.                                       |
| tier2MpnId               | nombre                                                         | Obtient ou définit l’ID MPN du partenaire de niveau 2 associé à cet élément de ligne. |
| totalForCustomer         | nombre                                                         | Obtient ou définit le montant total après la remise et la taxe.                 |
| totalOtherDiscount       | nombre                                                         | Obtient ou définit la remise associée à cet achat.              |
| unitPrice                | nombre                                                         | Obtient ou définit le prix unitaire.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Représente un élément de facturation de facture pour les abonnements basés sur l’utilisation.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| attributs               | chaîne                                                         | Obtient les attributs.                                                  |
| billingCycleType         | chaîne                                                         | Obtient ou définit le type de cycle de facturation.                                  |
| billingProvider          | chaîne                                                         | Obtient le fournisseur de facturation.                                            |
| chargeEndDate            | chaîne au format date-heure UTC                                 | Obtient ou définit la date de fin des frais.                             |
| chargeStartDate          | chaîne au format date-heure UTC                                 | Obtient ou définit la date de début des frais.                           |
| chargeType               | chaîne                                                         | Obtient ou définit le type de frais.                                      |
| consumedQuantity         | nombre                                                         | Obtient ou définit le nombre total d’unités consommées.                                |
| consumptionDiscount      | chaîne                                                         | Obtient ou définit la remise sur la consommation.                             |
| consumptionPrice         | chaîne                                                         | Obtient ou définit le prix de la quantité consommée.                          |
| devise                 | chaîne                                                         | Obtient ou définit la devise associée aux prix.                 |
| customerName             | chaîne                                                         | Obtient ou définit le nom du client.                                       |
| customerId               | chaîne                                                         | Obtient ou définit l’identificateur unique du client.                          |
| detailLineItemId         | nombre                                                         | Obtient ou définit l’ID d’élément de ligne de détail. Identifie de façon unique les éléments de ligne pour les cas où le calcul est différent pour les unités consommées. Exemple : total consommé = 1338, 1024 est facturé avec un taux, 314 est facturé avec un taux différent.        |
| NomDomaine               | chaîne                                                         | Obtient ou définit le nom de domaine.                                             |
| includedQuantity         | nombre                                                         | Obtient ou définit les unités incluses dans l’ordre.                         |
| invoiceLineItemType      | chaîne                                                         | Obtient le type de l’élément de ligne de facture.                                   |
| invoiceNumber            | chaîne                                                         | Obtient ou définit le numéro de la facture.                                      |
| listPrice                | nombre                                                         | Obtient ou définit le prix de chaque unité.                                  |
| mpnId                    | nombre                                                         | Obtient ou définit l’ID MPN associé à cet élément de ligne. Pour les revendeurs directs, il s’agit de l’ID MPN du revendeur. Pour les revendeurs indirects, il s’agit de l’ID MPN de la valeur ajoutée revendeur (VAR).                                   |
| orderId                  | chaîne                                                         | Obtient ou définit l’identificateur unique de l’ordre.                             |
| Divisé par overagequantity          | nombre                                                         | Obtient ou définit la quantité consommée au-dessus de l’utilisation autorisée.               |
| partnerBillableAccountId | chaîne                                                         | Obtient ou définit l’ID de compte facturable du partenaire.                         |
| Partenaire                | chaîne                                                         | Obtient ou définit l’ID du locataire Azure Active Directory partenaire.            |
| partnerName              | chaîne                                                         | Obtient ou définit le nom du partenaire.                                      |
| postTaxEffectiveRate     | nombre                                                         | Obtient ou définit le tarif effectif après taxes.                         |
| postTaxTotal             | nombre                                                         | Obtient ou définit le total des frais après taxe. Frais tarif + montant des taxes |
| preTaxCharges            | nombre                                                         | Obtient ou définit le prix facturé avant les taxes.                          |
| preTaxEffectiveRate      | nombre                                                         | Obtient ou définit le prix effectif avant les taxes.                        |
| région                   | chaîne                                                         | Obtient ou définit la région associée à l’instance de ressource.        |
| resourceGuid             | chaîne                                                         | Obtient ou définit l’identificateur de ressource.                                 |
| resourceName             | chaîne                                                         | Obtient ou définit le nom de la ressource. Exemple : base de données (Go/mois).         |
| FormName              | chaîne                                                         | Obtient ou définit le nom du service. Exemple : Azure Data Service.           |
| serviceType              | chaîne                                                         | Obtient ou définit le type de service. Exemple : Azure SQL Azure DB.           |
| référence                      | chaîne                                                         | Obtient ou définit la référence SKU du service.                                         |
| subscriptionDescription  | chaîne                                                         | Obtient ou définit la description de l’abonnement.                            |
| subscriptionId           | chaîne                                                         | Obtient ou définit l’identificateur unique de l’abonnement.                      |
| subscriptionName         | chaîne                                                         | Obtient ou définit le nom de l’abonnement.                                   |
| taxAmount                | nombre                                                         | Obtient ou définit le montant des taxes facturées.                               |
| tier2MpnId               | nombre                                                         | Obtient ou définit l’ID MPN du partenaire de niveau 2 associé à cet élément de ligne. |
| unité                     | chaîne                                                         | Obtient ou définit l’unité de mesure pour l’utilisation d’Azure.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Représente les opérations disponibles sur une instruction de facture dans application/pdf.

| Propriété                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | objet                                                         | ByteArrayContent avec contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Représente un élément de facturation de facture pour les abonnements basés sur une licence.

| Propriété | Type | Description |
| --- | --- | --- |
| PartnerId | chaîne | Obtient ou définit l’ID de locataire du partenaire. |
| CustomerId | chaîne | Obtient ou définit l’ID du locataire client. |
| CustomerName | chaîne | Obtient ou définit le nom du client. |
| CustomerDomainName | chaîne | Obtient ou définit le nom de domaine du client. |
| CustomerCountry | chaîne | Obtient ou définit le pays du client. |
| InvoiceNumber | chaîne | Obtient ou définit le numéro de la facture. |
| MpnId | chaîne | Obtient ou définit l’ID MPN associé à cet élément de ligne. |
| ResellerMpnId | int | Obtient ou définit l’identificateur unique de l’ordre. |
| OrderDate | DateTime | Obtient ou définit la date de création de l’ordre. |
| ProductId | chaîne | Obtient ou définit l’identificateur unique du produit. |
| SkuId | chaîne | Obtient ou définit l’identificateur unique de la référence (SKU). |
| AvailabilityId | chaîne | Obtient ou définit l’identificateur unique de disponibilité. |
| ProductName | chaîne | Obtient ou définit le nom du produit. |
| SkuName | chaîne | Obtient ou définit le nom de la référence (SKU). |
| ChargeType | chaîne | Obtient ou définit le type de frais. |
| UnitPrice | decimal | Obtient ou définit le prix unitaire. |
| EffectiveUnitPrice | decimal | Obtient ou définit le prix unitaire effectif. |
| Unité | chaîne | Obtient ou définit le type d’unité. |
| Quantité | int | Obtient ou définit le nombre d’unités associées à cet élément de ligne. |
| Sous-total | decimal | Obtient ou définit le montant après la remise. |
| TaxTotal | decimal | Obtient ou définit les taxes facturées. |
| TotalForCustomer | decimal | Obtient ou définit le montant total après la remise et la taxe. |
| Currency | chaîne | Obtient ou définit la devise utilisée pour cet élément de ligne. |
| PublisherName | chaîne | Obtient ou définit le nom de l’éditeur associé à cet achat. |
| PublisherId | chaîne | Obtient ou définit l’ID d’éditeur associé à cet achat. |
| SubscriptionDescription | chaîne | Obtient ou définit la description de l’abonnement associée à cet achat. |
| SubscriptionId | chaîne | Obtient ou définit l’ID d’abonnement associé à cet achat. |
| ChargeStartDate | DateTime | Obtient ou définit la date de début de la facturation associée à cet achat. |
| ChargeEndDate | DateTime | Obtient ou définit la date de fin de frais associée à cet achat. |
| TermAndBillingCycle | chaîne | Obtient ou définit le terme et le cycle de facturation associés à cet achat. |
| AlternateId | chaîne | Obtient ou définit l’ID de remplacement (ID de devis). |
| PriceAdjustmentDescription | chaîne | Obtient ou définit la description de l’ajustement de prix. |
| DiscountDetails | chaîne |  **Deprecated**. Obtient ou définit les détails de la remise associés à cet achat. |
| PricingCurrency | chaîne | Obtient ou définit le code de la devise de tarification. |
| PCToBCExchangeRate | decimal | Obtient ou définit la devise de tarification au taux de change de la devise de facturation. |
| PCToBCExchangeRateDate | DateTime | Obtient ou définit la date du taux de change à laquelle la devise de tarification du taux de change de la devise de facturation a été déterminée. |
| BillableQuantity | decimal | Obtient ou définit les unités achetées. Pour chaque colonne de conception nommée **BillableQuantity**. |
| MeterDescription | chaîne | Obtient ou définit la description du compteur pour l’élément de ligne de consommation. |
| ReservationOrderId | chaîne | Obtient ou définit l’identificateur d’ordre de réservation pour un achat Azure RI. |
| BillingFrequency | chaîne | Obtient ou définit la fréquence de facturation. |
| InvoiceLineItemType | InvoiceLineItemType | Retourne le type de l’élément de ligne de facture. |
| BillingProvider | BillingProvider | Retourne le fournisseur de facturation. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Représente les Articles de ligne de rapprochement non facturés pour une utilisation quotidienne.

| Propriété | Type | Description |
| --- | --- | --- |
| PartnerId | chaîne | Obtient ou définit l’ID de locataire du partenaire. |
| PartnerName | chaîne | Obtient ou définit le nom du partenaire. |
| CustomerId | chaîne | Obtient ou définit l’ID de locataire du client auquel appartient l’utilisation. |
| CustomerName | chaîne | Obtient ou définit le nom de la société cliente à laquelle l’utilisation appartient. |
| CustomerDomainName | chaîne | Obtient ou définit le nom de domaine du client auquel appartient l’utilisation. |
| InvoiceNumber | chaîne | Obtient ou définit l’ID de la facture à laquelle l’utilisation appartient. |
| ProductId | chaîne | Obtient ou définit l’identificateur unique du produit. |
| SkuId | chaîne | Obtient ou définit l’identificateur unique de la référence (SKU). |
| AvailabilityId | chaîne | Obtient ou définit l’identificateur unique de disponibilité. |
| SkuName | chaîne | Obtient ou définit le nom de la référence (SKU) pour le service. |
| ProductName | chaîne | Obtient ou définit le nom du produit. |
| PublisherName | chaîne | Obtient ou définit le nom de l’éditeur. |
| PublisherId | chaîne | Obtient ou définit l’ID du serveur de publication. |
| SubscriptionId | chaîne | Obtient ou définit l'ID d'abonnement. |
| SubscriptionDescription | chaîne | Obtient ou définit la description de l’abonnement. |
| ChargeStartDate | DateTime | Obtient ou définit la date de début des frais. |
| ChargeEndDate | DateTime | Obtient ou définit la date de fin de la facturation. |
| UsageDate | DateTime | Obtient ou définit la date d’utilisation. |
| MeterType | chaîne | Obtient ou définit le type de compteur. |
| MeterCategory | chaîne | Obtient ou définit la catégorie du compteur. |
| MeterId | chaîne | Obtient ou définit l’ID de compteur (GUID). |
| MeterSubCategory | chaîne | Obtient ou définit la sous-catégorie du compteur. |
| MeterName | chaîne | Obtient ou définit le nom du compteur. |
| MeterRegion | chaîne | Obtient ou définit la région du compteur. |
| UnitOfMeasure | chaîne | Obtient ou définit l’unité de mesure. |
| ResourceLocation | chaîne | Obtient ou définit l’emplacement de la ressource. |
| ConsumedService | chaîne | Obtient ou définit le nom du service consommé. |
| ResourceGroup | chaîne | Obtient ou définit le nom du groupe de ressources. |
| URI | chaîne | Obtient ou définit l’URI de l’instance de ressource sur le sujet de l’utilisation. |
| Tags | chaîne | Obtient ou définit les balises ajoutées par le client. |
| AdditionalInfo | chaîne | Obtient ou définit les métadonnées spécifiques au service. Par exemple, un type d’image pour un ordinateur virtuel. |
| ServiceInfo1 | chaîne | Obtient ou définit les métadonnées de service Azure internes. |
| ServiceInfo2 | chaîne | Obtient ou définit les informations de service, par exemple, un type d’image pour un ordinateur virtuel et un nom de fournisseur de services Internet pour ExpressRoute. |
| CustomerCountry | chaîne | Obtient ou définit le pays du client. |
| MpnId | chaîne | Obtient ou définit l’ID MPN associé à cet élément de ligne. |
| ResellerMpnId | chaîne | Obtient ou définit l’ID MPN du revendeur du niveau 2 associé à cet élément de ligne. |
| ChargeType | chaîne | Obtient ou définit le type de frais. |
| UnitPrice | decimal | Obtient ou définit le prix unitaire. |
| Quantité | decimal | Obtient ou définit la quantité d’utilisation. |
| Unité | chaîne | Obtient ou définit le type d’unité (par exemple, 1 heure). |
| BillingPreTaxTotal | decimal | Obtient ou définit le coût total ou le coût total avant les taxes dans la devise locale du client ou de la devise de facturation. |
| BillingCurrency | chaîne | Obtient ou définit la devise ISO dans laquelle le compteur est facturé en devise locale du client ou de la devise de facturation. |
| PricingPreTaxTotal | decimal | Obtient ou définit le coût total ou le coût total avant les taxes dans la devise USD ou le catalogue utilisé pour l’évaluation. |
| PricingCurrency | chaîne | Obtient ou définit la devise ISO dans laquelle le compteur est facturé dans la devise USD ou dans le catalogue utilisé pour l’évaluation. |
| EntitlementId | chaîne | Obtient ou définit l’ID du droit (abonnement Azure). |
| EntitlementDescription | chaîne | Obtient ou définit la description du droit (abonnement Azure). |
| PCToBCExchangeRate | chaîne | Obtient ou définit la devise de tarification au taux de change de la devise de facturation. |
| PCToBCExchangeRateDate | DateTime | Obtient ou définit la devise de tarification à la date du taux de change de la devise de facturation. |
| EffectiveUnitPrice | decimal | Obtient ou définit le prix unitaire effectif. |
| RateOfPartnerEarnedCredit | decimal | Obtient ou définit le taux de crédit gagné du partenaire. |
| hasPartnerEarnedCredit | bool | Obtient ou définit le crédit gagné du partenaire appliqué. |
| InvoiceLineItemType | InvoiceLineItemType | Retourne le type de l’élément de ligne de facture. |
| BillingProvider | BillingProvider | Retourne le fournisseur de facturation. |
