---
title: Authentification auprès de l’Espace partenaires
description: L’Espace partenaires utilise Azure AD pour l’authentification ; pour utiliser les API Espace partenaires, vous devez configurer correctement vos paramètres d’authentification.
ms.assetid: 2307F2A8-7BD4-4442-BEF7-F065F16DA0B2
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 36292ac800f7722ce3b5b95c8af19e4690f60ad9
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157101"
---
# <a name="partner-center-authentication"></a>Authentification auprès de l’Espace partenaires

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’Espace partenaires utilise Azure Active Directory pour l’authentification. Quand vous interagissez avec l’API, le SDK ou le module PowerShell de l’Espace partenaires, vous devez configurer correctement une application Azure AD, puis demander un jeton d’accès. Les jetons d’accès obtenus avec l’authentification d’application uniquement ou d’application + utilisateur peuvent être utilisés avec l’Espace partenaires. Deux éléments importants doivent cependant être pris en compte.

- Utilisez l’authentification multifacteur lors de l’accès à l’API Espace partenaires avec l’authentification d’application + utilisateur. Pour plus d’informations sur cette modification, consultez [Activer le modèle d’application sécurisé](enable-secure-app-model.md).

- Toutes les opérations de l’API Espace partenaires ne prennent pas en charge l’authentification d’application uniquement. Vous devrez utiliser l’authentification d’application + utilisateur dans certains scénarios. Sous le titre *Prérequis* de chaque article [Scénario](https://docs.microsoft.com/partner-center/develop/scenarios), vous trouverez la documentation qui indique si l’authentification d’application uniquement, l’authentification d’application + utilisateur ou les deux sont prises en charge.

## <a name="initial-setup"></a>Configuration initiale

1. Pour commencer, vous devez vérifier que vous disposez à la fois d’un compte Espace partenaires principal et d’un compte Espace partenaires de bac à sable (sandbox) d’intégration. Pour plus d’informations, consultez [Configurer des comptes Espace partenaires pour l’accès aux API](set-up-api-access-in-partner-center.md). Notez l’ID d’inscription et le secret de l’application Azure AAD et le secret (le secret client est nécessaire pour l’identification d’application uniquement) pour votre compte principal et votre compte de bac à sable (sandbox) d’intégration.

2. Connectez-vous à Azure AD à partir du portail Azure. Dans **Autorisations pour d’autres applications**, définissez des autorisations pour **Windows Azure Active Directory** sur **Autorisations déléguées**, puis sélectionnez **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**.

3. Dans le portail Azure, **ajoutez une application**. Recherchez « Espace partenaires Microsoft », qui est l’application Espace partenaires Microsoft. Définissez **Autorisations déléguées** sur **Accéder à l’API Espace partenaires**. Si vous utilisez l’Espace partenaires pour Microsoft Cloud Germany ou l’Espace partenaires pour Microsoft Cloud for US Government, cette étape est obligatoire. Si vous utilisez l’instance globale de l’Espace partenaires, cette étape est facultative. Les partenaires CSP peuvent utiliser la fonctionnalité de gestion des applications dans le portail de l’Espace partenaires pour ignorer cette étape pour l’instance globale de l’Espace partenaires.

## <a name="app-only-authentication"></a>Authentification d’application uniquement

Si vous souhaitez utiliser l’authentification d’application uniquement pour accéder à l’API REST, l’API .NET, l’API Java ou le module PowerShell de l’Espace partenaires, vous pouvez le faire en tirant parti des instructions suivantes.

## <a name="net-app-only-authentication"></a>.NET (authentification d’application uniquement)

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a>Java (authentification d’application uniquement)

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a>REST (authentification d’application uniquement)

### <a name="rest-request"></a>Demande REST

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a>Réponse REST

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>Authentification d’application + utilisateur

Historiquement, l’[octroi d’informations d’identification du mot de passe du propriétaire de la ressource](https://tools.ietf.org/html/rfc6749#section-4.3) a été utilisé pour demander un jeton d’accès à utiliser avec l’API REST, l’API .NET, l’API Java ou le module PowerShell de l’Espace partenaires. Cette méthode permettait de demander un jeton d’accès auprès d’Azure Active Directory en utilisant un identificateur de client et des informations d’identification d’utilisateur. Toutefois, cette approche ne fonctionnera plus, car l’Espace partenaires exige l’authentification multifacteur lors de l’utilisation de l’authentification d’application + utilisateur. Pour se conformer à cette exigence, Microsoft a introduit un framework sécurisé et scalable pour l’authentification des partenaires du programme Fournisseur de solutions cloud (CSP) et des fournisseurs de panneaux de configuration (CPV) qui utilisent l’authentification multifacteur. Ce framework est connu sous le nom de Modèle d’application sécurisé, et il est constitué d’un processus de consentement et d’une demande de jeton d’accès avec un jeton d’actualisation.

### <a name="partner-consent"></a>Consentement du partenaire

Le processus de consentement du partenaire est un processus interactif où le partenaire s’authentifie avec l’authentification multifacteur et consent à l’application, et où un jeton d’actualisation est stocké dans un référentiel sécurisé comme Azure Key Vault. Nous vous recommandons d’utiliser un compte dédié à des fins d’intégration pour ce processus.

> [!IMPORTANT]
> La solution d’authentification multifacteur appropriée doit être activée pour le compte de service utilisé dans le processus de consentement du partenaire. Si ce n’est pas le cas, le jeton d’actualisation qui en résulte n’est pas conforme aux exigences de sécurité.

### <a name="samples-for-app--user-authentication"></a>Exemples pour l’authentification d’application + utilisateur

Le processus de consentement du partenaire peut être effectué de différentes façons. Pour aider les partenaires à comprendre comment effectuer chaque opération nécessaire, nous avons développé les exemples suivants. Quand vous implémentez la solution appropriée dans votre environnement, il est important de développer une solution qui est conforme à vos standards de codage et à vos stratégies de sécurité.

## <a name="net-appuser-authentication"></a>.NET (authentification d’application + utilisateur)

L’exemple de projet de [consentement de partenaire](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) montre comment utiliser un site web développé avec ASP.NET pour recueillir le consentement, demander un jeton d’actualisation et le stocker de façon sécurisée dans Azure Key Vault. Effectuez les étapes suivantes afin de créer les prérequis nécessaires pour cet exemple.

1. Créez une instance Azure Key Vault en utilisant le portail Azure ou les commandes PowerShell suivantes. Avant d’exécuter la commande, veillez à modifier les valeurs des paramètres de façon appropriée. Le nom du coffre doit être unique.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Pour plus d'informations sur la création d’un Azure Key Vault, voir [Démarrage rapide : Définir et récupérer un secret auprès d’Azure Key Vault avec le portail Azure](https://docs.microsoft.com/azure/key-vault/quick-create-portal) ou [Démarrage rapide : Définir et récupérer un secret auprès d’Azure Key Vault à l’aide de PowerShell](https://docs.microsoft.com/azure/key-vault/quick-create-powershell). Ensuite, définissez et récupérez un secret.

2. Créez une application Azure AD et une clé en utilisant le portail Azure ou les commandes suivantes.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Veillez à prendre note des valeurs de l’identificateur de l’application et du secret, car elles seront utilisées dans les étapes ci-dessous.

3. Accordez à l’application Azure AD nouvellement créée les autorisations de lire les secrets en utilisant le portail Azure ou les commandes suivantes.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Créez une application Azure AD configurée pour l’Espace partenaires. Effectuez les actions suivantes pour réaliser cette étape.

    - Accédez à la fonctionnalité [Gestion des applications](https://partner.microsoft.com/pcv/apiintegration/appmanagement) du tableau de bord de l’Espace partenaires
    - Cliquez sur *Ajouter une nouvelle application web* pour créer une application Azure AD.

    Veillez à renseigner les valeurs pour *ID d’application*, *ID de compte** et *Clé*, car elles seront utilisées dans les étapes ci-dessous.

5. Clonez le dépôt [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) en utilisant Visual Studio ou la commande suivante.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Ouvrez le projet *PartnerConsent* qui se trouve dans le répertoire `Partner-Center-DotNet-Samples\secure-app-model\keyvault`.

7. Renseignez les paramètres de l’application qui se trouvent dans le fichier [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > Les informations sensibles, comme les secrets d’application, ne doivent pas être stockées dans des fichiers de configuration. Cela a néanmoins été fait ici, car il ne s’agit que d’un exemple d’application. Avec votre application de production, nous vous recommandons fortement d’utiliser l’authentification basée sur les certificats. Pour plus d’informations, consultez [Informations d’identification de certificat pour l’authentification d’application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials).

8. Quand vous exécutez cet exemple de projet, il vous invite à vous authentifier. Une fois l’authentification réussie, un jeton d’accès est demandé auprès d’Azure AD. Les informations retournées par Azure AD incluent un jeton d’actualisation qui est stocké dans l’instance Azure Key Vault configurée.

## <a name="java-appuser-authentication"></a>Java (authentification d’application + utilisateur)

L’exemple de projet de [consentement de partenaire](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) montre comment utiliser un site web développé avec JSP pour recueillir le consentement, demander un jeton d’actualisation et le stocker de façon sécurisée dans Azure Key Vault. Effectuez ce qui suit afin de créer les prérequis nécessaires pour cet exemple.

1. Créez une instance Azure Key Vault en utilisant le portail Azure ou les commandes PowerShell suivantes. Avant d’exécuter la commande, veillez à modifier les valeurs des paramètres de façon appropriée. Le nom du coffre doit être unique.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Pour plus d'informations sur la création d’un Azure Key Vault, voir [Démarrage rapide : Définir et récupérer un secret auprès d’Azure Key Vault avec le portail Azure](https://docs.microsoft.com/azure/key-vault/quick-create-portal) ou [Démarrage rapide : Définir et récupérer un secret auprès d’Azure Key Vault à l’aide de PowerShell](https://docs.microsoft.com/azure/key-vault/quick-create-powershell).

2. Créez une application Azure AD et une clé en utilisant le portail Azure ou les commandes suivantes.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Veillez à prendre note des valeurs de l’identificateur de l’application et du secret, car elles seront utilisées dans les étapes ci-dessous.

3. Accordez à l’application Azure AD nouvellement créée les autorisations de lire les secrets en utilisant le portail Azure ou les commandes suivantes.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Créez une application Azure AD configurée pour l’Espace partenaires. Effectuez les opérations suivantes pour réaliser cette étape.

    - Accédez à la fonctionnalité [Gestion des applications](https://partner.microsoft.com/pcv/apiintegration/appmanagement) du tableau de bord de l’Espace partenaires
    - Cliquez sur *Ajouter une nouvelle application web* pour créer une application Azure AD.

    Veillez à renseigner les valeurs pour *ID d’application*, *ID de compte** et *Clé*, car elles seront utilisées dans les étapes ci-dessous.

5. Clonez le dépôt [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) en utilisant la commande suivante.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Ouvrez le projet *PartnerConsent* qui se trouve dans le répertoire `Partner-Center-Java-Samples\secure-app-model\keyvault`.

7. Renseignez les paramètres de l’application qui se trouvent dans le fichier [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > Les informations sensibles, comme les secrets d’application, ne doivent pas être stockées dans des fichiers de configuration. Cela a néanmoins été fait ici, car il ne s’agit que d’un exemple d’application. Avec votre application de production, nous vous recommandons fortement d’utiliser l’authentification basée sur les certificats. Pour plus d’informations, consultez [Authentification par certificat de coffre de clés](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. Quand vous exécutez cet exemple de projet, il vous invite à vous authentifier. Une fois l’authentification réussie, un jeton d’accès est demandé auprès d’Azure AD. Les informations retournées par Azure AD incluent un jeton d’actualisation qui est stocké dans l’instance Azure Key Vault configurée.

## <a name="cloud-solution-provider-authentication"></a>Authentification de fournisseur de solutions cloud

Les partenaires du programme Fournisseur de solutions cloud peuvent utiliser le jeton d’actualisation obtenu via le processus de [consentement de partenaire](#partner-consent).

### <a name="samples-for-cloud-solution-provider-authentication"></a>Exemples pour l’authentification de fournisseur de solutions cloud

Pour aider les partenaires à comprendre comment effectuer chaque opération nécessaire, nous avons développé les exemples suivants. Quand vous implémentez la solution appropriée dans votre environnement, il est important de développer une solution qui est conforme à vos standards de codage et à vos stratégies de sécurité.

## <a name="net-csp-authentication"></a>.NET (authentification de fournisseur de solutions cloud)

1. Si vous ne l’avez pas encore fait, effectuez le [processus de consentement de partenaire](#partner-consent).

2. Clonez le dépôt [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) en utilisant Visual Studio ou la commande suivante.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Ouvrez le projet `CSPApplication` qui se trouve dans le répertoire `Partner-Center-DotNet-Samples\secure-app-model\keyvault`.

4. Mettez à jour les paramètres de l’application qui se trouvent dans le fichier [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config).

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. Définissez les valeurs appropriées pour les variables **PartnerId** et **CustomerId** qui se trouvent dans le fichier [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs).

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Quand vous exécutez cet exemple de projet, il obtient le jeton d’actualisation obtenu lors du processus de consentement de partenaire. Ensuite, il demande un jeton d’accès pour interagir avec le SDK de l’Espace partenaires pour le compte du partenaire. Enfin, il demande un jeton d’accès pour interagir avec Microsoft Graph pour le compte du client spécifié.

## <a name="java-csp-authentication"></a>Java (authentification de fournisseur de solutions cloud)

1. Si vous ne l’avez pas encore fait, effectuez le [processus de consentement de partenaire](#partner-consent).

2. Clonez le dépôt [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) en utilisant Visual Studio ou la commande suivante

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Ouvrez le projet `cspsample` qui se trouve dans le répertoire `Partner-Center-Java-Samples\secure-app-model\keyvault`.

4. Mettez à jour les paramètres de l’application qui se trouvent dans le fichier [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties).

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Quand vous exécutez cet exemple de projet, il obtient le jeton d’actualisation obtenu lors du processus de consentement de partenaire. Ensuite, il demande un jeton d’accès pour interagir avec le SDK de l’Espace partenaires pour le compte du partenaire.

6. Facultatif : décommentez les appels de fonction *RunAzureTask* et *RunGraphTask* si vous voulez voir comment interagir avec Azure Resource Manager et Microsoft Graph pour le compte du client.

## <a name="control-panel-provider-authentication"></a>Authentification de fournisseur de panneau de configuration

Les fournisseurs de panneau de configuration ont besoin que chaque partenaire qu’ils prennent en charge effectue le processus de [consentement de partenaire](#partner-consent). Une fois cette opération terminée, le jeton d’actualisation obtenu via ce processus est utilisé pour accéder à l’API REST et à l’API .NET de l’Espace partenaires.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Exemples pour l’authentification de fournisseur de panneau de configuration

Pour aider les fournisseurs de panneau de configuration à comprendre comment effectuer chaque opération nécessaire, nous avons développé les exemples suivants. Quand vous implémentez la solution appropriée dans votre environnement, il est important de développer une solution qui est conforme à vos standards de codage et à vos stratégies de sécurité.

## <a name="net-cpv-authentication"></a>.NET (authentification de fournisseur de panneau de configuration)

1. Développez et déployez un processus pour les partenaires fournisseurs de solutions cloud afin de fournir le consentement approprié. Pour plus d'informations et pour obtenir un exemple, consultez [Consentement du partenaire](#partner-consent).

    > [!IMPORTANT]
    > Les informations d’identification utilisateur d’un partenaire fournisseur de solutions cloud ne doivent pas être stockées. Le jeton d’actualisation obtenu via le processus de consentement de partenaire doit être stocké et utilisé afin de demander des jetons d’accès pour interagir avec les API Microsoft.

2. Clonez le dépôt [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) en utilisant Visual Studio ou la commande suivante.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Ouvrez le projet `CPVApplication` qui se trouve dans le répertoire `Partner-Center-DotNet-Samples\secure-app-model\keyvault`.

4. Mettez à jour les paramètres de l’application qui se trouvent dans le fichier [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config).

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. Définissez les valeurs appropriées pour les variables **PartnerId** et **CustomerId** qui se trouvent dans le fichier [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs).

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Quand vous exécutez cet exemple de projet, il obtient le jeton d’actualisation pour le partenaire spécifié. Ensuite, il demande un jeton d’accès pour accéder à l’Espace partenaires et à Azure AD Graph pour le compte du partenaire. La tâche suivante qu’il effectue est la suppression et la création d’octrois d’autorisations dans le locataire du client. Comme il n’existe aucune relation entre le fournisseur du panneau de configuration et le client, ces autorisations doivent être ajoutées en utilisant l’API Espace partenaires. L’exemple suivant montre comment procéder.

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

Une fois ces autorisations établies, l’exemple effectue des opérations en utilisant Azure AD Graph pour le compte du client.

## <a name="java-cpv-authentication"></a>Java (authentification de fournisseur de panneau de configuration)

1. Développez et déployez un processus pour les partenaires fournisseurs de solutions cloud afin de fournir le consentement approprié. Pour plus d'informations et pour obtenir un exemple, consultez [Consentement du partenaire](#partner-consent).

    > [!IMPORTANT]
    > Les informations d’identification utilisateur d’un partenaire fournisseur de solutions cloud ne doivent pas être stockées. Le jeton d’actualisation obtenu via le processus de consentement de partenaire doit être stocké et utilisé afin de demander des jetons d’accès pour interagir avec les API Microsoft.

2. Clonez le dépôt [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) en utilisant la commande suivante.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Ouvrez le projet `cpvsample` qui se trouve dans le répertoire `Partner-Center-Java-Samples\secure-app-model\keyvault`.

4. Mettez à jour les paramètres de l’application qui se trouvent dans le fichier [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties).

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    La valeur de `partnercenter.displayName` doit être le nom d’affichage de votre application de la Place de marché.

5. Définissez les valeurs appropriées pour les variables **partnerId** et **customerId** qui se trouvent dans le fichier [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java).

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Quand vous exécutez cet exemple de projet, il obtient le jeton d’actualisation pour le partenaire spécifié. Ensuite, il demande un jeton d’accès pour accéder à l’Espace partenaires pour le compte du partenaire. La tâche suivante qu’il effectue est la suppression et la création d’octrois d’autorisations dans le locataire du client. Comme il n’existe aucune relation entre le fournisseur du panneau de configuration et le client, ces autorisations doivent être ajoutées en utilisant l’API Espace partenaires. L’exemple suivant montre comment accorder les autorisations.

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

Décommentez les appels de fonction *RunAzureTask* et *RunGraphTask* si vous voulez voir comment interagir avec Azure Resource Manager et Microsoft Graph pour le compte du client.
