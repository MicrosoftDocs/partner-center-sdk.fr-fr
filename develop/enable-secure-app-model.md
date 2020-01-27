---
title: Activer le modèle d’application sécurisée
description: Sécurisez vos applications de l’espace partenaires et du panneau de configuration.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0a6c3d14ca55350db832c10956b0751acb8f8a0c
ms.sourcegitcommit: 0dea06cd7f95026d93f970d3c294370a58dfcb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76723185"
---
# <a name="enabling-the-secure-application-model-framework"></a>Activation de l’infrastructure du modèle d’application sécurisée

S'applique à :

- Espace partenaires

Microsoft propose une infrastructure sécurisée et évolutive pour l’authentification des partenaires du fournisseur de solutions Cloud (CSP) et des fournisseurs du panneau de configuration (CPV) via l’architecture d’authentification multifacteur (MFA) Microsoft Azure.

Vous pouvez utiliser le nouveau modèle pour élever la sécurité pour les appels d’intégration de l’API de l’espace partenaires. Cela aidera toutes les parties (y compris Microsoft, les partenaires CSP et CPVs) à protéger leur infrastructure et les données client contre les risques de sécurité.

## <a name="scope"></a>Étendue

Cette rubrique concerne les acteurs suivants :

- CPVs
  - Un CPV est un éditeur de logiciels indépendant qui développe des applications qui sont utilisées par les partenaires CSP pour s’intégrer aux API de l’espace partenaires.
  - Un CPV n’est pas un partenaire CSP disposant d’un accès direct au tableau de bord ou aux API de l’espace partenaires.
- Fournisseurs de solutions de chiffrement et fournisseurs directs CSP qui utilisent l’authentification d’application ID + utilisateur et s’intègrent directement avec les API de l’espace partenaires.

## <a name="security-requirements"></a>Exigences de sécurité

Pour plus d’informations sur les exigences de sécurité, consultez [conditions de sécurité des partenaires](https://docs.microsoft.com/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>Modèle d’application sécurisé

Les applications de la place de marché doivent emprunter l’identité des privilèges du partenaire CSP pour appeler les API Microsoft. Les attaques de sécurité sur ces applications sensibles peuvent entraîner la compromission des données client.

Pour obtenir une vue d’ensemble et les détails de la nouvelle infrastructure d’authentification, téléchargez le document [infrastructure de modèle d’application sécurisée](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) . Ce document décrit les principes et les meilleures pratiques pour rendre les applications de la place de marché durables et robustes contre les compromissions de sécurité.

## <a name="samples"></a>exemples

Les documents de présentation et les exemples de code suivants décrivent la manière dont les partenaires peuvent implémenter l’infrastructure de modèle d’application sécurisée :

- [Document de présentation du CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Document de présentation du CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [Exemples .NET](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Exemples Java](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

- [Instructions REST et exemples](#rest)
- [Instructions et exemples PowerShell](#powershell)

## <a name="rest"></a>REST

Pour effectuer des appels REST avec l’infrastructure de modèle d’application sécurisée avec un exemple de code, vous devez effectuer les opérations suivantes :

1. [Créer une application Web](#create-a-web-app)
2. [Recevoir un code d’autorisation](#get-authorization-code)
3. [Obtenir un jeton d’actualisation](#get-refresh-token)
4. [Recevoir un jeton d’accès](#get-access-token)
5. [Effectuer un appel d’API de l’espace partenaires](#make-partner-center-api-calls)

> [!TIP]
> Vous pouvez utiliser le module PowerShell de l’espace partenaires pour obtenir un code d’autorisation et un jeton d’actualisation. Vous pouvez choisir cette option à la place des étapes 2 et 3. Pour plus d’informations, consultez la [section PowerShell et des exemples](#powershell).

### <a name="create-a-web-app"></a>Créer une application Web

Vous devez créer et inscrire une application Web dans l’espace partenaires avant d’effectuer des appels REST.

1. Connectez-vous au [portail Azure](https://portal.azure.com).
2. Créer une application Azure Active Directory (Azure AD).
3. Accordez des autorisations d’application déléguée aux ressources suivantes, *en fonction des exigences de votre application*. Si nécessaire, vous pouvez ajouter des autorisations déléguées pour les ressources d’application.
    1. **Microsoft Partner Center** (certains locataires illustrent cela comme **SampleBECApp**)
    2. **API de gestion Azure** (si vous envisagez d’appeler des API Azure)
    3. **Azure Active Directory Windows**
4. Assurez-vous que l’URL d’origine de votre application est définie sur un point de terminaison où une application Web en ligne est en cours d’exécution. Cette application doit accepter le [code d’autorisation](#get-authorization-code) de l’appel de connexion Azure ad. Par exemple, dans l’exemple de code de [la section suivante](#get-authorization-code), l’application Web s’exécute sur `https://localhost:44395/`.
5. Notez les informations suivantes des paramètres de votre application Web dans Azure AD :
    - ID de l’application
    - Secret de l’application

> [!NOTE]
> Il est recommandé d' [utiliser un certificat comme secret de votre application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials). Toutefois, vous pouvez également créer une clé d’application dans la Portail Azure. L’exemple de code de [la section suivante](#get-authorization-code) utilise une clé d’application.

### <a name="get-authorization-code"></a>Recevoir le code d’autorisation

Vous devez obtenir un code d’autorisation que votre application Web doit accepter à partir de l’appel de connexion Azure AD :

1. Connectez-vous à Azure AD à l’URL suivante : <https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1>. Veillez à vous connecter avec le compte d’utilisateur à partir duquel vous allez effectuer des appels d’API de l’espace partenaires (par exemple, un agent admin ou un compte agent commercial).
2. Remplacez **application-ID** par votre ID d’application Azure ad (Guid).
3. Lorsque vous y êtes invité, connectez-vous avec votre compte d’utilisateur avec MFA configuré.
4. Lorsque vous y êtes invité, entrez des informations supplémentaires sur MFA (numéro de téléphone ou adresse de messagerie) pour vérifier votre connexion.
5. Une fois que vous êtes connecté, le navigateur redirige l’appel vers votre point de terminaison d’application Web avec votre code d’autorisation. Par exemple, l’exemple de code suivant redirige vers `https://localhost:44395/`.

#### <a name="authorization-code-call-trace"></a>Suivi des appels du code d’autorisation

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a>Récupérer le jeton d’actualisation

Vous devez ensuite utiliser votre code d’autorisation pour obtenir un jeton d’actualisation :

1. Effectuez un appel de publication vers le point de terminaison de connexion Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` avec le code d’autorisation. Pour obtenir un exemple, consultez l' [exemple d’appel](#sample-refresh-call)suivant.
2. Notez le jeton d’actualisation qui est retourné.
3. Stockez le jeton d’actualisation dans Azure Key Vault. Pour plus d’informations, consultez la documentation de l' [API Key Vault](https://docs.microsoft.com/rest/api/keyvault/).

> [!IMPORTANT]
> Le jeton d’actualisation doit être [stocké en tant que secret](https://docs.microsoft.com/rest/api/keyvault/setsecret/setsecret) dans Key Vault.

#### <a name="sample-refresh-call"></a>Exemple d’appel d’actualisation

Demande d’espace réservé :

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

Corps de la demande :

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Réponse de l’espace réservé :

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Corps de la réponse :

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Obtenir un jeton d’accès

Vous devez obtenir un jeton d’accès avant de pouvoir effectuer des appels aux API de l’espace partenaires. Vous devez utiliser un jeton d’actualisation pour obtenir un jeton d’accès, car le jeton d’accès a généralement une durée de vie très limitée (par exemple, moins d’une heure).

Demande d’espace réservé :

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

Corps de la demande :

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Réponse de l’espace réservé :

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Corps de la réponse :

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Effectuer des appels d’API de l’espace partenaires

Vous devez utiliser votre jeton d’accès pour appeler les API de l’espace partenaires. Consultez l’exemple d’appel suivant.

#### <a name="example-partner-center-api-call"></a>Exemple d’appel d’API de l’espace partenaires

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Vous pouvez utiliser le [module PowerShell de l’espace partenaires](https://www.powershellgallery.com/packages/PartnerCenter) pour réduire l’infrastructure requise pour échanger un code d’autorisation pour un jeton d’accès. Cette méthode est facultative pour effectuer des [appels REST de l’espace partenaires](#rest).

Pour plus d’informations sur ce processus, consultez la documentation relative au [modèle d’application sécurisée](https://docs.microsoft.com/powershell/partnercenter/secure-app-model) PowerShell.

1. Installez les modules PowerShell du Azure AD et de l’espace partenaires.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Utilisez la commande **[New-PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/new-partneraccesstoken)** pour effectuer le processus de consentement et capturer le jeton d’actualisation requis.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Le paramètre **ServicePrincipal** est utilisé avec la commande **New-PartnerAccessToken** , car une application Azure ad avec un type **Web/API** est utilisée. Ce type d’application requiert qu’un identificateur et une clé secrète du client soient inclus dans la demande de jeton d’accès. Lorsque la commande **obtenir des informations d’identification** est appelée, vous êtes invité à entrer un nom d’utilisateur et un mot de passe. Entrez l’identificateur de l’application en tant que nom d’utilisateur. Entrez le mot de passe secret de l’application. Lorsque la commande **New-PartnerAccessToken** est appelée, vous êtes invité à entrer à nouveau les informations d’identification. Entrez les informations d’identification du compte de service que vous utilisez. Ce compte de service doit être un compte partenaire disposant des autorisations appropriées.

3. Copiez la valeur du jeton d’actualisation.

    ```powershell
    $token.RefreshToken | clip
    ```

Vous devez stocker la valeur du jeton d’actualisation dans un référentiel sécurisé, par exemple Azure Key Vault. Pour plus d’informations sur la façon de tirer parti du module d’application sécurisée avec PowerShell, consultez l’article [Multi-Factor Authentication](https://docs.microsoft.com/powershell/partnercenter/multi-factor-auth) .
