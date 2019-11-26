---
title: Application de test de la console
description: Cette application de test de console fournit un exemple de code pour tous les scénarios pris en charge par les API de l’espace partenaires. Vous pouvez également l’utiliser pour le test.
ms.assetid: 56F5B4C6-CE87-4D13-9D8C-09F38E946292
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 51de7cc8b6a721c3c0d04f57d20e4d9afef50283
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488919"
---
# <a name="console-test-app"></a>Application de test de la console

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’application de test console est fournie C# dans et Java, elle fournit des exemples de code pour tous les scénarios pris en charge par les API de l’espace partenaires. Vous pouvez également l’utiliser pour le test.

## <a name="get-the-code"></a>Obtenir le code

Téléchargez l’exemple de code pour l’application de test de la console.

## <a name="net"></a>.NET

[Téléchargez l’exemple de code](http://go.microsoft.com/fwlink/p/?LinkId=746682) et modifiez-le si nécessaire.

> [!IMPORTANT]
> Avant de générer l’application, mettez à jour les valeurs dans le fichier *app. config* afin de refléter les informations d’authentification Azure ad que vous avez créées dans l’authentification de l' [espace partenaires](partner-center-authentication.md). En particulier, vous devez utiliser les paramètres de votre compte sandbox d’intégration lors du développement anticipé ou pour les tests en production.

Sous **ScenarioSettings** dans le fichier *app. config* , vous pouvez définir les paramètres qui seront automatiquement transmis dans les scénarios que vous exécutez.

Pour modifier la liste des scénarios exécutés, mettez en commentaire les lignes dans **IPartnerScenario\[\] mainScenarios** ou dans une méthode d' **extraction de scénarios** individuelle trouvée dans le fichier *Program.cs* .

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

[Téléchargez l’exemple de code](http://go.microsoft.com/fwlink/p/?LinkId=2026887) et modifiez-le si nécessaire.

> [!IMPORTANT]
> Avant de générer l’application, mettez à jour les valeurs du fichier *SamplesConfigurations. JSON* pour refléter les informations d’authentification Azure ad que vous avez créées dans [l’authentification de l’espace partenaires](partner-center-authentication.md). En particulier, vous devez utiliser les paramètres de votre compte sandbox d’intégration lors du développement anticipé ou pour les tests en production.

Sous **ScenarioSettings** dans le fichier *SamplesConfiguration. JSON* , vous pouvez définir les paramètres qui seront automatiquement transmis dans les scénarios que vous exécutez.

Pour modifier la liste des scénarios exécutés, mettez en commentaire les lignes dans **IPartnerScenario\[\] mainScenarios** ou dans une méthode d' **extraction de scénarios** individuelle trouvée dans le fichier *Program. Java* .

## <a name="what-to-change"></a>Éléments à modifier

Utilisez les listes suivantes pour déterminer les éléments à modifier ou à ne pas modifier dans l’exemple de code.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

Pour **PartnerServiceSettings**, ne modifiez pas les éléments suivants :

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Tous ces paramètres sont nécessaires pour que les exemples d’appels d’API fonctionnent correctement.

### <a name="userauthentication"></a>UserAuthentication

Pour **UserAuthentication**, vous devez modifier :

- **ApplicationID** (votre ID d’application Azure Active Directory utilisé pour la connexion)
- **Nom d’utilisateur** (votre nom d’utilisateur Active Directory)
- **Mot** de passe (votre mot de passe Active Directory).

Ne pas modifier :

- **Resourceurl n'**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

Pour **AppAuthentication**, vous devez modifier :

- **ApplicationID** (votre ID d’application Active Directory utilisé pour la connexion de l’application)
- **Applicationsecret :** (votre secret d’application Active Directory utilisé pour la connexion de l’application)
- **Domaine** (votre domaine Active Directory sur lequel l’application est hébergée)

### <a name="scenariosettings"></a>ScenarioSettings

Pour **ScenarioSettings**, ne modifiez pas les éléments suivants :

- **CustomerDomainSuffix** (le suffixe de domaine utilisé lors de la création d’un client)

Paramètres facultatifs. Si le champ n’est pas renseigné, ces informations doivent être entrées lors de l’exécution d’un scénario, le cas échéant) :

- **CustomerIdToDelete** (ID du client utilisé pour la suppression)
- **DefaultCustomerId** (ID client à utiliser dans les scénarios liés aux clients)
- **DefaultInvoiceID** (ID de facture à utiliser dans les scénarios de facture)
- **PartnerMpnId** (ID MPN du partenaire à utiliser dans les scénarios de partenaires indirects)
- **DefaultServiceRequestId** (ID de demande de service à utiliser dans les scénarios de demande de service)
- **DefaultSupportTopicID** (ID de la rubrique de support à utiliser dans les scénarios de demande de service)
- **DefaultOfferID** (ID d’offre à utiliser dans les scénarios d’offre)
- **DefaultOrderID** (ID de commande à utiliser dans les scénarios d’ordre)
- **DefaultSubscriptionID** (ID d’abonnement à utiliser dans les scénarios d’abonnement)

Modification facultative. Tous ces paramètres spécifient la quantité d’entrées par page lors de la récupération du contenu paginé :

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**