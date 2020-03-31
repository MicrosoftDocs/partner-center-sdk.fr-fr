---
title: Obtient toutes les informations d’analyse des revendeurs indirects
description: Obtention des informations d’analyse des revendeurs indirects.
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7e9de270c7619de51363b2226c6b8a79ac382ef4
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416147"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Obtient toutes les informations d’analyse des revendeurs indirects

**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


Comment obtenir toutes les informations d’analyse des revendeurs indirects pour vos clients. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de demande |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/Partner/v1/Analytics/indirectresellers http/1.1 |

 

**Paramètres d’URI**

<table>
<thead>
    <th>Paramètre</th>
    <th>Type</th>
    <th>Description</th>
</thead>
<tbody>
    <tr>
        <td>partnerTenantId</td>
        <td>chaîne</td>
        <td>ID de locataire du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects. </td>
    </tr>
    <tr>
        <td>id</td>
        <td>chaîne</td>
        <td>ID de revendeur indirect</td>
    </tr>
    <tr>
        <td>nom</td>
        <td>chaîne</td>
        <td>Nom du partenaire pour lequel vous souhaitez récupérer les données des revendeurs indirects.</td>
    </tr>
    <tr>
        <td>market</td>
        <td>chaîne</td>
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
        <td>chaîne</td>
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
        <td>filtre</td>
        <td>chaîne</td>
        <td>
            <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction comporte un champ et une valeur qui sont associés aux opérateurs <strong>eq</strong> ou <strong>ne</strong>, et les instructions peuvent être combinées à l’aide des opérateurs <strong>and</strong> ou <strong>or</strong>. Vous pouvez spécifier les champs suivants :</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>identifi</em></li>
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
            <p><strong>Exemple :</strong></br>
              <code>.../indirectresellers?filter=market eq &#39;US&#39;</code></p>
            <p><strong>Exemple :</strong></br>
                <code>.../indirectresellers?filter=market eq &#39;US&#39; or (firstSubscriptionCreationDate le cast(&#39;2018-01-01&#39;,Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast(&#39;2018-04-01&#39;,Edm.DateTimeOffset))</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>aggregationLevel</td>
        <td>chaîne</td>
        <td><p>Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agit des chaînes suivantes : &quot;day&quot;, &quot;week&quot; ou &quot;month&quot;. Par défaut, la valeur est &quot;day&quot;.</p>
        <p><em>aggregationLevel</em> n’est pas pris en charge sans <strong>GroupBy</strong>. <em>aggregationLevel</em> s’applique à toutes les <strong>datefields</strong> présentes dans le <strong>GroupBy</strong></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>chaîne</td>
        <td>
            <p>Une instruction qui commande les valeurs de données de résultats pour chaque installation. La syntaxe est <code>...&orderby=field[order],field [order],...</code> le paramètre Field peut être l’une des chaînes suivantes :</p>
            <ul>
                <li>&quot;partnerTenantId&quot;</li> 
                <li>ID de &quot;&quot;</li> 
                <li>&quot;name&quot;</li> 
                <li>&quot;marché&quot;</li> 
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
            <p>Le paramètre <em>order</em>, facultatif, peut comporter les valeurs &quot;asc&quot; ou &quot;desc&quot; afin de spécifier l’ordre croissant ou décroissant pour chaque champ. La valeur par défaut est &quot;asc&quot;.</p>
            <p><strong>Exemple :</strong></br> 
                <code>...&orderby=market,subscriptionCount</code>
            </p> 
        </td>
    </tr>
    <tr>
        <td>groupby</td>
        <td>chaîne</td>
        <td>
            <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>identifi</em></li>
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
            <p>Les lignes de données renvoyées comportent les champs spécifiés dans le paramètre <em>groupby</em>, ainsi que dans les paramètres suivants :</p>
            <ul>
                <li><em>indirectResellerCount</em></li>
                <li><em>licenseCount</em></li>
                <li><em>subscriptionCount</em></li>
            </ul>
            <p>Le paramètre <em>groupby</em> peut être utilisé avec le paramètre <em>aggregationLevel</em>.</p>
            <p><strong>Exemple :</strong></br>
                <code>...&groupby=ageGroup,market&aggregationLevel=week</code>
            </p>
        </td>
    </tr>
</tbody>
</table>
 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, le corps de la réponse contient une collection de ressources de [revendeurs indirects](partner-center-analytics-resources.md#indirect_resellers) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

**Exemple de réponse**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>Voir aussi
 - [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)
