---
title: Obtenir les enregistrements d’utilisation d’un client pour Azure
description: Vous pouvez utiliser l’API d’utilisation d’Azure pour obtenir les enregistrements d’utilisation de l’abonnement Azure d’un client pendant une période donnée.
ms.assetid: 0270DBEA-AAA3-46FB-B5F0-D72B9BAC3112
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3ee3f2187f0e4961a7945c865bbcb80b90a6cf4b
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155321"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Obtenir les enregistrements d’utilisation d’un client pour Azure

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez obtenir les enregistrements d’utilisation de l’abonnement Azure d’un client pendant une période donnée à l’aide de l’API d’utilisation d’Azure.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

- Identificateur d’abonnement.

Cette API renvoie une consommation non classée quotidienne et horaire pour un intervalle de temps arbitraire. Toutefois, *cette API n’est pas prise en charge pour les plans Azure*. Si vous disposez d’un plan Azure, consultez les articles [obtenir une facture facturation de la consommation non facturée](get-invoice-unbilled-consumption-lineitems.md) et obtenir les lignes de facturation de [la consommation facturées](get-invoice-billed-consumption-lineitems.md) . Ces articles décrivent comment obtenir une consommation évaluée à un niveau quotidien par compteur et par ressource. Cette consommation de taux est équivalente aux données de grain journalier fournies par l’API d’utilisation d’Azure. Vous devez utiliser l’identificateur de facture pour récupérer les données d’utilisation facturées. Ou vous pouvez utiliser les périodes actuelles et précédentes pour recevoir des estimations d’utilisation non facturées. *Les filtres horaires de données et de plage de dates arbitraires ne sont actuellement pas pris en charge pour les ressources d’abonnement de plan Azure*.

## <a name="azure-utilization-api"></a>API d’utilisation d’Azure

Cette API d’utilisation Azure fournit l’accès aux enregistrements d’utilisation pendant une période qui représente le moment où l’utilisation a été signalée dans le système de facturation. Il permet d’accéder aux mêmes données d’utilisation utilisées pour créer et calculer le fichier de réconciliation. Toutefois, il n’a pas connaissance de la logique du fichier de rapprochement du système de facturation. Vous ne devez pas vous attendre à ce que les résultats du résumé du fichier de rapprochement correspondent au résultat récupéré à partir de cette API pour la même période.

Par exemple, le système de facturation utilise les mêmes données d’utilisation et applique des règles de retard pour déterminer ce qui est comptabilisé dans un fichier de réconciliation. Quand une période de facturation se ferme, toute utilisation jusqu’à la fin de la journée à laquelle la période de facturation se termine est incluse dans le fichier de réconciliation. Toute utilisation tardive au cours de la période de facturation qui est signalée dans les 24 heures suivant la fin de la période de facturation est comptabilisée dans le prochain fichier de rapprochement. Pour connaître les règles de mise en retard de la facturation du partenaire, consultez [obtenir des données de consommation pour un abonnement Azure](https://docs.microsoft.com/previous-versions/azure/reference/mt219001(v=azure.100)).

Cette API REST est paginée. Si la charge utile de la réponse est supérieure à une page unique, vous devez suivre le lien suivant pour obtenir la page suivante des enregistrements d’utilisation.

## <a name="c"></a>C\#

Pour obtenir les enregistrements d’utilisation Azure :

1. Procurez-vous l’ID client et l’ID d’abonnement.

2. Appelez la méthode [**IAzureUtilizationCollection. Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) pour retourner un [**ResourceCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) qui contient les enregistrements d’utilisation.

3. Obtenez un énumérateur d’enregistrements d’utilisation Azure pour parcourir les pages d’utilisation. Cette étape est requise, car la collection de ressources est paginée.

- **Exemple**: [application de test](console-test-app.md) de la console
- **Projet**: exemples du kit de développement logiciel (SDK) Partner Center
- **Classe**: GetAzureSubscriptionUtilization.cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour obtenir les enregistrements d’utilisation Azure, vous avez d’abord besoin d’un identificateur de client et d’un identificateur d’abonnement. Vous appelez ensuite la fonction **IAzureUtilizationCollection. Query** pour retourner un **ResourceCollection** qui contient les enregistrements d’utilisation. La collection de ressources étant paginée, vous devrez alors récupérer un énumérateur d’enregistrements d’utilisation Azure pour parcourir ces pages.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour obtenir les enregistrements d’utilisation Azure, vous avez d’abord besoin d’un identificateur de client et d’un identificateur d’abonnement. Vous appelez ensuite le [**PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). Cette commande retourne tous les enregistrements disponibles pendant la période spécifiée.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête |
|------- | ----------- |
| **GET** | *{baseURL}*/v1/Customers/{Customer-tenant-ID}/subscriptions/{subscription-ID}/utilizations/Azure ? Start\_Time = {start-Time} &Time\_end = {end-Time} &Granularity = {granularité} &Show\_Details = {true} |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez le chemin d’accès et les paramètres de requête suivants pour obtenir les enregistrements d’utilisation.

| Nom | Type | Obligatoire | Description |
| ---- | ---- | -------- | ----------- |
| customer-tenant-id | string | Oui | Chaîne au format GUID qui identifie le client. |
| subscription-id | string | Oui | Chaîne au format GUID qui identifie l’abonnement. |
| start_time | chaîne au format de décalage de date/heure UTC | Oui | Début de l’intervalle de temps qui représente le moment où l’utilisation a été signalée dans le système de facturation. |
| end_time | chaîne au format de décalage de date/heure UTC | Oui | Fin de l’intervalle de temps qui représente le moment où l’utilisation a été signalée dans le système de facturation. |
| granularité | string | Non  | Granularité des agrégations d’utilisation. Les options disponibles sont `daily` les suivantes : ( `hourly`par défaut) et.
| show_details | boolean | Non  | Indique s’il faut récupérer les détails d’utilisation au niveau de l’instance. Par défaut, il s’agit de `true`. |
| taille | nombre | Non | Nombre d’agrégations retournées par un seul appel d’API. La valeur par défaut est 1000. Le maximum est 1000. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

L’exemple de requête suivant produit des résultats similaires à ce que le fichier de réconciliation affiche pour la période 7/2-8/1. Ces résultats peuvent ne pas correspondre exactement (consultez la section [API d’utilisation d’Azure](#azure-utilization-api) pour plus d’informations).

Cet exemple de requête retourne les données d’utilisation signalées dans le système de facturation entre 7/2 à 12h00 (UTC) et 8/2 à 12h00 (UTC).

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne une collection de ressources d' [enregistrements d’utilisation Azure](azure-utilization-record-resources.md) dans le corps de la réponse. Si les données d’utilisation Azure ne sont pas encore prêtes dans un système dépendant, cette méthode retourne le code d’état HTTP 204 avec un en-tête Retry-after.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de suivi réseau pour lire le code d’état HTTP, le [type de code d’erreur](error-codes.md)et des paramètres supplémentaires.

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
