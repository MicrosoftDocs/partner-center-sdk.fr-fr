---
title: Authentification de l’espace partenaires
description: L’espace partenaires utilise Azure AD pour l’authentification, et pour utiliser les API de l’espace partenaires, vous devez configurer correctement vos paramètres d’authentification.
ms.assetid: 2307F2A8-7BD4-4442-BEF7-F065F16DA0B2
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7a29d178774f301f5f3030df119bf30953fa0d8f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486979"
---
# <a name="partner-center-authentication"></a>Authentification de l’espace partenaires

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’espace partenaires utilise Azure Active Directory pour l’authentification. Quand vous interagissez avec l’API de l’espace partenaires, le kit de développement logiciel (SDK) ou le module PowerShell, vous devez configurer correctement une application Azure AD, puis demander un jeton d’accès. Les jetons d’accès obtenus à l’aide de l’application uniquement ou de l’authentification de l’utilisateur et de l’application peuvent être utilisés avec l’espace partenaires. Toutefois, deux éléments importants doivent être pris en compte.

- Vous devez utiliser l’authentification multifacteur lors de l’accès à l’API espace partenaires à l’aide de l’authentification de l’utilisateur et de l’application. Pour plus d’informations sur cette modification, consultez [activer le modèle d’application sécurisée](enable-secure-app-model.md) .
- Toutes les opérations ne prennent pas en charge l’authentification de l’application uniquement par l’API de l’espace partenaires. Cela signifie que vous devrez utiliser l’authentification d’application + utilisateur dans certains scénarios. Sous l’en-tête *conditions préalables* de chaque [scénario](https://docs.microsoft.com/partner-center/develop/scenarios) , vous trouverez la documentation qui indique si l’authentification de l’application uniquement, l’authentification de l’application + de l’utilisateur ou les deux sont prises en charge.

## <a name="initial-setup"></a>Configuration initiale

1. Pour commencer, vous devez vous assurer que vous disposez à la fois d’un compte de centre de partenaires principal et d’un compte de centre de partenaires d’intégration sandbox. Pour plus d’informations, consultez [configurer des comptes de l’espace partenaires pour l’accès aux API](set-up-api-access-in-partner-center.md). Notez l’ID d’inscription de l’application Azure AAD et le secret (la clé secrète client est requise pour l’identification de l’application uniquement) pour votre compte principal et votre compte de bac à sable (sandbox) d’intégration.

2. Connectez-vous à Azure AD à partir du portail de gestion Azure. Dans **autorisations pour d’autres applications**, définissez les autorisations pour **Windows Azure Active Directory** sur **autorisations déléguées**et sélectionnez à **la fois accès au répertoire en tant qu’utilisateur connecté** et **Connectez-vous et lisez le profil utilisateur**.

3. Dans le portail de gestion Azure, **Ajoutez application**. Recherchez « Microsoft Partner Center », qui est l’application Microsoft Partner Center. Définissez les **autorisations déléguées** pour **accéder à l’API espace partenaires**. Si vous utilisez l’espace partenaires pour Microsoft Cloud Allemagne ou l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis, cette étape est obligatoire. Si vous utilisez l’instance globale de l’espace partenaires, cette étape est facultative. Les partenaires CSP peuvent utiliser la fonctionnalité de gestion des applications dans le portail de l’espace partenaires pour contourner cette étape pour l’instance globale de l’espace partenaires.

## <a name="app-only-authentication"></a>Authentification d’application uniquement

Si vous souhaitez utiliser l’authentification d’application uniquement pour accéder à l’API REST de l’espace partenaires, à l’API .NET, à l’API Java ou au module PowerShell, vous pouvez le faire en tirant parti des instructions suivantes.

### <a name="net-app-only-authentication"></a>.NET (authentification uniquement dans l’application)

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

### <a name="java-app-only-authentication"></a>Java (authentification uniquement dans l’application)

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

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

### <a name="rest-app-only-authentication"></a>REST (authentification d’application uniquement)

#### <a name="rest-request"></a>Demande REST

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

#### <a name="rest-response"></a>Réponse REST

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>Application + authentification utilisateur

Historiquement, l' [octroi des informations d’identification du mot de passe du propriétaire](https://tools.ietf.org/html/rfc6749#section-4.3) de la ressource a été utilisé pour demander un jeton d’accès à utiliser avec l’API REST de l’espace partenaires, l’API .net, l’API Java ou le module PowerShell. C’est ici que vous demandez un jeton d’accès à partir de Azure Active Directory à l’aide d’un identificateur de client et des informations d’identification de l’utilisateur. Cette approche ne fonctionnera plus car l’espace partenaires requiert l’authentification multifacteur lors de l’utilisation de l’authentification d’application + utilisateur. Pour se conformer à cette exigence, Microsoft a introduit un Framework sécurisé et évolutif pour authentifier les partenaires du fournisseur de solutions Cloud (CSP) et les fournisseurs du panneau de configuration (CPV) à l’aide de Multi-Factor Authentication. Cette infrastructure est connue sous le nom de modèle d’application sécurisée et est constituée d’un processus de consentement et d’une demande de jeton d’accès à l’aide d’un jeton d’actualisation.

### <a name="partner-consent"></a>Consentement du partenaire

Le processus de consentement du partenaire est un processus interactif dans lequel le partenaire s’authentifie à l’aide de Multi-Factor Authentication, qui consent à l’application, et un jeton d’actualisation est stocké dans un référentiel sécurisé tel que Azure Key Vault. Nous vous recommandons d’utiliser un compte dédié à des fins d’intégration pour ce processus.

> [!IMPORTANT]  
> La solution d’authentification multifacteur appropriée doit être activée pour le compte de service utilisé dans le processus de consentement du partenaire. Si ce n’est pas le cas, le jeton d’actualisation qui en résulte n’est pas conforme aux exigences de sécurité.

### <a name="samples-for-app--user-authentication"></a>Exemples d’authentification d’application + utilisateur

Le processus de consentement du partenaire peut être effectué de plusieurs façons. Pour aider les partenaires à comprendre comment effectuer chaque opération requise, nous avons développé les exemples suivants. Notez qu’il s’agit uniquement d’exemples. Lorsque vous implémentez la solution appropriée dans votre environnement, il est important de développer une solution qui est conforme aux normes de codage et aux stratégies de sécurité.

### <a name="net-appuser-authentication"></a>.NET (application + authentification utilisateur)

L’exemple de projet de [consentement de partenaire](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) montre comment utiliser un site Web développé à l’aide de ASP.net pour capturer le consentement, demander un jeton d’actualisation et le stocker en toute sécurité dans Azure Key Vault. Procédez comme suit pour créer les composants requis pour cet exemple.

1. Créez une instance de Azure Key Vault à l’aide du portail de gestion Azure ou des commandes PowerShell suivantes. Avant d’exécuter la commande, veillez à modifier les valeurs des paramètres en conséquence. Le nom du coffre doit être unique.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Si vous avez besoin d’aide pour créer l’instance de Azure Key Vault consultez [démarrage rapide : définir et récupérer un secret à partir de Azure Key Vault à l’aide du portail Azure ou du](https://docs.microsoft.com/azure/key-vault/quick-create-portal) [démarrage rapide : définir et récupérer un secret à partir de Azure Key Vault à l’aide de PowerShell](https://docs.microsoft.com/azure/key-vault/quick-create-powershell) pour obtenir des instructions pas à pas sur la création d’une instance de Azure Key Vault, puis définir et récupérer une clé secrète.

2. Créez une application Azure AD et une clé à l’aide du portail de gestion Azure ou des commandes suivantes.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Veillez à noter l’identificateur de l’application et les valeurs secrètes, car elles seront utilisées dans les étapes ci-dessous.

3. Accordez à l’application nouvellement créée Azure AD les autorisations lire les secrets à l’aide du portail de gestion Azure ou des commandes suivantes.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Créez un Azure AD application configurée pour l’espace partenaires. Effectuez les actions suivantes pour effectuer cette étape.

    - Accédez à la fonctionnalité de [gestion des applications](https://partner.microsoft.com/pcv/apiintegration/appmanagement) du tableau de bord espace partenaires
    - Cliquez sur *Ajouter une nouvelle application Web* pour créer une application de Azure ad.

    Veillez à documenter l' *ID d’application*, * l’ID de compte * * et les valeurs de *clé* , car elles seront utilisées dans les étapes ci-dessous.

5. Clonez le référentiel [Partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) à l’aide de Visual Studio ou de la commande suivante.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Ouvrez le projet *PartnerConsent* situé dans le répertoire `Partner-Center-DotNet-Samples\secure-app-model\keyvault`.
7. Remplir les paramètres d’application trouvés dans le [fichier Web. config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > Les informations sensibles telles que les secrets d’application ne doivent pas être stockées dans des fichiers de configuration. Il a été effectué ici, car il s’agit d’un exemple d’application. Avec votre application de production, nous vous recommandons vivement d’utiliser l’authentification basée sur les certificats. Pour plus d’informations, consultez [informations d’identification de certificat pour l’authentification de l’application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials) .

8. Lorsque vous exécutez cet exemple de projet, il vous invite à confirmer l’authentification. Une fois l’authentification réussie, un jeton d’accès est demandé à partir de Azure AD. Les informations retournées par Azure AD incluent un jeton d’actualisation qui est stocké dans l’instance configurée de Azure Key Vault.  

### <a name="java-appuser-authentication"></a>Java (application + authentification utilisateur)

L’exemple de projet de [consentement de partenaire](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) montre comment utiliser un site Web développé à l’aide de JSP pour capturer le consentement, demander un jeton d’actualisation et sécuriser le stockage dans Azure Key Vault. Pour créer les composants requis pour cet exemple, procédez comme suit.

1. Créez une instance de Azure Key Vault à l’aide du portail de gestion Azure ou des commandes PowerShell suivantes. Avant d’exécuter la commande, veillez à modifier les valeurs des paramètres en conséquence. Le nom du coffre doit être unique.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Si vous avez besoin d’aide pour créer l’instance de Azure Key Vault consultez [démarrage rapide : définir et récupérer un secret à partir de Azure Key Vault à l’aide du portail Azure ou du](https://docs.microsoft.com/azure/key-vault/quick-create-portal) [démarrage rapide : définir et récupérer un secret à partir de Azure Key Vault à l’aide de PowerShell](https://docs.microsoft.com/azure/key-vault/quick-create-powershell) pour obtenir une procédure pas à pas sur la création d’une instance de Azure Key Vault et la définition et la récupération d’un secret.

2. Créez une application Azure AD et une clé à l’aide du portail de gestion Azure ou des commandes suivantes.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Veillez à documenter l’identificateur de l’application et les valeurs secrètes, car elles seront utilisées dans les étapes ci-dessous.

3. Accordez à l’application de Azure AD nouvellement créée les autorisations lire les secrets à l’aide du portail de gestion Azure ou des commandes suivantes.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Créez un Azure AD application configurée pour l’espace partenaires. Procédez comme suit pour effectuer cette étape.

    - Accédez à la fonctionnalité de [gestion des applications](https://partner.microsoft.com/pcv/apiintegration/appmanagement) du tableau de bord espace partenaires
    - Cliquez sur *Ajouter une nouvelle application Web* pour créer une application de Azure ad.

    Veillez à documenter l' *ID d’application*, * l’ID de compte * * et les valeurs de *clé* , car elles seront utilisées dans les étapes ci-dessous.

5. Clonez le référentiel [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) à l’aide de la commande suivante :

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Ouvrez le projet *PartnerConsent* situé dans le répertoire `Partner-Center-Java-Samples\secure-app-model\keyvault`.
7. Remplir les paramètres d’application trouvés dans le fichier [Web. xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)

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
    > Les informations sensibles telles que les secrets d’application ne doivent pas être stockées dans des fichiers de configuration. Il a été effectué ici, car il s’agit d’un exemple d’application. Avec votre application de production, nous vous recommandons vivement d’utiliser l’authentification par certificat. Pour plus d’informations, consultez [Key Vault l’authentification par certificat](https://github.com/Azure-Samples/key-vault-java-certificate-authentication) .

8. Lorsque vous exécutez cet exemple de projet, il vous invite à confirmer l’authentification. Une fois l’authentification réussie, un jeton d’accès est demandé à partir de Azure AD. Les informations retournées par Azure AD incluent un jeton d’actualisation qui est stocké dans l’instance configurée de Azure Key Vault.  

## <a name="cloud-solution-provider-authentication"></a>Authentification du fournisseur de solutions Cloud

Les partenaires du fournisseur de solutions Cloud peuvent utiliser le jeton d’actualisation obtenu par le biais du processus de [consentement du partenaire](#partner-consent) .

### <a name="samples-for-cloud-solution-provider-authentication"></a>Exemples d’authentification du fournisseur de solutions Cloud

Pour aider les partenaires à comprendre comment effectuer chaque opération requise, nous avons développé les exemples suivants. Notez qu’il s’agit uniquement d’exemples. Lorsque vous implémentez la solution appropriée dans votre environnement, il est important de développer une solution qui est conforme aux normes de codage et aux stratégies de sécurité.

### <a name="net-csp-authentication"></a>.NET (authentification CSP)

1. Si vous ne l’avez pas encore fait, effectuez le [processus de consentement du partenaire](#partner-consent).
2. Clonez le référentiel [Partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) à l’aide de Visual Studio ou de la commande suivante

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Ouvrez le projet `CSPApplication` qui se trouve dans le répertoire `Partner-Center-DotNet-Samples\secure-app-model\keyvault`.
4. Mettez à jour les paramètres d’application trouvés dans le fichier [app. config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) .

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

5. Définissez les valeurs appropriées pour les variables **partenaire** et **CustomerID** trouvées dans le fichier [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) .

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Lorsque vous exécutez cet exemple de projet, il obtient le jeton d’actualisation obtenu pendant le processus de consentement du partenaire. Ensuite, il demande un jeton d’accès pour interagir avec le kit de développement logiciel (SDK) de l’espace partenaires au nom du partenaire. Enfin, il demande un jeton d’accès pour interagir avec Microsoft Graph pour le compte du client spécifié.

### <a name="java-csp-authentication"></a>Java (authentification CSP)

1. Si vous ne l’avez pas déjà fait, effectuez le [processus de consentement du partenaire](#partner-consent).
2. Clonez le référentiel [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) à l’aide de Visual Studio ou de la commande suivante

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Ouvrez le projet `cspsample` qui se trouve dans le répertoire `Partner-Center-Java-Samples\secure-app-model\keyvault`.
4. Mettez à jour les paramètres d’application trouvés dans le fichier [application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Lorsque vous exécutez cet exemple de projet, il obtient le jeton d’actualisation obtenu pendant le processus de consentement du partenaire. Ensuite, il demande un jeton d’accès pour interagir avec le kit de développement logiciel (SDK) de l’espace partenaires au nom du partenaire.
6. Facultatif : annulez les marques de commentaire des appels de fonction *RunAzureTask* et *RunGraphTask* si vous souhaitez savoir comment interagir avec avec Azure Resource Manager et Microsoft Graph pour le compte du client.

## <a name="control-panel-provider-authentication"></a>Authentification du fournisseur du panneau de configuration

Les fournisseurs du panneau de configuration doivent avoir chaque partenaire qu’ils prennent en charge pour effectuer le processus de [consentement du partenaire](#partner-consent) . Une fois cette opération terminée, le jeton d’actualisation obtenu par le biais de ce processus est utilisé pour accéder à l’API REST de l’espace partenaires et à l’API .NET.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Exemples d’authentification du fournisseur du panneau Cloud

Pour aider les fournisseurs du panneau de contrôle à comprendre comment effectuer chaque opération requise, nous avons développé les exemples suivants. Notez qu’il s’agit uniquement d’exemples. Lorsque vous implémentez la solution appropriée dans votre environnement, il est important de développer une solution qui est conforme aux normes de codage et aux stratégies de sécurité.

### <a name="net-cpv-authentication"></a>.NET (authentification CPV)

1. Développez et déployez un processus pour les partenaires de fournisseurs de solutions Cloud afin de fournir le consentement approprié. Pour obtenir des détails supplémentaires et un exemple, consultez le [consentement du partenaire](#partner-consent) .

    > [!IMPORTANT]  
    > Les informations d’identification de l’utilisateur d’un partenaire de fournisseur de solutions Cloud ne doivent pas être stockées. Le jeton d’actualisation obtenu par le biais du processus de consentement du partenaire doit être stocké et utilisé pour demander des jetons d’accès pour interagir avec toute API Microsoft.

2. Clonez le référentiel [Partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) à l’aide de Visual Studio ou de la commande suivante

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Ouvrez le projet `CPVApplication` qui se trouve dans le répertoire `Partner-Center-DotNet-Samples\secure-app-model\keyvault`.
4. Mettez à jour les paramètres d’application trouvés dans le fichier [app. config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) .

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

5. Définissez les valeurs appropriées pour les variables **partenaire** et **CustomerID** trouvées dans le fichier [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) .

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Lorsque vous exécutez cet exemple de projet, il obtient le jeton d’actualisation pour le partenaire spécifié. Ensuite, il demande un jeton d’accès pour accéder à l’espace partenaires et Azure AD graphique pour le compte du partenaire. La tâche suivante exécutée est la suppression et la création d’octrois d’autorisations dans le locataire client. Étant donné qu’il n’existe aucune relation entre le fournisseur du panneau de configuration et le client, ces autorisations doivent être ajoutées à l’aide de l’API espace partenaires. L’exemple suivant montre comment procéder.

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

Une fois ces autorisations établies, l’exemple effectue des opérations à l’aide de Azure AD graphique pour le compte du client.

### <a name="java-cpv-authentication"></a>Java (authentification CPV)

1. Développez et déployez un processus pour les partenaires de fournisseurs de solutions Cloud afin de fournir le consentement approprié. Pour obtenir des détails supplémentaires et un exemple, consultez le [consentement du partenaire](#partner-consent) .

    > [!IMPORTANT]  
    > Les informations d’identification de l’utilisateur d’un partenaire de fournisseur de solutions Cloud ne doivent pas être stockées. Le jeton d’actualisation obtenu par le biais du processus de consentement du partenaire doit être stocké et utilisé pour demander des jetons d’accès pour interagir avec toute API Microsoft.

2. Clonez le référentiel [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) à l’aide de la commande suivante :

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Ouvrez le projet `cpvsample` qui se trouve dans le répertoire `Partner-Center-Java-Samples\secure-app-model\keyvault`.
4. Mettez à jour les paramètres d’application trouvés dans le fichier [application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .

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

    La valeur de la `partnercenter.displayName` doit être le nom d’affichage de votre application Marketplace.

5. Définissez les valeurs appropriées pour les variables **partenaire** et **CustomerID** trouvées dans le fichier [Program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Lorsque vous exécutez cet exemple de projet, il obtient le jeton d’actualisation pour le partenaire spécifié. Ensuite, il demande un jeton d’accès pour accéder à l’espace partenaires pour le compte du partenaire. La tâche suivante exécutée est la suppression et la création d’octrois d’autorisations dans le locataire client. Étant donné qu’il n’existe aucune relation entre le fournisseur du panneau de configuration et le client, ces autorisations doivent être ajoutées à l’aide de l’API espace partenaires. L’exemple suivant montre comment procéder.

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

Annulez les marques de commentaire des appels de fonction *RunAzureTask* et *RunGraphTask* si vous souhaitez savoir comment interagir avec avec Azure Resource Manager et Microsoft Graph pour le compte du client.
