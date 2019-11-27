---
title: Prise en main
description: Le kit de développement logiciel (SDK) Partner Center comprend une API gérée et une API REST qui permet aux partenaires de gérer les données des clients, des abonnements et des commandes.
ms.assetid: D9A91032-CA5B-4CD2-ADBA-6C5513E05D32
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 945b8df7d26f8d14386870979f69e3fdbe18d04f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487279"
---
# <a name="get-started"></a>Prise en main

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Le kit de développement logiciel (SDK) Partner Center comprend une API gérée et une API REST qui permet aux partenaires de gérer les données des clients, des abonnements et des commandes.

## <a name="span-idget_the_codespan-idget_the_codespan-idget_the_codeget-the-code"></a><span id="Get_the_code"/><span id="get_the_code"/><span id="GET_THE_CODE"/>obtient le code

[Télécharger le kit de développement logiciel (SDK) Partner Center](http://go.microsoft.com/fwlink/p/?LinkId=746681)  

> [!NOTE]  
> L’accès d’API au centre partenaires pour les revendeurs indirects n’est pas un scénario pris en charge.

## <a name="span-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerdetermine-your-version-of-partner-center"></a><span id="Determine_your_version_of_Partner_Center"/><span id="determine_your_version_of_partner_center"/><span id="DETERMINE_YOUR_VERSION_OF_PARTNER_CENTER"/>déterminer votre version de l’espace partenaires

Certaines versions de l’espace partenaires n’ont pas le kit de développement logiciel (SDK) entier disponible. Pour plus d’informations, consultez [développement pour l’espace partenaires pour Microsoft national Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="span-idget_the_samplesspan-idget_the_samplesspan-idget_the_samplesget-the-samples"></a><span id="Get_the_samples"/><span id="get_the_samples"/><span id="GET_THE_SAMPLES"/>récupérer les exemples

Pour plus d’informations C# sur les extraits de code, les exemples REST et l’exemple d’application, consultez la page exemples de l' [espace partenaires](partner-center-samples.md).

## <a name="span-idsdk_test_vs_prodspan-idsdk_test_vs_prodtest-vs-production"></a><span id="sdk_test_vs_prod"/><span id="SDK_TEST_VS_PROD"/>test et production

Pendant que vous écrivez et testez votre code, vous devez utiliser votre compte de bac à sable (sandbox) d’intégration (et les jetons correspondants) afin de ne pas occasionner de frais accidentels que votre entreprise est responsable du paiement. Pour plus d’informations sur cet environnement de test, consultez [configurer l’accès aux API dans l’espace partenaires](set-up-api-access-in-partner-center.md).

Lorsque votre solution est testée et prête à être utilisée sur des comptes clients réels, vous devez mettre à jour vos jetons afin d’utiliser une application cliente Azure AD et une clé secrète correspondant à votre compte de centre de partenaires principal.

Pour obtenir des conseils et des suggestions sur le test et le débogage, y compris des informations supplémentaires sur les tests en production (TiP) et le bac à sable (sandbox) d’intégration, consultez [tester et déboguer](test-and-debug.md).

## <a name="span-idsdk_config_authspan-idsdk_config_authconfigure-your-authentication"></a><span id="sdk_config_auth"/><span id="SDK_CONFIG_AUTH"/>configurer votre authentification

Pour configurer votre authentification Azure AD afin que vous puissiez utiliser les API de l’espace partenaires, consultez la page authentification de l' [espace](partner-center-authentication.md)partenaires.  

> [!IMPORTANT]
> Microsoft propose une infrastructure sécurisée et évolutive pour l’authentification des partenaires du fournisseur de solutions Cloud (CSP) et des fournisseurs du panneau de configuration (CPV) via l’architecture d’authentification multifacteur (MFA) Microsoft Azure.
L’espace partenaires utilise Azure AD pour l’authentification, et pour utiliser les API de l’espace partenaires, vous devez configurer correctement vos paramètres d’authentification. 
> 
> Pour plus d’informations, consultez [activer le modèle d’application sécurisée](enable-secure-app-model.md).

## <a name="span-idget_helpspan-idget_helpspan-idget_helpget-help"></a><span id="Get_help"/><span id="get_help"/><span id="GET_HELP"/>obtenir de l’aide

Les partenaires peuvent bénéficier d’un support technique dans le [groupe Yammer du kit de développement logiciel (SDK) Partner Center](http://go.microsoft.com/fwlink/p/?LinkID=717360). Pour obtenir une aide plus personnalisée, les développeurs peuvent utiliser leurs avantages ou Support Premier de support MPN.

## <a name="span-idearly_adopter_programspan-idearly_adopter_programspan-idearly_adopter_programjoin-the-partner-center-api-and-sdk-early-adopter-program"></a><span id="Early_adopter_program"/><span id="early_adopter_program"/><span id="EARLY_ADOPTER_PROGRAM"/>rejoindre l’API espace partenaires et le programme SDK Early

Pour savoir comment collaborer avec Microsoft sur le développement de fonctionnalités et de fonctionnalités de partenaires, consultez [rejoindre l’API de l’espace partenaires et le programme d’adoption précoce du kit de développement logiciel (SDK)](early-adopter-program.md).