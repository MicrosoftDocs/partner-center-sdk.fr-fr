---
title: Obtenir toutes les informations analytiques sur l’utilisation d’Azure
description: Obtention de toutes les informations d’analyse de l’utilisation d’Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6302a2223bbb9c56943b04175a9cba44db1d1d2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095235"
---
# <a name="get-all-azure-usage-analytics-information"></a>Obtenir toutes les informations analytiques sur l’utilisation d’Azure

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtention de toutes les informations d’analyse de l’utilisation d’Azure pour vos clients.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête |
|---------|-------------|
| **GET** | [* \{ BASEURL \} *](partner-center-rest-urls.md)/Partner/v1/Analytics/usage/Azure http/1.1 |

### <a name="uri-parameters"></a>Paramètres d’URI

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
        <p>string</p>
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
        <p>int</p>
      </td>
      <td>
        <p>Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, <code>top=10000 and skip=0</code> récupère les 10000 premières lignes de données, <code>top=10000 and skip=10000</code> récupère les 10000 lignes de données suivantes, et ainsi de suite.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>Filter</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction contient un champ et une valeur associés aux <strong> <code>eq</code> </strong> <strong> <code>ne</code> </strong> opérateurs ou, et les instructions peuvent être combinées à l’aide <strong> <code>and</code> </strong> de ou de <strong> <code>or</code> </strong> . Vous pouvez spécifier les éléments suivants :</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p><strong>Exemple :</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39;</code>
        </p>
        <p><strong>Exemple :</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39; or (usageDate le cast(&#39;2018-01-01&#39;, Edm.DateTimeOffset) and usageDate le cast(&#39;2018-04-01&#39;, Edm.DateTimeOffset))</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>aggregationLevel</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agir de l’une des chaînes suivantes : <code>day</code> , <code>week</code> ou <code>month</code> . S’il n’est pas spécifié, la valeur par défaut est <code>day</code> .</p>
      <p>Le <code>aggregationLevel</code> paramètre n’est pas pris en charge sans <code>groupby</code> . Le <code>aggregationLevel</code> paramètre s’applique à tous les champs de date présents dans le <code>groupby</code> .</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>orderby</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>Instruction qui classe les valeurs des données de résultat pour chaque installation. La syntaxe est <code>...&orderby=field [order],field [order],...</code>. Le <code>field</code> paramètre peut être l’une des chaînes suivantes :</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p>Le paramètre <em>Order</em> est facultatif et peut avoir <code>asc</code> la <code>desc</code> valeur ou ; pour spécifier l’ordre croissant ou décroissant pour chaque champ, respectivement. Par défaut, il s’agit de <code>asc</code>.</p>
        <p><strong>Exemple :</strong><br/>
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>groupby</code></p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p>Les lignes de données retournées contiennent les champs spécifiés dans le <code>groupby</code> paramètre ainsi que la <em>quantité</em>.</p>
        <p>Le <code>groupby</code> paramètre peut être utilisé avec le <code>aggregationLevel</code> paramètre.</p>
        <p><strong>Exemple :</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources d' [utilisation Azure](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

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

## <a name="see-also"></a>Voir aussi

- [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)
