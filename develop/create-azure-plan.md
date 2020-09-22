---
title: Créer un plan Azure
description: Les développeurs peuvent acheter, créer et gérer des plans Azure par programme à l’aide des API de l’espace partenaires.
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927345"
---
# <a name="create-an-azure-plan"></a>Créer un plan Azure

**S’applique à :**

* Espace partenaires

Vous pouvez acheter, créer et gérer un plan Azure à l’aide des API de l’espace partenaires. Le processus est similaire à la création d’un abonnement Microsoft Azure (MS-AZR-0145P). Vous devez [obtenir l’élément de catalogue pour le plan Azure](#get-the-catalog-item-for-azure-plan), puis [créer et envoyer une commande](#create-and-submit-an-order).

## <a name="prerequisites"></a>Prérequis

* Informations d' [authentification de l’espace partenaires](partner-center-authentication.md) . Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
* Identificateur du client. Si vous n’avez pas d’identificateur de client, suivez les étapes de la section [obtenir une liste de clients](get-a-list-of-customers.md). Vous pouvez également vous connecter à l’espace partenaires, choisir le client dans la liste des clients, sélectionner un **compte**, puis enregistrer son **identifiant Microsoft**.
* [Confirmation de l’acceptation par le client du contrat du client Microsoft](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Obtenir l’élément de catalogue pour le plan Azure

Avant de pouvoir créer un plan Azure pour un client, vous devez récupérer l’élément de catalogue correspondant. Vous pouvez récupérer l’élément de catalogue à l’aide des API de catalogue de l’espace partenaires existantes avec les modèles de ressources suivants.

* **[Produit](product-resources.md#product)**: construction de regroupement pour les biens ou services pouvant être achetés. Un produit lui-même n’est pas un élément pouvant être acheté.
* **[Référence (SKU](product-resources.md#sku)**) : une référence SKU (Stock Keeping Unit) sous un produit. Les références SKU représentent les différentes formes du produit.
* **[Disponibilité](product-resources.md#availability)**: configuration dans laquelle une référence (SKU) est disponible à l’achat (par exemple, pays, devise ou secteur).

Pour obtenir l’élément de catalogue pour un plan Azure, procédez comme suit :

1. Identifiez et récupérez l’identificateur de *produit* pour le plan Azure. Suivez les étapes de la section [obtenir une liste de produits](get-a-list-of-products.md) et spécifiez **targetView** en tant que **MicrosoftAzure**. (Si vous connaissez déjà l’identificateur de *produit* du plan Azure, vous pouvez suivre les étapes de la section [obtenir un produit à l’aide de l’ID de produit à la](get-a-product-by-id.md) place.)

2. Récupérez la **référence SKU** du produit pour le plan Azure. Suivez les étapes de la section [obtenir une liste des références SKU pour un produit](get-a-list-of-skus-for-a-product.md). Si vous connaissez déjà l’identificateur de référence (SKU) pour le plan Azure, vous pouvez suivre les étapes de la section [obtenir une référence à l’aide de l’ID de référence SKU à la](get-a-sku-by-id.md) place.

3. Récupérez la **disponibilité** de la référence SKU du plan Azure. Suivez les étapes de la section [obtenir une liste des disponibilités pour une référence (SKU](get-a-list-of-availabilities-for-a-sku.md)). Si vous connaissez déjà l’identificateur pour la disponibilité dont vous avez besoin, vous pouvez suivre les étapes de la section [obtenir une disponibilité à l’aide de l’ID de disponibilité à la](get-an-availability-by-id.md) place. *Veillez à noter la valeur de la propriété **CatalogItemId** de la disponibilité pour le plan Azure. Vous aurez besoin de cette valeur pour créer une commande.*

## <a name="create-and-submit-an-order"></a>Créer et envoyer une commande

Pour envoyer votre commande pour un plan Azure, procédez comme suit :

1. [Créez un panier](create-a-cart.md) pour stocker la collection d’éléments de catalogue que vous souhaitez acheter. Lorsque vous créez un [panier](cart-resources.md#cart), les [éléments de ligne de panier](cart-resources.md#cartlineitem) sont automatiquement regroupés en fonction de ce qui peut être acheté ensemble dans le même [ordre](order-resources.md#order). (Vous pouvez également [mettre à jour un panier](update-a-cart.md).)

2. [Extraire le panier](checkout-a-cart.md), ce qui entraîne la création d’une [commande](order-resources.md#order).

## <a name="get-order-details"></a>Recevoir les détails de la commande

Vous pouvez [récupérer les détails d’une commande individuelle à l’aide de l’ID de commande](get-an-order-by-id.md). Vous pouvez également [récupérer une liste de toutes les commandes pour un client spécifique](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Après l’envoi d’une commande, un délai de 15 minutes maximum s’écoule avant que la commande apparaisse dans la liste de commandes de ce client.

## <a name="manage-azure-plans"></a>Gérer les plans Azure

Une fois la commande traitée avec succès, une ressource d' **abonnement** au centre partenaires sera créée pour le plan Azure. Vous pouvez utiliser les méthodes suivantes pour gérer les ressources d' **abonnement** du centre partenaires afin de gérer le plan Azure :

* [Obtenir les abonnements d’un client](get-all-of-a-customer-s-subscriptions.md)
* [Obtenir une liste d’abonnements par commande](get-a-list-of-subscriptions-by-order.md)

Lorsqu’un plan Azure est créé dans l’espace partenaires, un abonnement d’utilisation Azure correspondant est également créé dans Azure. Vous pouvez également créer des abonnements d’utilisation Azure supplémentaires sous le même plan Azure à l’aide du portail Azure et des API Azure. Vous pouvez obtenir les identificateurs de tous les abonnements d’utilisation Azure associés à un plan Azure en suivant les étapes de la section [obtenir une liste des droits Azure pour l’abonnement au centre des partenaires](get-a-list-of-azure-entitlements-for-subscription.md)

## <a name="lifecycle-management"></a>Gestion du cycle de vie

Vous pouvez suspendre un plan Azure existant en suivant les étapes de la section [suspendre un abonnement](suspend-a-subscription.md).

*Vous ne pouvez suspendre un plan Azure existant que s’il n’a plus d’actifs d’utilisation actifs qui lui sont associés, y compris les abonnements d’utilisation Azure et les réservations Azure.*

Pour plus d’informations sur la désactivation des abonnements d’utilisation Azure, consultez [API Azure sur la gestion du cycle de vie des abonnements](/rest/api/resources/subscriptions).

Pour supprimer des réservations Azure existantes, vous devez [annuler les réservations](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation).
Après avoir suspendu un plan Azure, vous pouvez le réactiver.

Pour plus d’informations sur la réactivation d’un plan Azure, consultez [réactiver un abonnement suspendu](reactivate-a-suspended-a-subscription.md) .

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Transition des offres CSP existantes vers le plan Azure

Vous ne pouvez pas créer de plan Azure pour un client existant avec un abonnement Microsoft Azure (MS-AZR-0145P). Toutefois, vous pouvez [transférer un client à partir de ses offres Azure CSP existantes vers les services Azure sous le plan Azure](/partner-center/azure-plan-transition) dans la nouvelle expérience de commerce dans le programme CSP à partir de l’espace partenaires. Pour effectuer la transition d’un client existant, utilisez les API de mise à niveau du produit pour suivre les étapes suivantes :

* [Vérifier si le client est éligible pour une transition vers le plan Azure](get-eligibility-for-product-upgrade.md)
* [Lancer une mise à niveau du produit pour le client](create-product-upgrade-entity.md)
* [Vérifier l’état d’une mise à niveau de produit](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Dépenses Azure

Vous pouvez suivre les [dépenses Azure](azure-spending.md) en interrogeant le résumé de l’utilisation et les enregistrements d’utilisation détaillée à l’aide des méthodes suivantes :

* [Obtenir le récapitulatif d’utilisation de partenaire](get-a-partner-usage-summary.md)
* [Obtenir tous les enregistrements d’utilisation de client d’un partenaire](get-a-customer-s-usage-records.md)
* [Obtenir le récapitulatif d’utilisation de client](get-a-customer-usage-summary.md)
* [Obtenir tous les enregistrements d’utilisation d’abonnement d’un client](get-a-customer-subscription-s-usage-records.md)
* [Obtenir le récapitulatif d’utilisation d’abonnement](get-a-customer-subscription-usage-summary.md)
* [Obtenir les données d’utilisation d’abonnement par ressource](get-a-customer-subscription-resource-usage-records.md)
* [Obtenir les données d’utilisation d’abonnement par compteur](get-a-customer-subscription-meter-usage-records.md)
* [Obtenir les ressources d’enregistrement d’utilisation d’un compteur](meter-usage-resources.md)
* [Obtenir les ressources d’enregistrement d’utilisation d’une ressource](resource-usage-resources.md)

Vous pouvez également définir et gérer le budget d’utilisation du client à l’aide des méthodes suivantes :

* [Obtenir le budget d’utilisation d’un client](get-a-customer-s-usage-spending-budget.md)
* [Mettre à jour le budget d’utilisation d’un client](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Facture et rapprochement

Vous pouvez gérer les factures et les données de réconciliation à l’aide des méthodes suivantes :

* [Obtenir une collection de factures](get-a-collection-of-invoices.md)
* [Obtenir des liens d’estimation de facture](get-invoice-estimate-links.md)
* [Obtenir une facture par ID](get-invoice-by-id.md)
* [Obtenir l’instruction de facture](get-invoice-statement.md)
* [Obtenir des récapitulatifs de facture](get-invoice-summaries.md)
* [Obtenir les éléments de ligne de consommation facturés](get-invoice-billed-consumption-lineitems.md)
* [Obtenir les éléments de ligne de consommation non facturés](get-invoice-unbilled-consumption-lineitems.md)
* [Obtient les Articles de ligne de rapprochement facturés](get-invoiceline-items.md)
* [Obtenir les éléments de ligne de rapprochement non facturés](get-invoice-unbilled-recon-lineitems.md)
