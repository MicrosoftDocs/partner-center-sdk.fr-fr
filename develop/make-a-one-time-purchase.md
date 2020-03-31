---
title: Effectuer un achat ponctuel
description: Comment effectuer un achat unique des logiciels et des produits de réservation, tels que les abonnements logiciels, les logiciels perpétuelles et les instances de machines virtuelles réservées Azure, à l’aide de l’API espace partenaires.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c94afb2a8e1167bfad0dca8ab750fe209ad97436
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416520"
---
# <a name="make-a-one-time-purchase"></a>Effectuer un achat ponctuel

**S’applique à**

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud for US Government

Comment effectuer un achat unique des logiciels et des produits de réservation, tels que les abonnements logiciels, les logiciels perpétuelles et les instances de machines virtuelles réservées Azure, à l’aide de l’API espace partenaires.

> [!NOTE]  
> Les abonnements logiciels ne sont pas disponibles sur les marchés suivants :  
>  
> | Marchés non disponibles            | &nbsp;                            | &nbsp;                                   |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Åland (îles d’)                  | Groenland                         | Papouasie-Nouvelle-Guinée                         |
> | Samoa américaines                 | Grenade                           | Pitcairn (îles)                         |
> | Andorre                        | Guadeloupe                        | Réunion (île)                                  |
> | Anguilla                       | Guam                              | Fédération de Russie                       |
> | Antarctique                     | Guernesey                          | Saba                                     |
> | Antigua-et-Barbuda            | Guinée                            | Saint-Barthélemy                         |
> | Aruba                          | Guinée-Bissau                     | Sainte-Lucie                              |
> | Bénin                          | Guyana                            | Saint-Martin (partie française)                             |
> | Bhoutan                         | Haïti                             | Saint-Pierre-et-Miquelon                |
> | Bonaire                        | Heard et McDonald (Îles) | Saint-Vincent-et-les-Grenadines         |
> | Bouvet (Île)                  | Île de Man                       | Samoa                                    |
> | Brésil                         | Jan Mayen                         | Saint-Marin                               |
> | Territoires britanniques de l’océan Indien | Jersey                            | São Tomé et Príncipe                    |
> | Îles Vierges britanniques         | Kiribati                          | Seychelles                               |
> | Burkina-Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Saint-Eustache                           |
> | Cambodge                       | Lesotho                           | Saint-Martin (partie néerlandaise)                             |
> | République centrafricaine       | Liberia                           | Salomon (îles)                          |
> | Tchad                           | Madagascar                        | Somalie                                  |
> | Chine                          | Malawi                            | Géorgie du Sud et les îles Sandwich du Sud |
> | Christmas (île)               | Maldives                          | Soudan du Sud                              |
> | Cocos-Keeling (îles)        | Mali                              | Sainte-Hélène, Ascension et Tristan da Cunha   |
> | Comores (Les)                        | Marshall (îles)                  | Surinam                                 |
> | Congo                          | Martinique                        | Svalbard                                 |
> | Congo (RDC)                    | Mauritanie                        | Swaziland                                |
> | Cook (îles)                   | Mayotte                           | Timor-Leste                              |
> | Djibouti                       | Micronésie                        | Togo                                     |
> | Dominique                       | Montserrat                        | Tokelau                                  |
> | Guinée équatoriale              | Mozambique                        | Tonga                                    |
> | Érythrée                        | Myanmar                           | Turks et Caïcos (îles)                 |
> | Malouines (îles)               | Nauru                             | Tuvalu                                   |
> | Guyane française                  | Nouvelle-Calédonie                     | Îles mineures éloignées des États-Unis                    |
> | Polynésie française               | Niger                             | Vanuatu                                  |
> | Terres australes françaises    | Niue                              | État de la Cité du Vatican                             |
> | Gabon                          | Norfolk (île)                    | Wallis-et-Futuna                        |
> | Gambie                         | Mariannes du Nord (îles)          | Yémen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>  
&nbsp;
> [!NOTE]
> Pour acheter un logiciel perpétuel, vous devez avoir été préalablement qualifié. Pour plus d’informations, contactez le support.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client. Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="making-a-one-time-purchase"></a>Achat unique

Pour effectuer un achat unique, procédez comme suit :

1. [Activation](#enablement) -(instance de machine virtuelle réservée Azure uniquement) Inscrivez un abonnement Azure CSP actif pour l’activer pour l’achat d’un produit de réservation.
2. [Détection](#discovery) : recherchez et sélectionnez les produits et références SKU que vous souhaitez acheter, puis vérifiez leur disponibilité.
3. [Soumission de commande](#order-submission) : créez un panier d’achat avec les Articles de votre commande et envoyez-le.
4. [Obtenir les détails](#get-order-details) de la commande-passez en revue les détails d’une commande, toutes les commandes pour un client ou afficher les commandes par type de cycle de facturation.

Après avoir effectué votre achat unique, les scénarios suivants vous montrent comment gérer le cycle de vie de vos produits en obtenant des informations sur vos droits, ainsi que sur la façon de récupérer les relevés de solde, les factures et les résumés des factures.

- [Gestion du cycle de vie](#lifecycle-management)
- [Facture et rapprochement](#invoice-and-reconciliation)

## <a name="enablement"></a>Activation

Une fois que vous avez identifié l’abonnement actif auquel vous souhaitez ajouter l’instance de machine virtuelle réservée Azure, vous devez inscrire l’abonnement afin qu’il soit activé. Pour inscrire une ressource d' [abonnement](subscription-resources.md) existante afin qu’elle soit activée, consultez [inscrire un abonnement](register-a-subscription.md).

Après l’inscription de votre abonnement, vous devez vérifier que le processus d’inscription est terminé en vérifiant l’état de l’inscription. Pour ce faire, consultez [obtenir l’état de l’inscription de l’abonnement](get-subscription-registration-status.md).

## <a name="discovery"></a>Découverte

Une fois l’abonnement activé, vous êtes prêt à sélectionner les produits et références SKU et à vérifier leur disponibilité à l’aide des modèles d’API de l’espace partenaires suivants :

- [Produit](product-resources.md#product) : construction de regroupement pour les biens ou services pouvant être achetés. Un produit seul n’est pas un élément pouvant être acheté.
- [Référence](product-resources.md#sku) (SKU), une unité de conservation de stock (SKU) achetée dans un produit. Celles-ci représentent les différentes formes du produit.
- [Disponibilité](product-resources.md#availability) : configuration dans laquelle une référence (SKU) est disponible à l’achat (par exemple, pays, devise et secteur).

Avant d’effectuer un achat unique, procédez comme suit :

1. Identifiez et récupérez le produit et la référence (SKU) que vous souhaitez acheter. Pour ce faire, vous pouvez répertorier les produits et les références SKU en premier, ou si vous connaissez déjà les ID du produit et de la référence SKU, en les sélectionnant.

    - [Obtenir la liste des produits](get-a-list-of-products.md)
    - [Obtenir un produit à l’aide de l’ID de produit](get-a-product-by-id.md)
    - [Obtenir la liste des références SKU d’un produit](get-a-list-of-skus-for-a-product.md)
    - [Obtenir une référence SKU à l’aide de l’ID de référence](get-a-sku-by-id.md)

2. Vérifiez l’inventaire d’une référence (SKU). Cette étape n’est nécessaire que pour les références (SKU) marquées avec un prérequis **InventoryCheck** .

    - [Vérifier le stock](check-inventory.md)

3. Récupérez la [disponibilité](product-resources.md#availability) de la [référence SKU](product-resources.md#sku). Vous aurez besoin de la **CatalogItemId** de disponibilité lors de la mise en place de la commande. Pour ce faire, utilisez l’une des API suivantes :

    - [Obtenir la liste des disponibilités d’une référence SKU](get-a-list-of-availabilities-for-a-sku.md)
    - [Procurez-vous une disponibilité à l’aide de l’ID de disponibilité](get-an-availability-by-id.md)  

## <a name="order-submission"></a>Soumission de commande

Pour soumettre votre commande, procédez comme suit :

1. Créez un panier pour stocker la collection d’éléments de catalogue que vous souhaitez acheter. Lorsque vous créez un [panier](cart-resources.md), les [éléments de ligne de panier](cart-resources.md#cartlineitem) sont automatiquement regroupés en fonction de ce qui peut être acheté ensemble dans le même [ordre](order-resources.md).

    - [Créer un panier d’achat](create-a-cart.md)
    - [Mettre à jour un panier d’achat](update-a-cart.md)

2. Consultez le panier. L’extraction d’un panier entraîne la création d’une [commande](order-resources.md).

    - [Extraire le panier](checkout-a-cart.md)

## <a name="get-order-details"></a>Recevoir les détails de la commande

Une fois que vous avez créé votre commande, vous pouvez récupérer les détails d’une commande individuelle à l’aide de l’ID de commande ou obtenir la liste des commandes d’un client. Notez qu’il y a un délai de 15 minutes au maximum entre le moment où une commande est soumise et le moment où elle apparaîtra dans la liste des commandes d’un client.

- Pour afficher les détails d’une commande individuelle à l’aide de l’ID de commande. Consultez [obtenir une commande par ID](get-an-order-by-id.md).

- Pour obtenir la liste des commandes d’un client à l’aide de l’ID client. Consultez [la page obtenir toutes les commandes d’un client](get-all-of-a-customer-s-orders.md).

- Pour obtenir la liste des commandes d’un client par [type de cycle de facturation](product-resources.md#billingcycletype) , ce qui vous permet de répertorier les commandes (frais à usage unique) et les commandes annuelles ou mensuelles facturées séparément. Consultez [la page obtenir une liste de commandes par client et type de cycle de facturation](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Gestion du cycle de vie

Dans le cadre de la gestion du cycle de vie de vos achats à usage unique dans l’espace partenaires, vous pouvez récupérer des informations sur vos [habilitations](entitlement-resources.md)et obtenir des détails sur la réservation à l’aide de l’ID de commande de réservation. Pour obtenir des exemples d’utilisation, consultez [obtenir des droits](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Facture et rapprochement

Les scénarios suivants vous montrent comment afficher par programmation les [factures](invoice-resources.md)de votre client et obtenir les soldes et les résumés de votre compte qui incluent des frais à usage unique.  

**Solde et paiement** Pour obtenir le solde actuel du compte dans votre type de devise par défaut qui correspond à un solde des frais périodiques et ponctuels, consultez [obtenir le solde actuel de votre compte](get-the-reseller-s-current-account-balance.md)

**Solde et paiement à plusieurs devises** Pour obtenir le solde de votre compte actuel et un ensemble de résumés de facture contenant un résumé de facture avec des frais périodiques et ponctuels pour chacun des types de devise de votre client, consultez [obtenir des résumés de facture](get-invoice-summaries.md).

**Factures** Pour obtenir une collection de factures qui affichent des frais périodiques et ponctuels, consultez [obtenir une collection de factures](get-a-collection-of-invoices.md).

**Facture unique** Pour récupérer une facture spécifique à l’aide de l’ID de facture, consultez [obtenir une facture par ID](get-invoice-by-id.md).  

**Réconciliation** Pour obtenir une collection de détails sur les lignes de facturation (Articles de rapprochement) pour un ID de facture spécifique, consultez [obtenir des lignes de facturation](get-invoiceline-items.md).  

**Télécharger une facture au format PDF** Pour récupérer une déclaration de facture au format PDF à l’aide d’un ID de facture, consultez [obtenir une facture](get-invoice-statement.md).
