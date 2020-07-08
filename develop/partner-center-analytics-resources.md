---
title: Analytique de l’Espace partenaires
description: Documentation sur l’API publique de l’analyse de l’espace partenaires.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094711"
---
# <a name="partner-center-analytics---resources"></a>Analytique de l’Espace partenaires - Ressources

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’API Analytics vous permet d’accéder par programmation aux données qui sont présentées dans l’expérience utilisateur.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ces scénarios prennent uniquement en charge l’authentification avec les informations d’identification de l’utilisateur.

## <a name="csp-program-azure-usage-analytics"></a>Programme CSP : analyse de l’utilisation Azure

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations d’analyse de l’utilisation Azure de l’espace partenaires.

- [Obtenir toutes les informations analytiques sur l’utilisation d’Azure](get-all-azure-usage-analytics.md)

Ce scénario retourne vos informations d’analyse dans une collection de ressources d' [utilisation Azure](#azure-usage-resource) .

## <a name="azure-usage-resource"></a>Ressource d’utilisation Azure

Représente toutes les données analytiques pour l’utilisation d’Azure.

| Propriété | Type | Description |
|----------|------|-------------|
| CustomerTenantId | string | Identificateur du locataire du client. |
| customerName | string | Nom du client. |
| subscriptionId | string | Identificateur de l’abonnement. |
| subscriptionName | string | Nom de l’abonnement. |
| usageDate | string | Date d’utilisation. |
| resourceLocation | string | Emplacement du centre de données, Europe de l’Ouest, par exemple. |
| meterCategory | string | Catégorie du compteur, gestion des données, par exemple. |
| meterSubcategory | string | Sous-catégorie de compteur, par exemple géo-redondante. |
| meterUnit | string | Unité de mesure, telle que gigaoctets ou heures. |
| reservationOrderId | string | Ordre de réservation d’une instance réservée de machine virtuelle Azure. |
| reservationId | string | Instances réservées dans un ordre RI spécifique. |
| serviceType | string | Indique le type de machine virtuelle. Par exemple, Standard_E4s_v3. |
| quantité | long | Indique les nombres utilisés dans l’unité de mesure. |

## <a name="csp-program-indirect-resellers-analytics"></a>Programme CSP : analytique des revendeurs indirects

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations analytiques des revendeurs indirects de l’espace partenaires.

- [Obtenir toutes les informations analytiques sur les revendeurs indirects](get-all-indirect-resellers-analytics.md)

Ce scénario retourne vos informations d’analyse dans une collection de ressources de [revendeurs indirects](#indirect-resellers-resource) .

## <a name="indirect-resellers-resource"></a>Ressource des revendeurs indirects

Représente toutes les données analytiques des revendeurs indirects.

| Propriété | Type | Description |
|----------|------|-------------|
| partnerTenantId | string | ID de locataire du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. |
| id | string | ID de revendeur indirect. |
| name | string | Nom du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. |
| market | string | Le marché du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. |
| firstSubscriptionCreationDate | Chaîne au format date/heure UTC | Date de création du premier abonnement basé sur lequel vous souhaitez récupérer les données des revendeurs indirects. |
| latestSubscriptionCreationDate | Chaîne au format date/heure UTC | Date de création du dernier abonnement. |
| firstSubscriptionEndDate | Chaîne au format date/heure UTC | La première fois qu’un abonnement est terminé. |
| latestSubscriptionEndDate | Chaîne au format date/heure UTC | Dernière date de fin d’un abonnement. |
| firstSubscriptionSuspendedDate | Chaîne au format date/heure UTC | La première fois qu’un abonnement a été suspendu. |
| latestSubscriptionSuspendedDate | Chaîne au format date/heure UTC | Date la plus récente à laquelle un abonnement a été suspendu. |
| firstSubscriptionDeprovisionedDate | Chaîne au format date/heure UTC | La première fois qu’un abonnement a été annulé. |
| latestSubscriptionDeprovisionedDate | Chaîne au format date/heure UTC | Date la plus récente de l’annulation de l’approvisionnement d’un abonnement. |
| subscriptionCount | double | Nombre d’abonnements pour tous les revendeurs à valeur ajoutée |
| licenseCount | double | Nombre de licences pour tous les revendeurs à valeur ajoutée |
| indirectResellerCount | double | Nombre de revendeurs indirects |

## <a name="csp-program-subscription-analytics"></a>Programme CSP : analyse d’abonnement

Les scénarios suivants vous montrent comment utiliser l’API Analytics pour récupérer toutes vos informations d’analyse d’abonnements de l’espace partenaires, les filtrer avec une requête de recherche, ou les regrouper par dates ou termes.

- [Obtenir toutes les informations analytiques sur l’abonnement](get-all-subscription-analytics.md)
- [Obtenir des informations analytiques d’abonnement filtrées par une requête de recherche](get-subscription-analytics-by-search-query.md)
- [Obtenir des informations analytiques d’abonnement regroupées par dates ou périodes](get-subscription-analytics-grouped-by-dates-or-terms.md)

Tous ces scénarios retournent les informations analytiques dans une collection de ressources d' [abonnement](#subscription-resource) .

## <a name="subscription-resource"></a>Ressource d’abonnement

Représente toutes les données analytiques d’un abonnement.

|         Propriété          |              Type              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             string             |                                              Chaîne au format GUID qui identifie le locataire client.                                              |
|       customerName        |             string             |                                                               Nom du client.                                                                |
|      customerMarket       |             string             |                                                 Pays/région dans lequel le client fait des affaires.                                                 |
|            id             |             string             |                                                              Identificateur de l’abonnement.                                                              |
|          status           |             string             |                                          État de l’abonnement : « actif », « suspendu » ou « mis hors service ».                                           |
|        ProductName        |             string             |                                                                Nom du produit.                                                                |
|     subscriptionType      |             string             |       Type d’abonnement. **Remarque**: ce champ respecte la casse. Les valeurs prises en charge sont : « Office », « Azure », « Microsoft365 », « Dynamics », « EMS ».       |
|     autoRenewEnabled      |            boolean             |                                         Valeur indiquant si l’abonnement est renouvelé automatiquement.                                          |
|         Partenaire         |             string             | ID MPN. Pour un revendeur direct, ce paramètre sera l’ID MPN du partenaire. Pour un revendeur indirect, ce paramètre correspond à l’ID MPN du revendeur indirect. |
|       friendlyName        |             string             |                                                             Nom de l'abonnement.                                                              |
|        partnerName        |             string             |                                              Nom du partenaire pour lequel l’abonnement a été acheté                                               |
|       providerName        |             string             |            Lorsque la transaction d’abonnement est destinée au revendeur indirect, le nom du fournisseur est le fournisseur indirect qui a acheté l’abonnement.             |
|    effectiveStartDate     | Chaîne au format date/heure UTC |                                                           Date de début de l’abonnement.                                                            |
|     commitmentEndDate     | Chaîne au format date/heure UTC |                                                            Date de fin de l’abonnement.                                                             |
|    currentStateEndDate    | Chaîne au format date/heure UTC |                                           Date à laquelle l’état actuel de l’abonnement sera modifié.                                            |
| trialToPaidConversionDate | Chaîne au format date/heure UTC |                                 Date à laquelle l’abonnement convertit de l’essai au paiement. La valeur par défaut est null.                                 |
|      trialStartDate       | Chaîne au format date/heure UTC |                                Date de début de la période d’évaluation de l’abonnement. La valeur par défaut est null.                                 |
|       trialEndDate        | Chaîne au format date/heure UTC |                                  Date de fin de la période d’évaluation de l’abonnement. La valeur par défaut est null.                                  |
|       lastUsageDate       | Chaîne au format date/heure UTC |                                        Date à laquelle l’abonnement a été utilisé pour la dernière fois. La valeur par défaut est null.                                        |
|     deprovisionedDate     | Chaîne au format date/heure UTC |                                      Date à laquelle l’abonnement a été annulé. La valeur par défaut est null.                                      |
|      lastRenewalDate      | Chaîne au format date/heure UTC |                                       Date à laquelle l’abonnement a été renouvelé pour la dernière fois la valeur par défaut est null.                                       |
|       licenseCount        |             nombre             |                                                             Nombre total de licences.                                                              |
|     subscriptionCount     |             nombre             |                        Nombre d’abonnements. Remarque : cette valeur s’affiche uniquement dans la réponse d’une requête d’agrégation.                         |

## <a name="search-analytics"></a>Analyse de recherche

> [!NOTE]
> L’appartenance au programme CSP n’est pas nécessaire pour recevoir des analyses de recherche.

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations analytiques de recherche de l’espace partenaires.

- [Obtenir toutes les informations analytiques sur la recherche](get-all-search-analytics.md)

Ce scénario retourne vos informations d’analyse dans une collection de ressources de [recherche](#search-resource) .

## <a name="search-resource"></a>Rechercher une ressource

Représente toutes les données analytiques pour une recherche.

| Propriété | Type | Description |
|----------|------|-------------|
| companyName | string | Nom de la société de facturation. |
| contactButtonClicked | Boolean | Indique si l’utilisateur a cliqué sur le bouton contact. |
| keywordCountry | string | Pays spécifié dans la recherche. |
| detailsViewed | Boolean | Indique si les détails de la recherche ont été affichés. |
| keywordIndustryFocus | string | Secteur dans lequel rechercher, par exemple, la santé. |
| mpnId | string | ID d’Microsoft Partner Network (MPN). Pour un revendeur direct, ce paramètre sera l’ID MPN du partenaire. Pour un revendeur indirect, ce paramètre correspond à l’ID MPN du revendeur indirect. |
| partnerMarket | string | Paramètres régionaux dans lesquels le partenaire entreprend une activité. |
| keywordProduct | string | Le produit spécifié dans la recherche. |
| referralSubmitted | Boolean | Indique si une référence a été envoyée. |
| searchDate | Chaîne au format date/heure UTC | Date à laquelle la requête de recherche s’est produite. |
| keywordSearchText | string | Texte spécifié dans la recherche. |
| searchResultPageViews | long | Nombre de fois où le partenaire est apparu dans le résultat de la recherche. Partie d’une réponse uniquement sur l’agrégation.
| contactClicks | long | Nombre de clics effectués sur le bouton du contact. Partie d’une réponse uniquement sur l’agrégation.
| referralCount | long | Nombre de références générées à partir de la recherche. Partie d’une réponse uniquement sur l’agrégation.
| profileViews | long | Nombre d’affichages du profil de partenaire. Partie d’une réponse uniquement sur l’agrégation.

## <a name="referrals-analytics"></a>Analyse des références

> [!NOTE]
> L’appartenance au programme CSP n’est pas requise pour l’analyse des références.

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations d’analyse des références de l’espace partenaires.

- [Obtenir toutes les informations analytiques sur les références](get-all-referrals-analytics.md)

Ce scénario retourne vos informations d’analyse dans une collection de ressources de [références](#referrals-resource) .

> [!NOTE]
> Les analyses de références ne sont pas disponibles pour l’espace partenaires géré par 21Vianet.

## <a name="referrals-resource"></a>Ressource de références

Représente toutes les données analytiques pour une référence.

| Propriété | Type | Description |
|----------|------|-------------|
| id | string | Identificateur du locataire du client.  |
| status | string | Indique si la référence a abouti à un client.  |
| customerMarket | string | Pays/région dans lequel le client fait des affaires. |
| customerName | string | Nom du client. |
| customerOrgSize | string | Plage indiquant le nombre d’employés dans l’organisation du client. Par exemple, « 10to50employees ». |
| acceptedDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été acceptée. |
| acknowledgedDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été reconnue. |
| archivedDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été archivée. |
| declinedDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été refusée. |
| expiredDate | Chaîne au format date/heure UTC | Date à laquelle la référence a expiré. |
| lostDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été perdue. |
| missedDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été manquée. |
| createdDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été créée. |
| skippedDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été ignorée. |
| wonDate | Chaîne au format date/heure UTC | Date à laquelle la référence a été remportée. |
| partnerMarket | string |  Pays/région dans lequel le partenaire fait des affaires. |
