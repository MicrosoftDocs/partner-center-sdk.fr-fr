---
title: Inscrire les détails de l’application pour l’espace partenaires pour Microsoft national Cloud
description: Les développeurs doivent inscrire des détails sur leur application avec Azure AD par le biais du Portail Azure. Cela permet de s’assurer que seules les applications spécifiées sont en mesure de se connecter aux données des partenaires et des clients.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.assetid: 73C5926A-0DEB-42E5-8982-7E44A2031F0B
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 494c803af64d8affd126a8de05fcdb18d648d774
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489549"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud"></a>Inscrire les détails de l’application pour l’espace partenaires pour Microsoft national Cloud

S’applique à :

- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les développeurs doivent inscrire des détails sur leur application avec Azure AD par le biais du Portail Azure. Cela permet de s’assurer que seules les applications spécifiées sont en mesure de se connecter aux données des partenaires et des clients.

Pour l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis, vous devez actuellement gérer les applications via PowerShell. Pour plus d’informations, consultez la [documentation de référence Azure PowerShell](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0#applications).

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Tenez compte des conditions supplémentaires suivantes lorsque vous créez une application pour Partner Center pour Microsoft Cloud Allemagne ou l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis.

## <a name="web-apps"></a>Applications Web

Pour les applications Web, utilisez les procédures suivantes pour inscrire votre ID d’application.

### <a name="create-or-update-web-app"></a>Créer ou mettre à jour une application Web

1. Accédez à la page de [inscriptions d’applications portail Azure](https://go.microsoft.com/fwlink/?linkid=2083908) pour inscrire votre application. Connectez-vous au Portail Azure à l’aide d’un compte professionnel ou scolaire, ou d’un compte Microsoft personnel.

2. Sélectionnez **nouvelle inscription**. Pour plus d’informations, consultez [démarrage rapide : inscrire une application auprès de la plateforme Microsoft Identity](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Configurer les autorisations d’accès à l’API pour l’application Web

1. Choisissez votre application. Accédez aux **paramètres** de l’application Web.
2. Dans la section accès à l' **API** , choisissez **autorisations requises**
3. Pour les autorisations Windows Azure Active Directory :
    1. Choisissez **Windows Azure Active Directory autorisations**.
    2. Dans **autorisations des applications**, sélectionnez lire les données d’annuaire.
    3. Enregistrez les autorisations.
4. Notez l’ID de l’application dans la section **Propriétés** de votre application Web.

### <a name="add-a-secret-key-to-your-app"></a>Ajoutez une clé secrète à votre application

1. Accédez à la section **clés** de votre application Web.
2. Entrez la description de la clé et sélectionnez une durée de 1 ou 2 ans, selon vos besoins.
3. Enregistrez et copiez la valeur de la clé secrète. **Cette valeur ne s’affichera plus une fois que vous aurez quitté cette page.**

Vous devez disposer des informations suivantes à partir de la configuration de l’application Web :

- ID de l’application
- Secret de l’application

### <a name="register-the-web-app-in-partner-center"></a>Inscrire l’application Web dans l’espace partenaires

1. Connectez-vous à <https://partnercenter.microsoft.com>.
2. Choisissez **tableau de bord**, choisissez **paramètres du compte**, puis gestion des **applications**.
3. Dans la section **application Web** , choisissez **inscrire l’application existante**.
4. Sélectionnez l’application Web que vous avez créée dans le portail de gestion Azure.
5. Choisissez **inscrire votre application**.

## <a name="native-apps"></a>Applications natives

Les applications natives n’ont pas besoin d’être inscrites auprès de l’espace partenaires. Toutefois, ces applications doivent être configurées pour fournir un accès aux API de l’espace partenaires.

>[!NOTE]
>Avant de créer une application native dans le portail de gestion Azure, connectez-vous à l’espace partenaires à l’aide des informations d’identification de l’utilisateur administrateur du locataire partenaire. Cela crée les paramètres sur le locataire pour activer les autorisations de l’application.

### <a name="create-native-app"></a>Créer une application native

1. Accédez à la page de [inscriptions d’applications portail Azure](https://go.microsoft.com/fwlink/?linkid=2083908) pour inscrire votre application. Connectez-vous au Portail Azure à l’aide d’un compte professionnel ou scolaire, ou d’un compte Microsoft personnel.

2. Sélectionnez **nouvelle inscription**. Pour plus d’informations, consultez [démarrage rapide : inscrire une application auprès de la plateforme Microsoft Identity](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Configurer les autorisations d’accès à l’API pour une application native

1. Choisissez votre application. Accédez à **paramètres**.
2. Dans accès à l’API, choisissez **autorisations requises**.
3. Choisissez **Windows Azure Active Directory autorisations**. Dans **autorisations déléguées**, sélectionnez les autorisations suivantes :
    - **Se connecter et lire le profil utilisateur**
    - **Lire les données d’annuaire**
    - **Accéder au répertoire en tant qu’utilisateur connecté**
    - **Lire tous les groupes**
4. Enregistrez les autorisations.
5. Sélectionnez **Ajouter** dans **autorisations requises**.
6. Choisissez **Sélectionner une API**.
    1. Dans la zone de recherche, entrez **Microsoft Partner Center** et sélectionnez-le dans la liste des résultats.
    2. Choisissez **Sélectionner**.
7. Choisissez **Sélectionner les autorisations**.
    1. Sélectionnez **accéder à l’espace partenaires des EPI**.
    2. Choisissez **Sélectionner**.
8. Choisissez **terminé**.

>[!IMPORTANT]
> Notez l’ID de l’application dans les propriétés de votre application.

Vous n’avez pas besoin d’inscrire des applications natives dans l’espace partenaires, mais l’application native doit être consentie par l’administrateur. Notez l’ID d’application de votre application native.