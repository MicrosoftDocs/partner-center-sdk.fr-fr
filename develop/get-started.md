---
title: Prendre en main
description: Le SDK de l’Espace partenaires comprend une API gérée et une API REST qui permet aux partenaires de gérer les données des clients, des abonnements et des commandes.
ms.assetid: D9A91032-CA5B-4CD2-ADBA-6C5513E05D32
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f8ff1468afbab87ec2b62765f4340aebcc914bf3
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416669"
---
# <a name="get-started"></a>Prendre en main

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Le SDK de l’Espace partenaires comprend une API gérée et une API REST qui permet aux partenaires de gérer les données des clients, des abonnements et des commandes.

## <a name="span-idget_the_codespan-idget_the_codespan-idget_the_codeget-the-code"></a><span id="Get_the_code"/><span id="get_the_code"/><span id="GET_THE_CODE"/>Obtenir le code

[Télécharger le SDK de l’Espace partenaires](https://go.microsoft.com/fwlink/p/?LinkId=746681)  

> [!NOTE]  
> L’accès par API à l’Espace partenaires pour les revendeurs indirects n’est pas un scénario pris en charge.

## <a name="span-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerdetermine-your-version-of-partner-center"></a><span id="Determine_your_version_of_Partner_Center"/><span id="determine_your_version_of_partner_center"/><span id="DETERMINE_YOUR_VERSION_OF_PARTNER_CENTER"/>Déterminer votre version de l’Espace partenaires

Le SDK n’est pas entièrement disponible pour certaines versions de l’Espace partenaires. Pour plus d’informations, consultez [Développement de l’Espace partenaires pour les clouds nationaux Microsoft](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="span-idget_the_samplesspan-idget_the_samplesspan-idget_the_samplesget-the-samples"></a><span id="Get_the_samples"/><span id="get_the_samples"/><span id="GET_THE_SAMPLES"/>Obtenir les exemples

Pour plus d’informations sur les extraits de code C#, les exemples REST et l’exemple d’application, consultez [Exemples de l’Espace partenaires](partner-center-samples.md).

## <a name="span-idsdk_test_vs_prodspan-idsdk_test_vs_prodtest-vs-production"></a><span id="sdk_test_vs_prod"/><span id="SDK_TEST_VS_PROD"/>Test et production

Quand vous commencez à écrire et tester votre code, vous devez utiliser votre compte de bac à sable d’intégration (et les jetons correspondants) afin de ne pas occasionner des frais pour votre entreprise par erreur. Pour plus d’informations sur cet environnement de test, consultez [Configurer l’accès aux API dans l’Espace partenaires](set-up-api-access-in-partner-center.md).

Lorsque votre solution est testée et prête à être utilisée sur des comptes de clients réels, vous devez mettre à jour vos jetons afin d’utiliser une application cliente et un secret Azure AD qui correspondent à votre compte de l’Espace partenaires principal.

Pour obtenir des conseils et des suggestions sur les tests et le débogage, notamment plus d’informations sur l’environnement TiP (Test-in-Production) et le bac à sable d’intégration, consultez [Test et débogage](test-and-debug.md).

## <a name="span-idsdk_config_authspan-idsdk_config_authconfigure-your-authentication"></a><span id="sdk_config_auth"/><span id="SDK_CONFIG_AUTH"/>Configurer votre authentification

Pour configurer votre authentification Azure AD afin de pouvoir utiliser les API de l’Espace partenaires, consultez [Authentification auprès de l’Espace partenaires](partner-center-authentication.md).  

> [!IMPORTANT]
> Microsoft propose un framework sécurisé et scalable pour l’authentification des partenaires du programme Fournisseur de solutions Cloud et des fournisseurs de panneaux de contrôle (CPV) par le biais de l’architecture de l’authentification multifacteur (MFA) Microsoft Azure.
L’Espace partenaires utilise Azure AD pour l’authentification. Pour utiliser les API de l’Espace partenaires, vous devez configurer correctement vos paramètres d’authentification. 
> 
> Pour plus d’informations, consultez [Activer le modèle d’application sécurisé](enable-secure-app-model.md).

## <a name="span-idget_helpspan-idget_helpspan-idget_helpget-help"></a><span id="Get_help"/><span id="get_help"/><span id="GET_HELP"/>Obtenir de l’aide

Les partenaires peuvent bénéficier d’un support technique au sein du [groupe Yammer du SDK de l’Espace partenaires](https://go.microsoft.com/fwlink/p/?LinkID=717360). Pour obtenir une aide plus personnalisée, les développeurs peuvent utiliser les avantages de leur Support Premier ou du support MPN.

## <a name="span-idearly_adopter_programspan-idearly_adopter_programspan-idearly_adopter_programjoin-the-partner-center-api-and-sdk-early-adopter-program"></a><span id="Early_adopter_program"/><span id="early_adopter_program"/><span id="EARLY_ADOPTER_PROGRAM"/>Rejoindre le programme Utilisateur précoce du SDK et de l’API de l’Espace partenaires

Pour déterminer comment collaborer avec Microsoft sur le développement des fonctionnalités de l’Espace partenaires, consultez [Rejoindre le programme Utilisateur précoce du SDK et de l’API de l’Espace partenaires](early-adopter-program.md).