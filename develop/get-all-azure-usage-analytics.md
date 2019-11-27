---
title: Récupération de toutes les informations d’analyse d’utilisation Azure
description: Obtention de toutes les informations d’analyse de l’utilisation d’Azure.
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 49df0ac0741ed486ab34015b409eced7fde59afd
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485999"
---
# <a name="get-all-azure-usage-analytics-information"></a>Récupération de toutes les informations d’analyse d’utilisation Azure

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


Obtention de toutes les informations d’analyse de l’utilisation d’Azure pour vos clients. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête |
|---------|-------------|
| **Télécharger** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/Partner/v1/Analytics/usage/Azure http/1.1 |

 

**Paramètres d’URI**

<table>
  <thead>
      <th>
        <p>Paramètre</p>
      </th>
      <th>
        <p>Type</p>
      </th>
      <th>
        <p>Description</p>
      </th>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>top</p>
      </td>
      <td>
        <p>chaîne</p>
      </td>
      <td>
        <p>Le nombre de lignes de données à renvoyer dans la requête. La valeur maximale et la valeur par défaut en l’absence de définition est 10000. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>skip</p>
      </td>
      <td>
        <p>entier</p>
      </td>
      <td>
        <p>Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, <code>top=10000 and skip=0</code> récupère les 10000 premières lignes de données, <code>top=10000 and skip=10000</code> récupère les 10000 lignes de données suivantes, et ainsi de suite.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>filter</p>
      </td>
      <td>
        <p>chaîne</p>
      </td>
      <td>
        <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction comporte un champ et une valeur qui sont associés aux opérateurs <strong>eq</strong> ou <strong>ne</strong>, et les instructions peuvent être combinées à l’aide des opérateurs <strong>and</strong> ou <strong>or</strong>. Vous pouvez spécifier les champs suivants :</p>
        <ul>
          <li><em>customerTenantId</em></li>
          <li><em>Souhaite</em></li>
          <li><em>subscriptionId</em></li>
          <li><em>subscriptionName</em></li>
          <li><em>usageDate</em></li>
          <li><em>resourceLocation</em></li>
          <li><em>meterCategory</em></li>
          <li><em>meterSubcategory</em></li>
          <li><em>meterUnit</em></li>
          <li><em>reservationOrderId</em></li>
          <li><em>Réservation</em></li>
          <li><em>consumptionMeterId</em></li>
          <li><em>serviceType</em></li>
        </ul>
        <p><strong>Exemple :</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39;</code>
        </p>
        <p><strong>Exemple :</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39; or (usageDate le cast(&#39;2018-01-01&#39;, Edm.DateTimeOffset) and usageDate le cast(&#39;2018-04-01&#39;, Edm.DateTimeOffset))</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>aggregationLevel</p>
      </td>
      <td>
        <p>chaîne</p>
      </td>
      <td>
        <p>Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agit des chaînes suivantes : &quot;day&quot;, &quot;week&quot; ou &quot;month&quot;. Par défaut, la valeur est &quot;day&quot;.</p>
      <p>Le paramètre <em>aggregationLevel</em> n’est pas pris en charge sans <em>GroupBy</em>. Le paramètre <em>aggregationLevel</em> s’applique à tous les champs de date présents dans le <em>GroupBy</em>.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>orderby</p>
      </td>
      <td>
        <p>chaîne</p>
      </td>
      <td>
        <p>Une instruction qui commande les valeurs de données de résultats pour chaque installation. La syntaxe est <code>...&orderby=field [order],field [order],...</code> le paramètre <em>Field</em> peut être l’une des chaînes suivantes :</p>
        <ul>
          <li>&quot;customerTenantId&quot;</li>
          <li>&quot;customerName&quot;</li>
          <li>&quot;subscriptionId&quot;</li>
          <li>&quot;subscriptionName&quot;</li>
          <li>&quot;usageDate&quot;</li>
          <li>&quot;resourceLocation&quot;</li>
          <li>&quot;meterCategory&quot;</li>
          <li>&quot;meterSubcategory&quot;</li>
          <li>&quot;meterUnit&quot;</li>
          <li>&quot;reservationOrderId&quot;</li>
          <li>&quot;réservation&quot;</li>
          <li>&quot;consumptionMeterId&quot;</li>
          <li>&quot;serviceType&quot;</li>
        </ul>
        <p>Le paramètre <em>Order</em> est facultatif et peut être &quot;ASC&quot; ou &quot;DESC&quot; pour spécifier l’ordre croissant ou décroissant pour chaque champ, respectivement. La valeur par défaut est &quot;asc&quot;.</p>
        <p><strong>Exemple :</strong><br/> 
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>groupby</p>
      </td>
      <td>
        <p>chaîne</p>
      </td>
      <td>
        <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p>
        <ul>
          <li><em>customerTenantId</em></li>
          <li><em>Souhaite</em></li>
          <li><em>subscriptionId</em></li>
          <li><em>subscriptionName</em></li>
          <li><em>usageDate</em></li>
          <li><em>resourceLocation</em></li>
          <li><em>meterCategory</em></li>
          <li><em>meterSubcategory</em></li>
          <li><em>meterUnit</em></li>
          <li><em>reservationOrderId</em></li>
          <li><em>Réservation</em></li>
          <li><em>consumptionMeterId</em></li>
          <li><em>serviceType</em></li>
        </ul>
        <p>Les lignes de données retournées contiendront les champs spécifiés dans le paramètre <em>GroupBy</em> ainsi que la <em>quantité</em>.</p>
        <p>Le paramètre <em>groupby</em> peut être utilisé avec le paramètre <em>aggregationLevel</em>.</p>
        <p><strong>Exemple :</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>


**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, le corps de la réponse contient une collection de ressources d' [utilisation Azure](partner-center-analytics-resources.md#azure_usage) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20  
}
```


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>Voir aussi
  - [Analyse de l’espace partenaires-Ressources](partner-center-analytics-resources.md)

