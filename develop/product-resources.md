---
title: Ressources de produits
description: Ressources qui représentent des biens ou services pouvant être achetés. Comprend des ressources pour décrire le type de produit et la forme (référence SKU) et pour vérifier la disponibilité du produit dans un inventaire.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0474f2e7e089d8e637e18fa9bd7f77ffd5fb2f4e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097325"
---
# <a name="products-resources"></a>Ressources de produits

**S’applique à**

- Espace partenaires

Ressources qui représentent des biens ou services pouvant être achetés. Comprend des ressources pour décrire le type de produit et la forme (référence SKU) et pour vérifier la disponibilité du produit dans un inventaire.

## <a name="product"></a>Produit

Représente un service ou un service valide. Un produit par lui-même n’est pas un élément pouvant être acheté.

| Propriété           | Type                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | string                        | ID de ce produit.                                                 |
| title              | string                        | Titre du produit.                                                       |
| description        | string                        | Description du produit.                                                 |
| productType        | [ItemType](#itemtype)         | Objet qui décrit la ou les catégorisations de type de ce produit.     |
| isMicrosoftProduct | bool                          | Indique s’il s’agit d’un produit Microsoft.                          |
| publisherName      | string                        | Nom de l’éditeur du produit, le cas échéant.                          |
| liens              | [ProductLinks](#productlinks) | Liens de ressources contenus dans le produit.                         |

## <a name="itemtype"></a>itemType

Représente le type d’un produit.

| Propriété        | Type                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | string                        | Identificateur de type.                                                                 |
| displayName     | string                        | Nom complet de ce type.                                                      |
| subtype         | [ItemType](#itemtype)         | facultatif. Objet qui décrit une catégorisation de sous-type pour ce type d’élément.     |

## <a name="productlinks"></a>ProductLinks

Contient une liste de liens pour un [produit](#product).

| Propriété        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| x64            | [Lien](utility-resources.md#link)                             | Lien permettant d’accéder aux références (SKU) sous-jacentes.          |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressources contenus dans cette ressource.   |

## <a name="sku"></a>Sku

Représente une référence SKU (Stock Keeping Unit) sous un produit. Celles-ci représentent les différentes formes du produit.

| Propriété               | Type             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | string           | ID de cette référence (SKU). Cet ID est unique uniquement dans le contexte de son produit parent. |
| title                  | string           | Titre de la référence (SKU).                                                                 |
| description            | string           | Description de la référence (SKU).                                                           |
| productId              | string           | ID du [produit](#product) parent qui contient cette référence (SKU).                      |
| minimumQuantity        | int              | Quantité minimale autorisée pour l’achat.                                            |
| maximumQuantity        | int              | Quantité maximale autorisée pour l’achat.                                            |
| isTrial                | bool             | Indique si cette référence (SKU) est un élément d’évaluation.                                           |
| supportedBillingCycles | tableau de chaînes | Liste des cycles de facturation pris en charge pour cette référence (SKU). Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | tableau de chaînes | Liste des étapes ou actions requises avant l’achat de cet élément. Les valeurs prises en charge sont les suivantes :<br/>  « InventoryCheck »-indique que l’inventaire de l’élément doit être évalué avant toute tentative d’achat de cet élément.<br/> « AzureSubscriptionRegistration »-indique qu’un abonnement Azure est nécessaire et doit être inscrit avant de tenter d’acheter cet élément.  |
| inventoryVariables     | tableau de chaînes | Liste des variables nécessaires à l’exécution d’une vérification de stock sur cet élément. Les valeurs prises en charge sont les suivantes :<br/> « CustomerId » : ID du client pour lequel l’achat est destiné.<br/> « AzureSubscriptionId » : ID de l’abonnement Azure à utiliser pour l’achat d’une réservation Azure.</br> « ArmRegionName » : région pour laquelle vérifier l’inventaire. Cette valeur doit correspondre à la valeur « ArmRegionName » du DynamicAttributes de la référence (SKU). |
| provisioningVariables  | tableau de chaînes | Liste des variables qui doivent être fournies dans le contexte de provisionnement d’un [élément de ligne de panier](cart-resources.md#cartlineitem) lors de l’achat de cet article. Les valeurs prises en charge sont les suivantes :<br/> Étendue : étendue d’un achat de réservation Azure : « unique », « partagé ».<br/> « SubscriptionId » : ID de l’abonnement Azure à utiliser pour l’achat d’une réservation Azure.<br/> « Duration »-Durée de la réservation Azure : « 1Year », « 3Year ».  |
| dynamicAttributes      | paires clé/valeur  | Dictionnaire de propriétés dynamiques qui s’appliquent à cet élément. Notez que les propriétés de ce dictionnaire sont dynamiques et peuvent être modifiées sans préavis. Vous ne devez pas créer de fortes dépendances sur des clés particulières existantes dans la valeur de cette propriété.    |
| liens                  | [ResourceLinks](utility-resources.md#resourcelinks) | Liens de ressources contenus dans la référence (SKU).                   |

## <a name="availability"></a>Disponibilité

Représente une configuration dans laquelle une référence (SKU) est disponible à l’achat (par exemple, le pays, la devise et le secteur d’activité).

| Propriété        | Type                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | string                        | ID de cette disponibilité. Cet ID est unique uniquement dans le contexte de son [produit](#product) parent et de sa [référence SKU](#sku). **Remarque** Cet ID peut changer au fil du temps. Vous devez compter uniquement sur cette valeur dans un laps de temps bref après l’avoir récupérée.  |
| productId       | string                        | ID du [produit](#product) qui contient cette disponibilité.           |
| skuId           | string                        | ID de la [référence SKU](#sku) qui contient cette disponibilité.                   |
| catalogItemId   | string                        | Identificateur unique de cet élément dans le catalogue. Il s’agit de l’ID qui doit être rempli dans les propriétés [OrderLineItem. OfferID](order-resources.md#orderlineitem) ou [CartLineItem. CatalogItemId](cart-resources.md#cartlineitem) lors de l’achat de la [référence SKU](#sku)parente. **Remarque** Cet ID peut changer au fil du temps. Vous ne devez vous fier à cette valeur qu’au bout d’un bref laps de temps après l’avoir récupérée. Il ne doit être accessible et utilisé qu’au moment de l’achat.  |
| defaultCurrency | string                        | Devise par défaut prise en charge pour cette disponibilité.                               |
| segment         | string                        | Secteur d’activité pour cette disponibilité. Les valeurs prises en charge sont les suivantes : commercial, éducation, gouvernement, à but non lucratif. |
| country         | string                                              | Pays ou région (au format de code pays ISO) auquel cette disponibilité s’applique. |
| isPurchasable   | bool                                                | Indique si cette disponibilité est achetée. |
| isRenewable     | bool                                                | Indique si cette disponibilité est renouvelable. |
| product      | [Produit](#product)               | Produit auquel cette disponibilité correspond. |
| sku          | [Sku](#sku)            | Référence (SKU) à laquelle cette disponibilité correspond. |
| terms           | Tableau de ressources de [terme](#term)  | Collection des termes applicables à cette disponibilité. |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks) | Liens de ressources contenus dans la disponibilité. |

## <a name="term"></a>Terme

Représente un terme pour lequel la disponibilité peut être achetée.

| Propriété              | Type                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | string                                      | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont P1M (1 mois), P1Y (1 an) et P3Y (3 ans). |
| description           | string                                      | Description du terme.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Représente une demande de vérification de l’inventaire par rapport à certains éléments du catalogue.

| Propriété         | Type                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | Tableau de [InventoryItem](#inventoryitem)            | Liste des éléments de catalogue évalués par le contrôle d’inventaire.                           |
| inventoryContext | paires clé/valeur                                     | Dictionnaire des valeurs de contexte nécessaires pour effectuer le ou les chèques d’inventaire. Chaque [référence](#sku) des produits définit les valeurs (le cas échéant) nécessaires pour effectuer cette opération.  |
| liens            | [ResourceLinks](utility-resources.md#resourcelinks) | Liens de ressources contenus dans la demande de contrôle d’inventaire.                            |

## <a name="inventoryitem"></a>InventoryItem

Représente un élément unique dans une opération de contrôle d’inventaire. Cette ressource est utilisée pour spécifier les éléments cibles dans une demande d’entrée et est également utilisée pour représenter les résultats de sortie de l’opération de vérification d’inventaire.

| Propriété         | Type                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | string                                                            | Souhaitée ID du [produit](#product).                            |
| skuId            | string                                                            | ID de la [référence (SKU](#sku)). Lorsque vous utilisez cette ressource comme entrée pour une demande d’inventaire, cette valeur est facultative. Si cette valeur n’est pas fournie, toutes les références SKU sous le produit seront considérées comme des éléments cibles de l’opération de vérification d’inventaire.      |
| isRestricted     | bool                                                              | Indique si cet élément a été trouvé pour un inventaire restreint.            |
| restrictions     | Tableau de [InventoryRestriction](#inventoryrestriction)            | Détails des restrictions trouvées pour cet élément. Cette propriété est remplie uniquement si **isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Représente les détails d’une restriction d’inventaire. Cela s’applique uniquement aux résultats de la vérification de stock, et non aux demandes d’entrée.

| Propriété         | Type                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | string                | Code qui identifie la raison de la restriction.                                    |
| description      | string                | Description de la restriction d’inventaire.                                               |
| properties       | paires clé/valeur       | Dictionnaire de propriétés qui peut fournir des détails supplémentaires sur la restriction.           |

## <a name="billingcycletype"></a>BillingCycleType

[Énumération](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent un type de cycle de facturation.

| Valeur              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | Initialiseur Enum.                                                                          |
| Mensuelle            | 1            | Indique que le partenaire sera facturé chaque mois.                                        |
| Annuelle             | 2            | Indique que le partenaire sera facturé annuellement.                                       |
| None               | 3            | Indique que le partenaire ne sera pas facturé. Cette valeur peut être utilisée pour les éléments d’essai.    |
| OneTime            | 4            | Indique que le partenaire sera facturé une seule fois.                                       |
