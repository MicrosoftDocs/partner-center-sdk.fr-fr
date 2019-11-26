---
title: Ressources du panier
description: Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a9fb1c81cae0e7efa0a5e84d2b4d93e44ce7efb9
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489079"
---
# <a name="cart-resources"></a>Ressources du panier

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.

## <a name="cart"></a>Caddie

Décrit un panier.

| Propriété              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | chaîne           | Identificateur de panier qui est fourni lors de la création réussie du panier.                               |
| creationTimeStamp     | DateTime         | Date à laquelle le panier a été créé, au format date/heure. Appliqué en cas de réussite de la création du panier.      |
| lastModifiedTimeStamp | DateTime         | Date de la dernière mise à jour du panier, au format date/heure. Appliqué en cas de réussite de la création du panier. |
| expirationTimeStamp   | DateTime         | Date d’expiration du panier, au format date/heure. Appliqué en cas de réussite de la création du panier.          |
| lastModifiedUser      | chaîne           | Utilisateur qui a mis à jour le panier pour la dernière fois. Appliqué en cas de réussite de la création du panier.                          |
| LineItems             | Tableau d’objets | Tableau de ressources [CartLineItem](#cartlineitem) .                                                   |
| status                | chaîne           | État du panier. Les valeurs possibles sont « active » (peut être mise à jour/envoyée) et « ordered » (a déjà été envoyé). |

## <a name="cartlineitem"></a>CartLineItem

Représente un élément contenu dans un panier.

| Propriété             | Type                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | chaîne                           | Identificateur unique pour un élément de ligne de panier. Appliqué en cas de réussite de la création du panier.                                                                   |
| catalogItemId        | chaîne                           | Identificateur de l’élément de catalogue.                                                                                                                          |
| friendlyName         | chaîne                           | Facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.                                                                 |
| quantity             | entier                              | Nombre de licences ou d’instances.                                                                                                                  |
| currencyCode         | chaîne                           | Code de la devise.                                                                                                                                    |
| billingCycle         | Objet                           | Type de cycle de facturation défini pour la période actuelle.                                                                                                 |
| termDuration         | chaîne                           | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont P1M (1 mois), P1Y (1 an) et P3Y (3 ans).                                |
| participants         | Liste de paires de chaînes d’objets      | Collection de partenaire sur l’enregistrement (MPNID) sur l’achat.                                                                                          |
| provisioningContext  | Dictionary < String, String >       | Contexte supplémentaire utilisé lors de la configuration de l’élément acheté. Pour déterminer les valeurs nécessaires pour un élément particulier, reportez-vous à la propriété provisioningVariables de la référence. |
| orderGroup           | chaîne                           | Groupe pour indiquer les éléments qui peuvent être envoyés ensemble dans le même ordre.                                                                          |
| addonItems           | Liste d’objets **CartLineItem** | Collection d’éléments de ligne de panier pour les modules complémentaires qui seront achetés pour l’abonnement de base qui résulte de l’achat de l’élément de ligne de panier racine. |
| erreur                | Objet                           | Appliqué après la création du panier en cas d’erreur.                                                                                                    |
| RenewsTo             | Tableau d’objets                 | Tableau de ressources [RenewsTo](#renewsto) .                                                                            |

## <a name="renewsto"></a>RenewsTo

Représente un élément contenu dans un élément de ligne de panier.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | chaîne           | Non              | Représentation ISO 8601 de la durée du terme de renouvellement. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an). |

## <a name="carterror"></a>CartError

Représente une erreur qui se produit après la création d’un panier.

| Propriété         | Type                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CartErrorCode](#carterrorcode) | Type d’erreur de panier.                                                                       |
| errorDescription | chaîne                                 | Description de l’erreur, y compris les remarques sur les valeurs prises en charge, les valeurs par défaut ou les limites. |

## <a name="carterrorcode"></a>CartErrorCode

[Énumération](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent un type d’erreur de panier.

| Valeur                                | Position | Description                                             |
|--------------------------------------|----------|---------------------------------------------------------|
| Inconnu                              | 0        | Valeur par défaut.                                          |
| CurrencyIsNotSupported               | 10000    | La devise n’est pas prise en charge pour le marché spécifié. |
| CatalogItemIdIsNotValid              | 10001    | L’ID d’élément de catalogue n’est pas valide.                       |
| QuotaNotAvailable                    | 10002    | Le quota disponible est insuffisant.                    |
| InventoryNotAvailable                | 10003    | L’inventaire n’est pas disponible pour l’offre sélectionnée.  |
| ParticipantsIsNotSupportedForPartner | 10004    | La définition des participants n’est pas prise en charge pour ce partenaire. |
| UnableToProcessCartLineItem          | 10006    | Impossible de traiter l’élément de ligne de panier.                   |
| SubscriptionIsNotValid               | 10007    | L’abonnement n’est pas valide.                          |
| SubscriptionIsNotEnabledForRI        | 10008    | L’abonnement n’est pas activé pour les réservations Azure. |
| SandboxLimitExceeded                 | 10009    | La limite du bac à sable (sandbox) a été dépassée.                    |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Représente le résultat d’une extraction de panier.

| Propriété    | Type                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| o.f.      | Liste d’objets de [commande](order-resources.md#order) .         | Collection de commandes.       |
| orderErrors | Liste d’objets [OrderError](#ordererror) . | Collection d’erreurs de commande. |

## <a name="ordererror"></a>OrderError

Représente une erreur qui se produit pendant l’extraction d’un panier lors de la création d’une commande.

| Propriété     | Type   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | chaîne | ID du groupe de commandes avec l’erreur. |
| code         | entier    | Code d’erreur.                                 |
| description  | chaîne | Description de l’erreur.                   |

## <a name="ordererrorcode"></a>OrderErrorCode

[Énumération](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent un type d’erreur de commande.

| Valeur | Position | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Jeton de partenaire manquant dans le contexte de la requête. |
| InvalidInput | 800002 | Entrée de demande non valide. |
| ServiceException | 800003 | Erreur de service inattendue. |
| InvalidOfferId | 800004 | ID d’offre non valide. |
| CreateOrderError | 800005 | Échec de la création d’une commande. |
| ProvisioningStatusNotFound | 800007 | Impossible de récupérer les informations de configuration. |
| CartIdNotFound | 800008 | Impossible de récupérer l’ID du panier. |
| CartItemErrorInCreateOrder | 800009 | Erreur dans le ou les éléments du panier. |
| InventoryNotAvailable | 800010 | L’inventaire n’est pas disponible pour cet élément de catalogue. |
| AzureSubscriptionNotValid | 800011 | Cet abonnement n’est pas un abonnement Azure valide. |
| SubscriptionIsNotActive | 800012 | Cet abonnement n’est pas un abonnement actif. |
| SubscriptionIsNotEnabledForRI | 800013 | Cet abonnement n’est pas activé pour l’achat RI. |
| PendingAdjustment | 800014 | Une modification en attente est demandée pour cette commande. |
| MpnIdNotFound | 800015 | ID MPN introuvable. |
| NotValidIndirectResellerMpnId | 800016 | L’ID MPN n’est pas un revendeur indirect valide. |
| InvalidQuantity | 800017 | La quantité n’est pas disponible pour cet élément de catalogue. |
| SandboxLimitExceeded | 800018 | La limite du bac à sable (sandbox) a été respectée. |
| SandboxTenantOnly | 800019 | Cette opération est uniquement activée pour les locataires sandbox. |
| CatalogItemNotEligibleForPurchase | 800020 | L’élément du catalogue ne peut pas être acheté. |
| SubscriptionIsNotValid | 800021 | Cet abonnement n’est pas un abonnement valide. |
| ManualReviewRequired | 800022 | Vous pouvez être éligible pour cette transaction. Veuillez contacter le support technique pour obtenir de l’aide.|
| InsufficientFunds | 800023 | Vous n’êtes pas éligible à cette transaction, car votre ligne de crédit n’atteint pas le seuil minimal pour cet achat. Veuillez mettre à jour votre commande (ou) Contacter le support technique pour obtenir de l’aide. |
| ReviewCancelled | 800024 | Vous n’êtes pas éligible pour cette transaction. |
| LineOfCreditNotDefined | 800025 | Vous n’êtes pas éligible à cette transaction, car votre ligne de crédit n’atteint pas le seuil minimal pour cet achat. Veuillez mettre à jour votre commande (ou) Contacter le support technique pour obtenir de l’aide. |
| RiskError | 800026 | Vous n’êtes pas éligible pour cette transaction. |
| SubscriptionNotRegistered | 800030 | Cet abonnement n’est pas inscrit. |
| PurchaseSystemNotSupported | 800031 | Le système d’achat n’est pas pris en charge. |
| ConditionFailed | 800036 | Échec de la condition préalable. |
| AssetIdNotFound | 800037 | ID d’élément multimédia introuvable. |
| AssetFutureBillingInfoNotFound | 800038 | FutureBillingInfo de ressource introuvable. |
| ResellerProgramStatusNotActive | 800039 | L’état du programme du revendeur n’est pas actif. |
| AssetStatusChangeNotValid | 800040 | L’état de la ressource ne peut pas être remplacé par **{0}** à partir de **{1}** . |
| ItemAlreadyActivated | 800041 | Cet élément a déjà été activé. |
| NotSupported | 800042 | Non pris en charge. |
| PricingAccessForbidden | 800043 | L’accès aux informations de tarification n’est pas accordé. |
| OrderInProgress | 800060 | Votre commande est en cours. Veuillez consulter l’historique des commandes récemment en quelques minutes. |
| OrderCannotBeCancelled | 800061 | Impossible d’annuler l’ordre. |
| ReviewRejected | 800062 | Vous n’êtes pas éligible pour cette transaction. |
| CancelLegacyOrder | 800063 | Impossible d’annuler cette commande **{0}** . Utilisez `PATCH /customers/{1}/subscriptions/<subscriptionId>` pour suspendre les abonnements. |
| CartProcessedByAnotherRequest | 800064 | Le **{0}** du panier est en cours de traitement par une autre demande. |
| CartCheckOutNotAllowedWhenStatusIsOrdered | 800065 | Impossible d’extraire une **{0}** de panier déjà soumise. |
