---
title: Configurer l’accès aux API dans l’espace partenaires
description: Configurez des comptes pour le développement par rapport au kit de développement logiciel (SDK) de l’espace partenaires et testez-les
ms.assetid: 182A6831-6F00-4762-9A86-327BF87EA6AC
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 55c7259943dae2cd34ead9583f95afc38df47a3f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488059"
---
# <a name="set-up-api-access-in-partner-center"></a>Configurer l’accès aux API dans l’espace partenaires

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud for US Government
- Espace partenaires de Microsoft Cloud Germany

Cette rubrique décrit les comptes que vous devez développer sur le kit de développement logiciel (SDK) de l’espace partenaires. Cette rubrique explique également comment créer un [compte de bac à sable (sandbox) d’intégration](#integration-sandbox-account) et effectuer des tests dans le bac à sable d’intégration.

## <a name="account-definitions"></a>Définitions de comptes

Pour vous aider à intégrer et tester votre intégration d’API, l’espace partenaires prend en charge deux types de comptes :

### <a name="primary-partner-account"></a>Compte de partenaire principal

Ce compte est l’endroit où vous créez des commandes réelles pour les clients réels. Si vous apportez des modifications ou des transactions lorsque vous êtes connecté au compte principal, à l’aide du kit de développement logiciel (SDK) Partner Center ou de l’interface utilisateur du tableau de bord du partenaire, elles sont traitées comme des commandes officielles pour les clients réels. Ils seront reflétés dans votre facture et votre entreprise sera chargée de les payer.

### <a name="integration-sandbox-account"></a>Compte du bac à sable d’intégration

Ce compte est destiné au test de votre code et à son intégration avec les API de l’espace partenaires avant de le déployer de manière générale. Les modifications et les transactions que vous effectuez lorsque vous êtes connecté au compte du bac à sable (sandbox) d’intégration n’apparaissent pas dans votre facture.

Le compte du bac à sable (sandbox) d’intégration et le compte principal agissent indépendamment, et ne partagent pas les comptes d’administrateur, les comptes d’utilisateur, les clients, les commandes, les abonnements ou d’autres données.

Le bac à sable d’intégration prend en charge les transactions avec un nombre limité de clients, de commandes, d’abonnements, de sièges, etc.

Par stratégie, les comptes sandbox d’intégration sont destinés uniquement à des fins de test d’intégration.

Par défaut, il n’existe aucun compte de bac à sable (sandbox) d’intégration. Vous devez en créer un vous-même si vous envisagez d’utiliser le kit de développement logiciel (SDK) Partner Center.

## <a name="set-up-your-accounts"></a>Configurer vos comptes

Cette section décrit comment configurer un compte de partenaire principal et un compte de bac à sable (sandbox) d’intégration pour le kit de développement logiciel (SDK) de l’espace partenaires.

### <a name="create-an-integration-sandbox"></a>Créer un bac à sable (sandbox) d’intégration

1. Connectez-vous au tableau de bord du partenaire avec un compte d’administrateur général (votre compte de partenaire principal).
2. Dans le menu **paramètres** (icône d’engrenage), choisissez **paramètres de partenaire**.
3. Sur la page **paramètres du compte** , choisissez bac à **sable (sandbox) d’intégration**.

    >[!NOTE]
    >Si vous ne voyez pas d’option d’intégration du bac à sable (sandbox), vous ne disposez peut-être pas d’un compte d’administrateur général. Vous pouvez également utiliser un compte de bac à sable (sandbox) d’intégration et un bac à sable d’intégration a déjà été configuré.

4. Entrez les informations de contact du compte d’administration du bac à sable (sandbox) d’intégration. Ensuite, choisissez **créer un compte**. Patientez quelques minutes pour obtenir un message de confirmation indiquant que le compte a été créé.
5. Une fois que vous voyez le message de confirmation, déconnectez-vous du tableau de bord du partenaire.
6. Reconnectez-vous avec votre nouveau compte d’administrateur de bac à sable d’intégration. Veillez à utiliser le format **username@domain** pour vos informations d’identification, ainsi que le mot de passe que vous venez de spécifier.
7. Choisissez **configurer le compte** au-dessus des **tâches actuelles** pour terminer la configuration du compte sandbox.

### <a name="enable-api-access"></a>Activer l’accès à l’API

Une fois votre compte configuré, vous devez activer l’accès à l’API avant de pouvoir utiliser le kit de développement logiciel (SDK) Partner Center avec le bac à sable d’intégration. Vous devez activer l’accès à l’API séparément pour votre compte de partenaire principal et votre compte de bac à sable (sandbox) d’intégration.

1. Connectez-vous au tableau de bord du partenaire à l’aide d’un compte d’administrateur général.
2. Dans le menu **paramètres** (icône d’engrenage), sélectionnez **paramètres de partenaire**.
3. Sur la page **paramètres du compte** , choisissez gestion des **applications**.
4. Si vous n’avez pas encore d’application existante, ajoutez une nouvelle application Web. Si vous disposez d’une application Web existante, cliquez sur le bouton **Ajouter une clé** .
5. Copiez les informations d’inscription de l’application, en particulier la **clé** si vous créez une application Web, et stockez-la en lieu sûr.
6. Déconnectez-vous du tableau de bord du partenaire.
7. Reconnectez-vous avec votre compte de bac à sable (sandbox) d’intégration. Répétez les étapes 2-5 pour activer l’accès à l’API dans le bac à sable d’intégration.

## <a name="write-and-test-code"></a>Écrire et tester du code

Vous pouvez écrire du code et tester du code dans le bac à sable d’intégration. Vous aurez besoin des informations suivantes pour [configurer l’authentification de l’espace partenaires](partner-center-authentication.md) avec Azure ad.

| Nom de l’élément | Emplacement de l’élément |
| --------- | ------------- |
| ID de l’application/ID client | Dans le menu **paramètres** (icône d’engrenage), sélectionnez **paramètres de partenaire**. Sur la page **paramètres du compte** , sélectionnez gestion des **applications**. L’ID d’application/ID client est répertorié comme ID d’application d' **application inscrite**. |
| Clé | Si vous avez créé une application Web dans la section [activer l’accès à l’API](#enable-api-access), il s’agit de la clé que vous avez enregistrée à l’étape 5. |
| domaine. | Domaine du bac à sable (sandbox) d’intégration. |

## <a name="run-tested-code"></a>Exécuter le code testé

Pour utiliser votre solution avec des données client réelles, vous devez passer de vos informations d’identification du bac à sable (sandbox) d’intégration aux informations d’identification de votre compte partenaire principal.

Lorsque vous êtes prêt à utiliser votre code testé dans votre compte partenaire principal, vous devez recevoir un jeton de sécurité Azure AD. Ce jeton de sécurité est basé sur votre application de l’espace partenaires, la clé et le domaine (au lieu de votre application, clé et domaine du bac à sable (sandbox) d’intégration).

1. Suivez les étapes de la section authentification de l' [espace partenaires](partner-center-authentication.md) pour recevoir un jeton de sécurité Azure ad à l’aide de vos informations d’identification de l’espace partenaires principal. (Vous avez précédemment suivi ces étapes pour obtenir une Azure AD jeton de sécurité pour votre bac à sable d’intégration.)
2. Remplacez le jeton de sécurité d’intégration dans votre code par le nouveau jeton de sécurité de votre compte de partenaire principal.