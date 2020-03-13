---
title: Activer le modèle d’application sécurisé
description: Sécurisez votre Espace partenaires et vos applications de panneau de contrôle.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0a6c3d14ca55350db832c10956b0751acb8f8a0c
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2020
ms.locfileid: "76723185"
---
# <a name="enabling-the-secure-application-model-framework"></a>Activation du framework du modèle d’application sécurisé

S'applique à :

- Espace partenaires

Microsoft propose un framework sécurisé et scalable pour l’authentification des partenaires du programme Fournisseur de solutions Cloud et des fournisseurs de panneaux de contrôle (CPV) par le biais de l’architecture de l’authentification multifacteur (MFA) Microsoft Azure.

Vous pouvez utiliser le nouveau modèle pour renforcer la sécurité des appels d’intégration d’API de l’Espace partenaires. Il permet à toutes les parties (y compris Microsoft, les partenaires du programme Fournisseur de solutions Cloud et les CPV) de protéger leur infrastructure et leurs données client contre les risques de sécurité.

## <a name="scope"></a>Étendue

Cette rubrique concerne les acteurs suivants :

- CPV
  - Un CPV est un éditeur de logiciels indépendant qui développe des applications que les partenaires du programme Fournisseur de solutions Cloud intègrent aux API de l’Espace partenaires.
  - Un CPV n’est pas un partenaire du programme Fournisseur de solutions Cloud qui dispose d’un accès direct au tableau de bord ou aux API de l’Espace partenaires.
- Partenaires indirects et directs du programme Fournisseur de solutions Cloud qui utilisent un ID d’application et une authentification utilisateur et s’intègrent directement aux API de l’Espace partenaires.

## <a name="security-requirements"></a>Exigences de sécurité

Pour plus d’informations sur les exigences en matière de sécurité, consultez [Exigences de sécurité des partenaires](https://docs.microsoft.com/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>Modèle d’application sécurisé

Les applications de la Place de marché doivent emprunter les privilèges d’un partenaire du programme Fournisseur de solutions Microsoft Cloud pour appeler des API Microsoft. Des attaques de sécurité visant ces applications sensibles peuvent entraîner la compromission des données client.

Pour obtenir une vue d’ensemble et des détails sur le nouveau framework d’authentification, téléchargez le document [Framework du modèle d’application sécurisé](https://assetsprod.microsoft.com/secure-application-model-guide.pdf). Ce document décrit les principes et les bonnes pratiques qui permettent de rendre les applications de la Place de marché durables et robustes face aux risques de sécurité.

## <a name="samples"></a>exemples

Les documents de présentation et exemples de code suivants décrivent la manière dont les partenaires peuvent implémenter le framework du modèle d’application sécurisé :

- [Document de présentation des CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Document de présentation des fournisseurs de solutions Cloud](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [Exemples .NET](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Exemples Java](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

- [Instructions et exemples REST](#rest)
- [Instructions et exemples PowerShell](#powershell)

## <a name="rest"></a>REST

Pour effectuer des appels REST avec le framework du modèle d’application sécurisé et un exemple de code, vous devez effectuer les étapes suivantes :

1. [Créer une application web](#create-a-web-app)
2. [Obtenir un code d’autorisation](#get-authorization-code)
3. [Obtenir un jeton d’actualisation](#get-refresh-token)
4. [Obtenir un jeton d’accès](#get-access-token)
5. [Effectuer un appel d’API de l’Espace partenaires](#make-partner-center-api-calls)

> [!TIP]
> Vous pouvez utiliser le module PowerShell Espace partenaires pour obtenir un code d’autorisation et un jeton d’actualisation. Vous pouvez choisir cette option à la place des étapes 2 et 3. Pour plus d’informations, consultez la [section PowerShell et les exemples](#powershell).

### <a name="create-a-web-app"></a>Créer une application web

Vous devez créer et inscrire une application web dans l’Espace partenaires avant d’effectuer des appels REST.

1. Connectez-vous au [portail Azure](https://portal.azure.com).
2. Créez une application Azure Active Directory (Azure AD).
3. Accordez des autorisations d’application déléguées aux ressources suivantes, *en fonction des exigences de votre application*. Si nécessaire, vous pouvez ajouter d’autres autorisations déléguées pour les ressources d’application.
    1. **Espace partenaires Microsoft** (certains locataires le présentent en tant que **SampleBECApp**)
    2. **API de gestion Azure** (si vous envisagez d’appeler des API Azure)
    3. **Windows Azure Active Directory**
4. Vérifiez que l’URL d’accueil de votre application est définie sur un point de terminaison où une application web active est en cours d’exécution. Cette application a besoin d’accepter le [code d’autorisation](#get-authorization-code) de l’appel de connexion Azure AD. Par exemple, dans l’exemple de code de [la section suivante](#get-authorization-code), l’application web s’exécute sur `https://localhost:44395/`.
5. Notez les informations suivantes à partir des paramètres de votre application web dans Azure AD :
    - ID de l’application
    - Secret de l’application

> [!NOTE]
> Il est recommandé d’[utiliser un certificat comme secret de votre application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials). Toutefois, vous pouvez également créer une clé d’application dans le portail Azure. L’exemple de code indiqué dans [la section suivante](#get-authorization-code) utilise une clé d’application.

### <a name="get-authorization-code"></a>Obtenir un code d’autorisation

Vous devez obtenir un code d’autorisation que votre application web doit accepter à partir de l’appel de connexion Azure AD :

1. Connectez-vous à Azure AD à l’URL suivante : <https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1>. Veillez à vous connecter avec le compte d’utilisateur à partir duquel vous allez effectuer des appels d’API de l’Espace partenaires (par exemple, un agent administrateur ou un compte d’agent commercial).
2. Remplacez **Application-Id** par votre ID d’application Azure AD (GUID).
3. À l’invite, connectez-vous à l’aide de votre compte d’utilisateur avec MFA configuré.
4. À l’invite, entrez des informations MFA supplémentaires (numéro de téléphone ou adresse e-mail) pour vérifier votre connexion.
5. Une fois que vous êtes connecté, le navigateur redirige l’appel vers votre point de terminaison d’application web avec votre code d’autorisation. Par exemple, l’exemple de code suivant redirige vers `https://localhost:44395/`.

#### <a name="authorization-code-call-trace"></a>Suivi des appels de code d’autorisation

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

### <a name="get-refresh-token"></a>Obtenir un jeton d’actualisation

Vous devez ensuite utiliser votre code d’autorisation pour obtenir un jeton d’actualisation :

1. Effectuez un appel POST au point de terminaison de connexion Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` avec le code d’autorisation. Pour obtenir un exemple, consultez l’[exemple d’appel suivant](#sample-refresh-call).
2. Prenez note du jeton d’actualisation retourné.
3. Stockez le jeton d’actualisation dans Azure Key Vault. Pour plus d’informations, consultez la [documentation de l’API Key Vault](https://docs.microsoft.com/rest/api/keyvault/).

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

Vous devez obtenir un jeton d’accès avant d’effectuer des appels d’API de l’Espace partenaires. Vous devez utiliser un jeton d’actualisation pour obtenir un jeton d’accès, car le jeton d’accès a généralement une durée de vie très limitée (par exemple, moins d’une heure).

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

### <a name="make-partner-center-api-calls"></a>Effectuer des appels d’API de l’Espace partenaires

Vous devez utiliser votre jeton d’accès pour appeler des API de l’Espace partenaires. Consultez l’exemple d’appel suivant.

#### <a name="example-partner-center-api-call"></a>Exemple d’appel d’API de l’Espace partenaires

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Vous pouvez utiliser le [module PowerShell de l’Espace partenaires](https://www.powershellgallery.com/packages/PartnerCenter) pour réduire l’infrastructure nécessaire à l’échange du code d’autorisation contre un jeton d’accès. Cette méthode est facultative pour effectuer des [appels REST de l’Espace partenaires](#rest).

Pour plus d’informations sur ce processus, consultez la documentation PowerShell du [modèle d’application sécurisé](https://docs.microsoft.com/powershell/partnercenter/secure-app-model).

1. Installez les modules PowerShell d’Azure AD et de l’Espace partenaires.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Utilisez la commande **[New-PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/new-partneraccesstoken)** pour exécuter le processus de consentement et capturer le jeton d’actualisation nécessaire.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Le paramètre **ServicePrincipal** est utilisé avec la commande **New-PartnerAccessToken**, car une application Azure AD de type **Web/API** est utilisée. Ce type d’application nécessite l’inclusion d’un identificateur client et d’un secret dans la demande de jeton d’accès. Quand la commande **Get-Credential** est appelée, vous êtes invité à entrer un nom d’utilisateur et un mot de passe. Entrez l’identificateur de l’application comme nom d’utilisateur. Entrez le secret de l’application comme mot de passe. Quand la commande **New-PartnerAccessToken** est appelée, vous êtes invité à entrer les informations d’identification une nouvelle fois. Entrez les informations d’identification du compte de service que vous utilisez. Ce compte de service doit être un compte partenaire disposant des autorisations appropriées.

3. Copiez la valeur du jeton d’actualisation.

    ```powershell
    $token.RefreshToken | clip
    ```

Vous devez stocker la valeur du jeton d’actualisation dans un référentiel sécurisé, comme Azure Key Vault. Pour plus d’informations sur la façon d’exploiter le module d’application sécurisé avec PowerShell, consultez l’article sur l’[authentification multifacteur](https://docs.microsoft.com/powershell/partnercenter/multi-factor-auth).
