---
title: Acheter des éléments de catalogue
description: Comment acheter des éléments de catalogue à l’aide de l’API espace partenaires.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094952"
---
# <a name="purchase-catalog-items"></a>Acheter des éléments de catalogue

**S’applique à**

- Espace partenaires

Le scénario suivant illustre le processus générique pour l’achat d’éléments à partir du catalogue à l’aide de l’API espace partenaires.

## <a name="discovery"></a>Découverte

Sélectionnez produits et références SKU, puis vérifiez leur disponibilité à l’aide des modèles d’API de l’espace partenaires suivants :

- [Produit](product-resources.md#product) : construction de regroupement pour les biens ou services pouvant être achetés. Un produit par lui-même n’est pas un élément pouvant être acheté.
- [Référence](product-resources.md#sku) (SKU), une unité de conservation de stock (SKU) achetée dans un produit. Celles-ci représentent les différentes formes du produit.
- [Disponibilité](product-resources.md#availability) : configuration dans laquelle une référence (SKU) est disponible à l’achat (par exemple, pays, devise et secteur).

Pour acheter un élément dans le catalogue, procédez comme suit :

1. Identifiez et récupérez le produit et la référence (SKU) que vous souhaitez acheter.

   - [Obtenir la liste des produits](get-a-list-of-products.md)
   - [Obtenir un produit à l’aide de l’ID de produit](get-a-product-by-id.md)
   - [Obtenir la liste des références SKU d’un produit](get-a-list-of-skus-for-a-product.md)
   - [Obtenir une référence SKU à l’aide de l’ID de référence](get-a-sku-by-id.md)

2. Vérifiez l’inventaire d’une référence (SKU). Cette étape n’est nécessaire que pour les références (SKU) marquées avec une valeur **InventoryCheck** dans la propriété [purchasePrerequisites](product-resources.md#sku) .

   - [Vérifier le stock](check-inventory.md)

3. Récupérez la [disponibilité](product-resources.md#availability) de la [référence SKU](product-resources.md#sku). Vous aurez besoin de la **CatalogItemId** de disponibilité lors de la mise en place de la commande. Pour ce faire, utilisez l’une des API suivantes :

   - [Obtenir la liste des disponibilités d’une référence SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Procurez-vous une disponibilité à l’aide de l’ID de disponibilité](get-an-availability-by-id.md)

## <a name="order-submission"></a>Soumission de commande

Pour envoyer l’ordre des éléments du catalogue, procédez comme suit :

1. Créez un [panier](cart-resources.md) pour stocker la collection d’éléments de catalogue que vous souhaitez acheter. Lorsque vous créez un panier, les [éléments de ligne de panier](cart-resources.md#cartlineitem) sont automatiquement regroupés en fonction de ce qui peut être acheté ensemble dans le même [ordre](order-resources.md).

   - [Créer un panier d’achat](create-a-cart.md)
   - [Mettre à jour un panier d’achat](update-a-cart.md)

2. Consultez le panier. L’extraction d’un panier entraîne la création d’une [commande](order-resources.md).

   - [Extraire le panier](checkout-a-cart.md)

## <a name="get-order-details"></a>Recevoir les détails de la commande

Vous pouvez récupérer les détails d’une commande individuelle à l’aide de l’ID de commande ou obtenir la liste des commandes d’un client. Il y a un délai de 15 minutes entre le moment où une commande est soumise et le moment où elle apparaît dans une liste de commandes d’un client.

- Consultez [obtenir une commande par ID](get-an-order-by-id.md) pour obtenir les détails d’une commande spécifique à l’aide des ID de commande.

- Consultez [obtenir toutes les commandes](get-all-of-a-customer-s-orders.md) d’un client pour obtenir la liste des commandes d’un client à l’aide de l’ID client.

- Consultez [obtenir une liste de commandes par client et type de cycle de facturation](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) pour obtenir la liste des commandes d’un client par [type de cycle de facturation](product-resources.md#billingcycletype) , ce qui vous permet de répertorier les commandes d’élément de catalogue (frais à usage unique) et les commandes annuelles ou mensuelles facturées séparément.

## <a name="lifecycle-management"></a>Gestion du cycle de vie

Dans le cadre de la gestion du cycle de vie de vos éléments de catalogue dans l’espace partenaires, vous pouvez récupérer des informations sur les [droits](entitlement-resources.md)de l’élément de catalogue et obtenir les détails de la réservation à l’aide de l’ID de commande de réservation. Pour obtenir des exemples d’utilisation, consultez [obtenir des droits](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Facture et rapprochement

Les scénarios suivants vous montrent comment afficher par programme les [factures](invoice-resources.md)de votre client et obtenir les soldes et les résumés de votre compte qui incluent des frais à usage unique pour les éléments du catalogue.

### <a name="balance-and-payment"></a>Solde et paiement

Pour obtenir le solde actuel du compte dans votre type de devise par défaut qui correspond à un solde des frais périodiques et ponctuels (élément du catalogue), consultez [obtenir le solde actuel de votre compte](get-the-reseller-s-current-account-balance.md).

### <a name="multi-currency-balance-and-payment"></a>Solde et paiement à plusieurs devises

Pour obtenir le solde de votre compte actuel et un ensemble de résumés de facture contenant un résumé de facture avec des frais périodiques et ponctuels pour chacun des types de devise de votre client, consultez [obtenir des résumés de facture](get-invoice-summaries.md).

### <a name="invoices"></a>Factures

Pour obtenir une collection de factures qui affichent des frais périodiques et ponctuels, consultez [obtenir une collection de factures](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Facture unique

Pour récupérer une facture spécifique à l’aide de l’ID de facture, consultez [obtenir une facture par ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Rapprochement

Pour obtenir une collection de détails sur les lignes de facturation (Articles de rapprochement) pour un ID de facture spécifique, consultez [obtenir des lignes de facturation](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Télécharger une facture au format PDF

Pour récupérer une déclaration de facture au format PDF à l’aide d’un ID de facture, consultez [obtenir une facture](get-invoice-statement.md).
