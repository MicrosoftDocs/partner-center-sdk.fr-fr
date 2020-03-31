---
title: Analyse de l’espace partenaires
description: Documentation sur l’API publique de l’analyse de l’espace partenaires.
ms.assetid: B605C1CD-FC40-4393-8588-55C8F0CAA51A
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6cb716010afa61f60f2eb5d7b3f56c4bc9f46adc
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416426"
---
# <a name="partner-center-analytics---resources"></a>Analyse de l’espace partenaires-Ressources

**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


L’API Analytics vous permet d’accéder par programmation aux données qui sont présentées dans l’expérience utilisateur. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ces scénarios prennent uniquement en charge l’authentification avec les informations d’identification de l’utilisateur.


## <a name="span-idazure_usage_analyticsspan-idazure_usage_analyticsspan-idazure_usage_analyticscsp-program-azure-usage-analytics"></a><span id="Azure_Usage_Analytics"/><span id="azure_usage_analytics"/>programme CSP <span id="AZURE_USAGE_ANALYTICS"/>: analyse de l’utilisation Azure

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations d’analyse de l’utilisation Azure de l’espace partenaires.  

- [Obtenir toutes les informations analytiques sur l’utilisation d’Azure](get-all-azure-usage-analytics.md)  

Ce scénario retourne vos informations d’analyse dans une collection de ressources d' [utilisation Azure](#azure_usage) . 

## <a name="span-idazure_usagespan-idazure_usagespan-idazure_usageazure-usage-resource"></a><span id="Azure_Usage"/><span id="azure_usage"/><span id="AZURE_USAGE"/>ressource d’utilisation Azure

Représente toutes les données analytiques pour l’utilisation d’Azure.

| Propriété | Type | Description |
|----------|------|-------------|
| CustomerTenantId | chaîne | Identificateur du locataire du client. |
| customerName | chaîne | Nom du client. |
| subscriptionId | chaîne | Identificateur d’abonnement. |
| subscriptionName | chaîne | Nom de l’abonnement. |
| usageDate | chaîne | Date d’utilisation. |
| resourceLocation | chaîne | Emplacement du centre de données, Europe de l’Ouest, par exemple. |
| MeterCategory | chaîne | Catégorie du compteur, gestion des données, par exemple. |
| meterSubcategory | chaîne | Sous-catégorie de compteur, par exemple géo-redondante. |
| meterUnit | chaîne | Unité de mesure, telle que gigaoctets ou heures. | 
| ReservationOrderId | chaîne | Ordre de réservation d’une instance réservée de machine virtuelle Azure. |
| reservationId | chaîne | Instances réservées dans un ordre RI spécifique. |
| serviceType | chaîne | Indique le type de machine virtuelle. Par exemple, Standard_E4s_v3. |
| quantity | long | Indique les nombres utilisés dans l’unité de mesure. |


## <a name="span-idindirect_resellers_analyticsspan-idindirect_resellers_analyticsspan-idindirect_resellers_analyticscsp-program-indirect-resellers-analytics"></a>programme CSP <span id="Indirect_Resellers_Analytics"/><span id="indirect_resellers_analytics"/><span id="INDIRECT_RESELLERS_ANALYTICS"/>: analyse des revendeurs indirects

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations analytiques des revendeurs indirects de l’espace partenaires.  

- [Obtenir toutes les informations analytiques sur les revendeurs indirects](get-all-indirect-resellers-analytics.md)  

Ce scénario retourne vos informations d’analyse dans une collection de ressources de [revendeurs indirects](#indirect_resellers) . 


## <a name="span-idindirect_resellersspan-idindirect_resellersspan-ididirect_resellersindirect-resellers-resource"></a><span id="Indirect_Resellers"/><span id="indirect_resellers"/><span id="IDIRECT_RESELLERS"/>ressource des revendeurs indirects

Représente toutes les données analytiques des revendeurs indirects.

| Propriété | Type | Description |
|----------|------|-------------|
| partnerTenantId | chaîne | ID de locataire du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. |
| id | chaîne | ID de revendeur indirect. |
| nom | chaîne | Nom du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. |
| market | chaîne | Le marché du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. |
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


## <a name="span-idsubscription_analyticsspan-idsubscription_analyticsspan-idsubscription_analyticscsp-program-subscription-analytics"></a><span id="Subscription_Analytics"/><span id="subscription_analytics"/><span id="SUBSCRIPTION_ANALYTICS"/>programme CSP : analyse d’abonnement

Les scénarios suivants vous montrent comment utiliser l’API Analytics pour récupérer toutes vos informations d’analyse d’abonnements de l’espace partenaires, les filtrer avec une requête de recherche, ou les regrouper par dates ou termes.  

- [Obtenir toutes les informations analytiques sur l’abonnement](get-all-subscription-analytics.md)  
- [Obtenir des informations analytiques d’abonnement filtrées par une requête de recherche](get-subscription-analytics-by-search-query.md)  
- [Obtenir des informations analytiques d’abonnement regroupées par dates ou périodes](get-subscription-analytics-grouped-by-dates-or-terms.md)  

Tous ces scénarios retournent les informations analytiques dans une collection de ressources d' [abonnement](#subscription) . 


## <a name="span-idsubscriptionspan-idsubscriptionspan-idsubscriptionsubscription-resource"></a><span id="Subscription"/><span id="subscription"/><span id="SUBSCRIPTION"/>ressource d’abonnement


Représente toutes les données analytiques d’un abonnement.


|         Propriété          |              Type              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     CustomerTenantId      |             chaîne             |                                              Chaîne au format GUID qui identifie le locataire client.                                              |
|       customerName        |             chaîne             |                                                               Nom du client.                                                                |
|      customerMarket       |             chaîne             |                                                 Pays/région dans lequel le client fait des affaires.                                                 |
|            id             |             chaîne             |                                                              Identificateur d’abonnement.                                                              |
|          statut           |             chaîne             |                                          État de l’abonnement : « actif », « suspendu » ou « mis hors service ».                                           |
|        productName        |             chaîne             |                                                                Le nom du produit.                                                                |
|     subscriptionType      |             chaîne             |       Type d’abonnement. **Remarque**: ce champ respecte la casse. Les valeurs prises en charge sont : « Office », « Azure », « Microsoft365 », « Dynamics », « EMS ».       |
|     autoRenewEnabled      |            booléen             |                                         Valeur indiquant si l’abonnement est renouvelé automatiquement.                                          |
|         Partenaire         |             chaîne             | ID MPN. Pour un revendeur direct, il s’agit de l’ID MPN du partenaire. Pour un revendeur indirect, il s’agit de l’ID MPN du revendeur indirect. |
|       friendlyName        |             chaîne             |                                                             Nom de l'abonnement.                                                              |
|        partnerName        |             chaîne             |                                              Nom du partenaire pour lequel l’abonnement a été acheté                                               |
|       providerName        |             chaîne             |            Lorsque la transaction d’abonnement est destinée au revendeur indirect, le nom du fournisseur est le fournisseur indirect qui a acheté l’abonnement.             |
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

## <a name="span-idsearch_analyticsspan-idsearch_analyticsspan-idsearch_analyticssearch-analytics"></a><span id="Search_Analytics"/><span id="search_analytics"/><span id="SEARCH_ANALYTICS"/>analytique de recherche

> [!NOTE]  
> L’appartenance au programme CSP n’est pas requise pour recevoir des analyses de recherche.

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations analytiques de recherche de l’espace partenaires.  

- [Obtenir toutes les informations analytiques sur la recherche](get-all-search-analytics.md)  

Ce scénario retourne vos informations d’analyse dans une collection de ressources de [recherche](#search_resource) . 


## <a name="span-idsearch_resourcespan-idsearch_resourcespan-idsearch_resourcesearch-resource"></a><span id="Search_Resource"/><span id="search_resource"/><span id="SEARCH_RESOURCE"/>la ressource de recherche

Représente toutes les données analytiques pour une recherche.

| Propriété | Type | Description |  
|----------|------|-------------|  
| Prennent | chaîne | Nom de la société de facturation. |
| contactButtonClicked | Booléen | Indique si l’utilisateur a cliqué sur le bouton contact. |
| keywordCountry | chaîne | Pays spécifié dans la recherche. |
| detailsViewed | Booléen | Indique si les détails de la recherche ont été affichés. |
| keywordIndustryFocus | chaîne | Secteur dans lequel rechercher, par exemple, la santé. |
| mpnId | chaîne | ID d’Microsoft Partner Network (MPN). Pour un revendeur direct, il s’agit de l’ID MPN du partenaire. Pour un revendeur indirect, il s’agit de l’ID MPN du revendeur indirect. |
| partnerMarket | chaîne | Paramètres régionaux dans lesquels le partenaire entreprend une activité. |
| keywordProduct | chaîne | Le produit spécifié dans la recherche. |
| referralSubmitted | Booléen | Indique si une référence a été envoyée. |
| searchDate | Chaîne au format date/heure UTC | Date à laquelle la requête de recherche s’est produite. |
| keywordSearchText | chaîne | Texte spécifié dans la recherche. |
| searchResultPageViews | long | Nombre de fois où le partenaire est apparu dans le résultat de la recherche. Partie d’une réponse uniquement sur l’agrégation.
| contactClicks | long | Nombre de clics effectués sur le bouton du contact. Partie d’une réponse uniquement sur l’agrégation.
| referralCount | long | Nombre de références générées à partir de la recherche. Partie d’une réponse uniquement sur l’agrégation.
| profileViews | long | Nombre d’affichages du profil de partenaire. Partie d’une réponse uniquement sur l’agrégation.


## <a name="span-idreferral_analyticsspan-idreferral_analyticsspan-idreferral_analyticsreferrals-analytics"></a><span id="Referral_Analytics"/><span id="referral_analytics"/><span id="REFERRAL_ANALYTICS"/>analytiques de références

> [!NOTE]  
> L’appartenance au programme CSP n’est pas requise pour l’analyse des références.

Le scénario suivant vous montre comment utiliser l’API Analytics pour récupérer toutes les informations d’analyse des références de l’espace partenaires.  

- [Obtenir toutes les informations analytiques sur les références](get-all-referrals-analytics.md)  

Ce scénario retourne vos informations d’analyse dans une collection de ressources de [références](#referrals) . 

> [!NOTE]  
> Les analyses de références ne sont pas disponibles pour l’espace partenaires géré par 21Vianet. 


## <a name="span-idreferralsspan-idreferralsspan-idreferralsreferrals-resource"></a><span id="Referrals"/><span id="referrals"/><span id="REFERRALS"/>ressources de références

Représente toutes les données analytiques pour une référence.

| Propriété | Type | Description |
|----------|------|-------------|
| id | chaîne | Identificateur du locataire du client.  |
| statut | chaîne | Indique si la référence a abouti à un client.  |
| customerMarket | chaîne | Pays/région dans lequel le client fait des affaires. |
| customerName | chaîne | Nom du client. |
| customerOrgSize | chaîne | Plage indiquant le nombre d’employés dans l’organisation du client. Par exemple, « 10to50employees ». |
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
| partnerMarket | chaîne |  Pays/région dans lequel le partenaire fait des affaires. |  
