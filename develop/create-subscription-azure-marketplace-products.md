---
title: Créer un abonnement pour les produits de la place de marché commercial
description: Les développeurs peuvent créer et gérer un abonnement pour les produits de la place de marché commercial à l’aide des API de l’espace partenaires.
ms.assetid: ''
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9bdc918387af62eec6abdaf5656e0d8bafb7f2b3
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488649"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Créer un abonnement pour les produits de la place de marché commercial

S’applique à :

* Espace partenaires

Vous pouvez créer un abonnement pour des produits de la place de marché commerciale à l’aide des API de l’Espace partenaires. Vous devez [obtenir une liste des offres pour un marché](#get-a-list-of-offers-for-a-market), [créer et envoyer une commande](#create-and-submit-an-order) pour un abonnement de la place de marché commercial, puis [récupérer un lien d’activation](#get-activation-link).

Vous pouvez également [effectuer la gestion du cycle de vie](#lifecycle-management) et [gérer les factures](#invoice-and-reconciliation) pour ces abonnements.

## <a name="prerequisites"></a>Conditions préalables

* Informations d' [authentification de l’espace partenaires](partner-center-authentication.md) . Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
* Identificateur du client. Si vous n’avez pas d’identificateur de client : Connectez-vous à l’espace partenaires, sélectionnez le client dans la liste clients, sélectionnez **compte**, puis enregistrez son **identifiant Microsoft**.

## <a name="get-a-list-of-offers-for-a-market"></a>Obtenir la liste des offres pour un marché

Vous pouvez vérifier les offres disponibles pour un marché à l’aide des modèles d’API de l’espace partenaires suivants :

* **[Produit](product-resources.md#product)** : construction de regroupement pour les biens ou services pouvant être achetés. Un produit lui-même n’est pas un élément pouvant être acheté.
* **[Référence (SKU](product-resources.md#sku)** ) : une référence SKU (Stock Keeping Unit) sous un produit. Celles-ci représentent les différentes formes du produit.
* **[Disponibilité](product-resources.md#availability)** : configuration dans laquelle une référence (SKU) est disponible à l’achat (par exemple, pays, devise ou secteur d’activité).

Avant d’acheter une réservation Azure, procédez comme suit :

1. Identifiez et récupérez le produit et la référence (SKU) que vous souhaitez acheter. Si vous connaissez déjà l’ID de produit et l’ID de référence (SKU), sélectionnez-les.

    * [Obtenir une liste de produits](get-a-list-of-products.md)
    * [Obtenir un produit à l’aide de l’ID de produit](get-a-product-by-id.md)
    * [Obtenir la liste des références (SKU) d’un produit](get-a-list-of-skus-for-a-product.md)
    * [Obtenir une référence SKU à l’aide de l’ID de référence](get-a-sku-by-id.md)

    > [!NOTE]
    > Vous pouvez identifier les produits de la place de marché commercial en fonction de leur propriété **ProductType** **« Azure »** et de leur propriété de **sous-type** « **Saas »** .

2. Si les références SKU sont marquées d’un prérequis **InventoryCheck** , [Vérifiez l’inventaire d’une référence (SKU](check-inventory.md)).

    > [!NOTE]
    > À ce stade, aucun produit de la place de marché commercial ne prend en charge la vérification de stock ou est marqué avec un prérequis **InventoryCheck** .

3. Récupérez la disponibilité de la référence SKU. Vous aurez besoin de la **CatalogItemId** de disponibilité lors de la mise en place de la commande, que vous pouvez récupérer via les API suivantes :

    * [Obtenir la liste des disponibilités pour une référence (SKU)](get-a-list-of-availabilities-for-a-sku.md)
    * [Procurez-vous une disponibilité à l’aide de l’ID de disponibilité](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Créer et envoyer une commande

Pour soumettre votre commande de réservation Azure, procédez comme suit :

1. [Créez un panier](create-a-cart.md) pour stocker la collection d’éléments de catalogue que vous souhaitez acheter. Lorsque vous créez un [panier](cart-resources.md#cart), les [éléments de ligne de panier](cart-resources.md#cartlineitem) sont automatiquement regroupés en fonction de ce qui peut être acheté ensemble dans le même [ordre](order-resources.md#order). (Vous pouvez également [mettre à jour un panier](update-a-cart.md).)
2. [Extraire le panier](checkout-a-cart.md), ce qui entraîne la création d’une [commande](order-resources.md#order).

### <a name="get-order-details"></a>Recevoir les détails de la commande

Vous pouvez [récupérer les détails d’une commande individuelle à l’aide de l’ID de commande](get-an-order-by-id.md). Vous pouvez également [récupérer une liste de toutes les commandes pour un client spécifique](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> Après l’envoi d’une commande, un délai de 15 minutes maximum s’écoule avant que la commande apparaisse dans la liste de commandes de ce client.

## <a name="get-activation-link"></a>Accéder au lien d’activation

Le partenaire ou le client doit activer les abonnements aux produits Azure Marketplace. Vous pouvez [recevoir un lien d’activation par élément de ligne de commande](get-activation-link-by-order-line-item.md). Vous pouvez également [obtenir un abonnement par ID](get-a-subscription-by-id.md), puis énumérer sa propriété **Links** pour créer un lien d’activation.

## <a name="lifecycle-management"></a>Gestion du cycle de vie

Vous pouvez gérer le cycle de vie de vos abonnements à des produits de la place de marché commercial à l’aide des méthodes suivantes :

* [Annuler un abonnement au marché commercial](cancel-an-azure-marketplace-subscription.md)
* [Activer ou désactiver le renouvellement autorenouvelé pour un abonnement à la place de marché commercial](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Gestion des quantités

La quantité d’un abonnement au marché commercial doit être comprise dans les limites définies par la [référence SKU](product-resources.md#sku) associée (voir les attributs **minimumQuantity** et **maximumQuantity** ). Pour mettre à jour la quantité d’un abonnement à la place de marché commercial, utilisez la méthode suivante :

* [Modifier la quantité d’un abonnement](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Facture et rapprochement

Vous pouvez gérer les [factures](invoice-resources.md) client (y compris les frais liés aux abonnements à des produits de la place de marché commercial) à l’aide des méthodes suivantes :

* [Obtient les éléments de ligne de la consommation de la place de marché commercial facturés](get-invoice-billed-consumption-lineitems.md)
* [Obtenir des liens d’estimation de facture](get-invoice-estimate-links.md)
* [Obtient les éléments de ligne de facturation de la place de marché commercial non facturés](get-invoice-unbilled-consumption-lineitems.md)
* [Obtient les éléments de ligne de rapprochement non facturés de facture](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Test à l’aide du compte sandbox d’intégration

En production, après avoir créé un abonnement aux produits SaaS de la place de marché commercial, vous devez récupérer un lien d’activation personnalisé auprès de l’espace partenaires et visiter le site de l’éditeur pour terminer le processus d’installation. La facturation de l’abonnement commence uniquement une fois l’installation terminée.

Dans l’environnement du bac à sable (sandbox) CSP, il n’existe aucune intégration avec les éditeurs de logiciels indépendants. Si vous essayez de récupérer un lien d’activation à partir de l’espace partenaires, un lien factice est renvoyé. Vous ne pouvez pas utiliser ce lien factice pour terminer le processus d’installation sur le site de l’éditeur. Pour utiliser le compte de bac à sable (sandbox) d’intégration afin de tester la facturation des abonnements aux produits SaaS de la place de marché commercial, utilisez la méthode suivante pour activer l’abonnement. La facturation de l’abonnement commencera après l’activation réussie :

* [Activer un abonnement sandbox pour les produits de la place de marché commercial](activate-sandbox-subscription-azure-marketplace-products.md)

