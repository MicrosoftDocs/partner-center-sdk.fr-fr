---
title: Obtenir toutes les informations analytiques sur les revendeurs indirects
description: Obtention des informations d’analyse des revendeurs indirects.
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4a8bf1a958b28b5ea8c471a3bbee9009243f7455
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157771"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Obtenir toutes les informations analytiques sur les revendeurs indirects

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir toutes les informations d’analyse des revendeurs indirects pour vos clients.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête |
|---------|-------------|
| **GET** | baseURL/Partner/v1/Analytics/indirectresellers http/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>Paramètres URI

<table>
<thead>
    <th>Paramètre</th>
    <th>Type</th>
    <th>Description</th>
</thead>
<tbody>
    <tr>
        <td>partnerTenantId</td>
        <td>string</td>
        <td>ID de locataire du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. </td>
    </tr>
    <tr>
        <td>id</td>
        <td>string</td>
        <td>ID de revendeur indirect</td>
    </tr>
    <tr>
        <td>name</td>
        <td>string</td>
        <td>Nom du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects.</td>
    </tr>
    <tr>
        <td>market</td>
        <td>string</td>
        <td>Le marché du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects.</td>
    </tr>
    <tr>
        <td>firstSubscriptionCreationDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>Date de création du premier abonnement basé sur lequel vous souhaitez récupérer les données des revendeurs indirects.</td>
    </tr>
    <tr>
        <td>latestSubscriptionCreationDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>Date de création du dernier abonnement.</td>
    </tr>
    <tr>
        <td>firstSubscriptionEndDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>La première fois qu’un abonnement est terminé.</td>
    </tr>
    <tr>
        <td>latestSubscriptionEndDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>Dernière date de fin d’un abonnement. </td>
    </tr>
    <tr>
        <td>firstSubscriptionSuspendedDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>La première fois qu’un abonnement a été suspendu.</td>
    </tr>
    <tr>
        <td>latestSubscriptionSuspendedDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>Date la plus récente à laquelle un abonnement a été suspendu.</td>
    </tr>
    <tr>
        <td>firstSubscriptionDeprovisionedDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>La première fois qu’un abonnement a été annulé.</td>
    </tr>
    <tr>
        <td>latestSubscriptionDeprovisionedDate</td>
        <td>Chaîne au format date/heure UTC</td>
        <td>Date la plus récente de l’annulation de l’approvisionnement d’un abonnement.</td>
    </tr>
    <tr>
        <td>subscriptionCount</td>
        <td>double</td>
        <td>Nombre d’abonnements pour tous les revendeurs à valeur ajoutée</td>
    </tr>
    <tr>
        <td>licenseCount</td>
        <td>double</td>
        <td>Nombre de licences pour tous les revendeurs à valeur ajoutée</td>
    </tr>
    <tr>
        <td>indirectResellerCount</td>
        <td>double</td>
        <td>Nombre de revendeurs indirects</td>
    </tr>
    <tr>
        <td>top</td>
        <td>string</td>
        <td>Le nombre de lignes de données à renvoyer dans la requête. La valeur maximale et la valeur par défaut en l’absence de définition est 10000. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données.</td>
    </tr>
    <tr>
        <td>skip</td>
        <td>int</td>
        <td>
          <p>Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, <code>top=10000 and skip=0</code> récupère les 10000 premières lignes de données, <code>top=10000 and skip=10000</code> récupère les 10000 lignes de données suivantes, et ainsi de suite.</p>
        </td>
    </tr>
    <tr>
        <td>Filter</td>
        <td>string</td>
        <td>
            <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction comporte un champ et une valeur qui sont associés aux opérateurs <strong>eq</strong> ou <strong>ne</strong>, et les instructions peuvent être combinées à l’aide des opérateurs <strong>and</strong> ou <strong>or</strong>. Vous pouvez spécifier les champs suivants :</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>id</em></li>
                <li><em>Nom</em></li>
                <li><em>négoci</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p><strong>Exemple :</strong></br>
              <code>.../indirectresellers?filter=market eq &#39;US&#39;</code></p>
            <p><strong>Exemple :</strong></br>
                <code>.../indirectresellers?filter=market eq &#39;US&#39; or (firstSubscriptionCreationDate le cast(&#39;2018-01-01&#39;,Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast(&#39;2018-04-01&#39;,Edm.DateTimeOffset))</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>aggregationLevel</td>
        <td>string</td>
        <td><p>Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agit des chaînes suivantes : &quot;day&quot;, &quot;week&quot; ou &quot;month&quot;. Par défaut, la valeur est &quot;day&quot;.</p>
        <p><code>aggregationLevel</code>n’est pas pris <code>aggregationLevel</code>en charge sans. <code>aggregationLevel</code>s’applique à tous les <strong>datefields</strong> présents dans le<code>aggregationLevel</code></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>string</td>
        <td>
            <p>Instruction qui classe les valeurs des données de résultat pour chaque installation. La syntaxe est <code>...&orderby=field[order],field [order],...</code>. Le paramètre field peut comporter l’une des chaînes suivantes :</p>
            <ul>
                <li>&quot;partnerTenantId&quot;</li>
                <li>&quot;id&quot;</li>
                <li>&quot;name&quot;</li>
                <li>&quot;négoci&quot;</li>
                <li>&quot;firstSubscriptionCreationDate&quot;</li>
                <li>&quot;latestSubscriptionCreationDate&quot;</li>
                <li>&quot;firstSubscriptionEndDate&quot;</li>
                <li>&quot;latestSubscriptionEndDate&quot;</li>
                <li>&quot;firstSubscriptionSuspendedDate&quot;</li>
                <li>&quot;latestSubscriptionSuspendedDate&quot;</li>
                <li>&quot;firstSubscriptionDeprovisionedDate&quot;</li>
                <li>&quot;latestSubscriptionDeprovisionedDate&quot;</li>
                <li>&quot;subscriptionCount&quot;</li>
                <li>&quot;licenseCount&quot;</li>
            </ul>
            <p>Le paramètre <em>Order</em> est facultatif et peut être <code>asc</code> ou ; <code>desc</code> pour spécifier l’ordre croissant ou décroissant pour chaque champ. Par défaut, il s’agit de <code>asc</code>.</p>
            <p><strong>Exemple :</strong></br>
                <code>...&orderby=market,subscriptionCount</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>groupby</td>
        <td>string</td>
        <td>
            <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>id</em></li>
                <li><em>Nom</em></li>
                <li><em>négoci</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p>Les lignes de données retournées contiennent les champs <code>groupby</code> spécifiés dans la clause et les champs suivants :</p>
            <ul>
                <li><em>indirectResellerCount</em></li>
                <li><em>licenseCount</em></li>
                <li><em>subscriptionCount</em></li>
            </ul>
            <p>Le <code>groupby</code> paramètre peut être utilisé avec le <code>aggregationLevel</code> paramètre.</p>
            <p><strong>Exemple :</strong></br>
                <code>...&groupby=ageGroup,market&aggregationLevel=week</code>
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
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Response REST

En cas de réussite, le corps de la réponse contient une collection de ressources de [revendeurs indirects](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>Voir aussi

- [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)
