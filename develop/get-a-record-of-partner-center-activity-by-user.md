---
title: Obtenir un enregistrement de l’activité espace partenaires
description: Comment obtenir un enregistrement des opérations effectuées par un utilisateur ou une application partenaire sur une période donnée.
ms.assetid: C24054DA-3E31-4BCD-BEB5-085564C20C58
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: aa140c4deb71e4660078ac4f9496da3a834b2f0e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416753"
---
# <a name="get-a-record-of-partner-center-activity"></a>Obtenir un enregistrement de l’activité espace partenaires


**S’applique à**

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir un enregistrement des opérations effectuées par un utilisateur ou une application partenaire sur une période donnée.

Utilisez cette API pour récupérer les enregistrements d’audit des 30 jours précédents à partir de la date actuelle, ou pour une plage de dates spécifiée en incluant la date de début et/ou la date de fin. Notez, toutefois, que pour des raisons de performances, la disponibilité des données du journal d’activité est limitée aux 90 jours précédents. Les demandes avec une date de début supérieure à 90 jours avant la date actuelle recevront une exception de demande incorrecte (code d’erreur : 400) et un message approprié.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour récupérer un enregistrement des opérations de l’espace partenaires, commencez par établir la plage de dates pour les enregistrements que vous souhaitez récupérer. L’exemple de code qui suit utilise uniquement une date de début, mais vous pouvez également inclure une date de fin. Pour plus d’informations, consultez la méthode [**query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) . Créez ensuite les variables dont vous avez besoin pour le type de filtre que vous souhaitez appliquer et assignez les valeurs appropriées. Par exemple, pour filtrer par sous-chaîne du nom de la société, créez une variable qui contiendra la sous-chaîne. Pour filtrer par ID de client, créez une variable qui contiendra l’ID.

Dans l’exemple suivant, un exemple de code est fourni pour filtrer par une sous-chaîne de nom de société, un ID de client ou un type de ressource. Choisissez-en un et commentez les autres. Dans chaque cas, vous instanciez d’abord un objet [**SimpleFieldFilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) à l’aide de son [**constructeur**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) par défaut pour créer le filtre. Vous devez passer une chaîne qui contient le champ à rechercher et l’opérateur approprié à appliquer, comme indiqué. Vous devez également fournir la chaîne de filtrage.

Ensuite, utilisez la propriété [**AuditRecords**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) pour obtenir une interface pour auditer les opérations d’enregistrement, puis appelez la méthode [**query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) ou [**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) pour exécuter le filtre et obtenir la collection de [**AuditRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) qui représente la première page du résultat. Vous devez passer à la méthode la date de début, une date de fin facultative non utilisée dans l’exemple ici et un objet [**IQueryable**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery) qui représente une requête sur une entité. L’objet IQueryable est créé en passant le filtre créé ci-dessus à la méthode [**BuildSimpleQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) [**de QueryFactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .

Une fois que vous avez la page initiale des éléments, utilisez la méthode [**enumerates. AuditRecords. Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) pour créer un énumérateur que vous pouvez utiliser pour itérer au sein des pages restantes.

``` csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (e.g. "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1"; 
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource. 
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }
     
    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **dossier**d’exemples du kit de développement logiciel (SDK) Partner Center : audit

## <a name="span-idrequestspan-idrequestspan-idrequest-rest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/> demande REST


**Syntaxe de la requête**

| Méthode  | URI de demande                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/AuditRecords ? StartDate = {StartDate} http/1.1                                                                                                     |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/AuditRecords ? StartDate = {startDate} & EndDate = {ENDDATE} http/1.1                                                                                   |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/AuditRecords ? StartDate = {startDate} & EndDate = {endDate} & filter = {"Field" : "CompanyName", "value" : "{searchSubstring}", "opérateur" : "SUBSTRING"} http/1.1 |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/AuditRecords ? StartDate = {startDate} & EndDate = {endDate} & filter = {"Field" : "CustomerID", "value" : "{CustomerID}", "opérateur" : "Equals"} http/1.1          |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/AuditRecords ? StartDate = {startDate} & EndDate = {endDate} & filter = {"Field" : "ResourceType", "value" : "{ResourceType}", "opérateur" : "Equals"} http/1.1      |

 

**Paramètre URI**

Utilisez les paramètres de requête suivants lors de la création de la demande.

| Nom      | Type   | Obligatoire | Description                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startDate | date   | Non       | Date de début au format aaaa-mm-jj. Si aucune valeur n’est fournie, le jeu de résultats est défini par défaut sur 30 jours avant la date de la demande. Ce paramètre est facultatif lorsqu’un filtre est fourni.                                          |
| endDate   | date   | Non       | Date de fin au format aaaa-mm-jj. Ce paramètre est facultatif lorsqu’un filtre est fourni. Lorsque la date de fin est omise ou définie sur null, la demande retourne la fenêtre Max ou utilise la date de fin du jour, selon la valeur la plus petite. |
| filtre    | chaîne | Non       | Filtre à appliquer. Il doit s’agir d’une chaîne encodée. Ce paramètre est facultatif lorsque la date de début ou la date de fin sont fournies.                                                                                              |

 

**Syntaxe de filtre** Vous devez composer le paramètre de filtre sous la forme d’une série de paires clé-valeur séparées par des virgules. Chaque clé et valeur doit être placée individuellement entre guillemets et séparés par un signe deux-points. Le filtre entier doit être encodé.

Un exemple non encodé ressemble à ceci :

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

Le tableau suivant décrit les paires clé-valeur requises :

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Clé</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Champ</td>
<td>Champ à filtrer. Les valeurs prises en charge se trouvent dans la syntaxe de la <a href="#request">requête</a>.</td>
</tr>
<tr class="even">
<td>Valeur</td>
<td>Valeur par laquelle filtrer. La casse de la valeur est ignorée. Les paramètres de valeur suivants sont pris en charge, comme indiqué dans la syntaxe de la <a href="#request">requête</a>:
<ul>
<li><p>searchSubstring : remplacez par le nom de la société. Vous pouvez entrer une sous-chaîne correspondant à une partie du nom de la société (par exemple, &quot;BRI&quot; correspond &quot;Fabrikam, Inc.&quot;).</p>
<p>Exemple : &quot;valeur&quot;:&quot;BRI&quot;</p></li>
<li><p>customerId-remplacez par une chaîne au format GUID qui représente l’identificateur du client.</p>
<p>Exemple : &quot;valeur&quot;:&quot;0c39d6d5-c70d-4C55-BC02-f620844f3fd1&quot;</p></li>
<li><p>resourceType : remplacez par le type de ressource pour lequel récupérer les enregistrements d’audit (par exemple, abonnement). Les types de ressources disponibles sont définis dans <a href="https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype"><strong>resourceType</strong></a>.</p>
<p>Exemple : &quot;valeur&quot;: abonnement&quot;&quot;</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>Opérateur</td>
<td>Opérateur à appliquer. Les opérateurs pris en charge se trouvent dans la syntaxe de la <a href="#request">requête</a>.</td>
</tr>
</tbody>
</table>

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes Rest du centre du composant](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST


En cas de réussite, cette méthode retourne un ensemble d’activités qui répondent aux critères des filtres.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




