---
title: Acheter des réservations Azure
description: Vous pouvez acheter des réservations Azure pour un client à l’aide de l’API espace partenaires via votre abonnement Microsoft Azure existant (MS-AZR-0145P) ou un plan Azure.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c09f65ae5105a74be41a7ec45824e3889217a1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096185"
---
# <a name="purchase-azure-reservations"></a>Acheter des réservations Azure

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud for US Government

Pour acheter une réservation Azure pour un client à l’aide de l’API de l’espace partenaires, vous devez disposer d’un abonnement Microsoft Azure (**MS-AZR-0145P**) existant ou d’un plan Azure.

> [!NOTE]
> Les réservations Azure ne sont pas disponibles dans les marchés suivants :
>
> | Marchés non disponibles            | Marchés non disponibles (suite...) | Marchés non disponibles (suite...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Åland (îles d’)                  | Groenland                         | Papouasie-Nouvelle-Guinée                         |
> | Samoa américaines                 | Grenade                           | Pitcairn (îles)                         |
> | Andorre                        | Guadeloupe                        | Réunion (île)                                  |
> | Anguilla                       | Guam                              | Fédération de Russie                       |
> | Antarctique                     | Guernesey                          | Saba                                     |
> | Antigua-et-Barbuda            | Guinée                            | Saint-Barthélemy                         |
> | Aruba                          | Guinée-Bissau                     | Sainte-Lucie                              |
> | Bénin                          | Guyane                            | Saint-Martin                             |
> | Bhoutan                         | Haïti                             | Saint-Pierre-et-Miquelon                |
> | Bonaire                        | Heard et McDonald (Îles) | Saint-Vincent-et-les Grenadines         |
> | Bouvet (Île)                  | Man (Île de)                       | Samoa                                    |
> | Brésil                         | Jan Mayen                         | Saint-Marin                               |
> | Territoires britanniques de l’océan Indien | Jersey                            | São Tomé et Príncipe                    |
> | Îles Vierges britanniques         | Kiribati                          | Seychelles                               |
> | Burkina-Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Saint-Eustache                           |
> | Cambodge                       | Lesotho                           | Saint-Martin (partie néerlandaise)                             |
> | République centrafricaine       | Liberia                           | Salomon (Îles)                          |
> | Tchad                           | Madagascar                        | Somalie                                  |
> | Chine                          | Malawi                            | Géorgie du Sud et les îles Sandwich du Sud |
> | Christmas (île)               | Maldives                          | Soudan du Sud                              |
> | Cocos-Keeling (îles)        | Mali                              | Sainte-Hélène, Ascension et Tristan da Cunha   |
> | Comores (Les)                        | Marshall (îles)                  | Suriname                                 |
> | Congo                          | Martinique                        | Svalbard                                 |
> | Congo (RDC)                    | Mauritanie                        | Swaziland                                |
> | Cook (îles)                   | Mayotte                           | Timor-Leste                              |
> | Djibouti                       | Micronésie                        | Togo                                     |
> | Dominique                       | Montserrat                        | Tokelau                                  |
> | Guinée équatoriale              | Mozambique                        | Tonga                                    |
> | Érythrée                        | Myanmar                           | Turks et Caicos (îles)                 |
> | Malouines (îles)               | Nauru                             | Tuvalu                                   |
> | Guyane française                  | Nouvelle-Calédonie                     | États-Unis Îles mineures éloignées                    |
> | Polynésie française               | Niger                             | Vanuatu                                  |
> | Terres australes françaises    | Niue                              | État de la Cité du Vatican                             |
> | Gabon                          | Norfolk (île)                    | Wallis-et-Futuna                        |
> | Gambie                         | Mariannes du Nord (îles)          | Yémen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- ID d’abonnement pour un abonnement Azure CSP actif ou un plan Azure.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Comment acheter des réservations de Microsoft Azure

Une fois que vous avez identifié l’abonnement Azure CSP actif auquel vous souhaitez ajouter une réservation Azure, procédez comme suit pour l’acheter :

1. [Activation](#enablement) -inscrire un abonnement Azure CSP actif pour l’activer pour l’achat de réservations Azure.

2. [Détection](#discovery) : recherchez et sélectionnez les produits et les références SKU Azure que vous souhaitez acheter, puis vérifiez leur disponibilité.

3. [Soumission de commande](#order-submission) : créez un panier d’achat avec les Articles de votre commande et envoyez-le.

4. [Obtenir les détails](#get-order-details) de la commande-passez en revue les détails d’une commande, toutes les commandes pour un client ou afficher les commandes par type de cycle de facturation.

Une fois que vous avez acheté des réservations Azure, les scénarios suivants vous montrent comment gérer leur cycle de vie en obtenant des informations sur vos droits de réservation Azure et sur la façon de récupérer les relevés de solde, les factures et les résumés de facture.

- [Gestion du cycle de vie](#lifecycle-management)
- [Facture et rapprochement](#invoice-and-reconciliation)

## <a name="enablement"></a>Activation

L’activation consiste à associer un abonnement Microsoft Azure (**MS-AZR-0145P**) existant à une instance de machine virtuelle réservée Azure en inscrivant l’abonnement afin qu’il soit activé pour les réservations Azure. L’inscription est une condition préalable à l’achat de Azure Reserved VM Instances.

Un abonnement est nécessaire pour les raisons suivantes :

1. Pour vérifier si le client est autorisé à déployer des ressources et, par conséquent, à acheter Azure Reserved VM Instances dans une région.

2. Pour fournir une priorité de capacité pour les déploiements sur un abonnement. Cela s’applique uniquement à l’étendue unique Azure Reserved VM Instances avec l’option **priorité de capacité** sélectionnée.

Une fois que vous avez identifié l’abonnement actif auquel vous souhaitez ajouter la réservation Azure, vous devez inscrire l’abonnement afin qu’il soit activé pour les réservations Azure. Pour inscrire une ressource d' [abonnement](subscription-resources.md) existante afin qu’elle soit activée pour le tri des réservations Azure, consultez [inscrire un abonnement](register-a-subscription.md).

Après l’inscription de votre abonnement, vous devez vérifier que le processus d’inscription est terminé en vérifiant l’état de l’inscription. Pour ce faire, consultez [obtenir l’état de l’inscription de l’abonnement](get-subscription-registration-status.md).

> [!NOTE]
> Lorsque vous achetez Microsoft Azure réservation pour un client avec un plan Azure, vous devez d’abord inscrire le plan Azure. À l’instar d’un abonnement Microsoft Azure (**MS-AZR-0145P**), un plan Azure est représenté par une ressource d' [abonnement](subscription-resources.md) de l’espace partenaires. Par conséquent, vous pouvez utiliser la même méthode d’inscription d' [un abonnement](register-a-subscription.md) pour inscrire un plan Azure.

## <a name="discovery"></a>découverte,

Une fois l’abonnement activé pour l’achat des réservations Azure, vous êtes prêt à sélectionner les produits et références SKU et à vérifier leur disponibilité à l’aide des modèles d’API de l’espace partenaires suivants :

- [Produit](product-resources.md#product) : construction de regroupement pour les biens ou services pouvant être achetés. Un produit par lui-même n’est pas un élément pouvant être acheté.

- [Référence](product-resources.md#sku) (SKU), une unité de conservation de stock (SKU) achetée dans un produit. Celles-ci représentent les différentes formes du produit.

- [Disponibilité](product-resources.md#availability) : configuration dans laquelle une référence (SKU) est disponible à l’achat (par exemple, pays, devise et secteur).

Avant d’acheter une réservation Azure, procédez comme suit :

1. Identifiez et récupérez le produit et la référence (SKU) que vous souhaitez acheter. Pour ce faire, vous pouvez répertorier les produits et les références SKU en premier, ou si vous connaissez déjà les ID du produit et de la référence SKU, en les sélectionnant.

   - [Obtenir la liste de produits (par pays)](get-a-list-of-products.md)
   - [Obtenir un produit à l’aide de l’ID de produit](get-a-product-by-id.md)
   - [Obtenir la liste des références SKU d’un produit (par pays)](get-a-list-of-skus-for-a-product.md)
   - [Obtenir une référence SKU à l’aide de l’ID de référence](get-a-sku-by-id.md)

2. Vérifiez l’inventaire d’une référence (SKU). Cette étape n’est nécessaire que pour les références (SKU) marquées avec un prérequis **InventoryCheck** .

   - [Vérifier le stock](check-inventory.md)

3. Récupérez la [disponibilité](product-resources.md#availability) de la [référence SKU](product-resources.md#sku). Vous aurez besoin de la **CatalogItemId** de disponibilité lors de la mise en place de la commande. Pour ce faire, utilisez l’une des API suivantes :

   - [Obtenir la liste des disponibilités d’une référence SKU (par pays)](get-a-list-of-availabilities-for-a-sku.md)
   - [Procurez-vous une disponibilité à l’aide de l’ID de disponibilité](get-an-availability-by-id.md)

> [!IMPORTANT]
> Chaque Microsoft Azure produit de réservation a différents disponibilités pour l’abonnement Microsoft Azure (**MS-AZR-0145P**) et le plan Azure. Pour [obtenir la liste des produits (par pays)](get-a-list-of-products.md), ou [obtenir la liste des références (SKU) d’un produit (par pays)](get-a-list-of-skus-for-a-product.md), ou [obtenir la liste des disponibilités pour une référence (par pays)](get-a-list-of-availabilities-for-a-sku.md) qui s’appliquent uniquement au plan Azure, spécifiez le paramètre « reservationScope = AzurePlan ».

## <a name="order-submission"></a>Soumission de commande

Pour soumettre votre commande de réservation Azure, procédez comme suit :

1. Créez un panier pour stocker la collection d’éléments de catalogue que vous souhaitez acheter. Lorsque vous créez un [panier](cart-resources.md), les [éléments de ligne de panier](cart-resources.md#cartlineitem) sont automatiquement regroupés en fonction de ce qui peut être acheté ensemble dans le même [ordre](order-resources.md).

   - [Créer un panier d’achat](create-a-cart.md)
   - [Mettre à jour un panier d’achat](update-a-cart.md)

2. Consultez le panier. L’extraction d’un panier entraîne la création d’une [commande](order-resources.md).

   - [Extraire le panier](checkout-a-cart.md)

## <a name="get-order-details"></a>Recevoir les détails de la commande

Une fois que vous avez créé votre commande de réservation Azure, vous pouvez récupérer les détails d’une commande individuelle à l’aide de l’ID de commande ou obtenir la liste des commandes d’un client. Il y a un délai de 15 minutes entre le moment où une commande est soumise et le moment où elle apparaît dans une liste de commandes d’un client.

- Pour afficher les détails d’une commande individuelle à l’aide de l’ID de commande. Consultez [obtenir une commande par ID](get-an-order-by-id.md).

- Pour obtenir la liste des commandes d’un client à l’aide de l’ID client. Consultez [la page obtenir toutes les commandes d’un client](get-all-of-a-customer-s-orders.md).

- Pour obtenir la liste des commandes d’un client par [type de cycle de facturation](product-resources.md#billingcycletype) , ce qui vous permet de répertorier les commandes de réservation Azure (frais à usage unique) et les commandes annuelles ou mensuelles facturées séparément. Consultez [la page obtenir une liste de commandes par client et type de cycle de facturation](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Gestion du cycle de vie

Dans le cadre de la gestion du cycle de vie de vos réservations Azure dans l’espace partenaires, vous pouvez récupérer des informations sur vos [droits](entitlement-resources.md)de réservation Azure et obtenir des détails sur la réservation à l’aide de l’ID de commande de réservation. Pour obtenir des exemples d’utilisation, consultez [obtenir des droits](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Facture et rapprochement

Les scénarios suivants vous montrent comment afficher par programmation les [factures](invoice-resources.md)de votre client et obtenir les soldes et les résumés de votre compte qui incluent des frais à usage unique pour les réservations Azure.

### <a name="balance-and-payment"></a>Solde et paiement

Pour obtenir le solde actuel du compte dans votre type de devise par défaut qui correspond à un solde des frais périodiques et ponctuels (réservation Azure), consultez [obtenir le solde actuel de votre compte](get-the-reseller-s-current-account-balance.md)

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
