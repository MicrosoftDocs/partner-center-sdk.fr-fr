---
title: Configurer l’accès aux API dans l’Espace partenaires
description: Configurez des comptes permettant de développer des API à l’aide du SDK de l’Espace partenaires et d’effectuer des tests dans le bac à sable (sandbox) d’intégration.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 111ec6e92bff1aff0184e1fbbd4d208720e014e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095834"
---
# <a name="set-up-api-access-in-partner-center"></a>Configurer l’accès aux API dans l’Espace partenaires

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud for US Government
- Espace partenaires de Microsoft Cloud Germany

Cet article décrit les comptes dont vous avez besoin pour développer des API à l’aide du SDK de l’Espace partenaires. Cet article explique également comment créer un [compte sandbox d’intégration](#integration-sandbox-account) et effectuer des tests dans le bac à sable d’intégration.

## <a name="account-definitions"></a>Définitions des comptes

Pour intégrer et tester l’intégration de vos API, l’Espace partenaires prend en charge deux types de comptes :

### <a name="primary-partner-account"></a>Compte de partenaire principal

Ce compte permet de créer des commandes réelles pour des clients réels. Si vous apportez des modifications ou effectuez des transactions lorsque vous êtes connecté au compte principal, que ce soit à l’aide du SDK de l’Espace partenaires ou de l’interface utilisateur du tableau de bord du partenaire, celles-ci sont traitées comme des commandes officielles pour des clients réels. Elles apparaîtront dans votre facture et votre entreprise devra les payer.

### <a name="integration-sandbox-account"></a>Compte de sandbox d’intégration

Ce compte permet de tester votre code, ainsi que son intégration aux API de l’Espace partenaires, avant son déploiement général. Les modifications et les transactions que vous effectuez lorsque vous êtes connecté au compte de sandbox d’intégration ne figurent pas dans votre facture.

Le compte de sandbox d’intégration et le compte principal sont indépendants l’un de l’autre, et ne partagent pas leurs comptes d’administrateur, comptes d’utilisateur, clients, commandes, abonnements ni aucune autre donnée.

Le sandbox d’intégration prend en charge les transactions, mais le nombre de clients, de commandes, d’abonnements ou d’utilisateurs qu’elles impliquent est toutefois limité.

Par stratégie, les comptes sandbox d’intégration doivent uniquement être utilisés pour tester l’intégration.

Par défaut, il n’existe pas déjà de compte sandbox d’intégration. Vous devez le créer vous-même si vous prévoyez d’utiliser le SDK de l’Espace partenaires.

## <a name="set-up-your-accounts"></a>Configurer vos comptes

Cette section explique comment configurer un compte de partenaire principal et un compte sandbox d’intégration pour le SDK de l’Espace partenaires.

### <a name="create-an-integration-sandbox"></a>Créer un sandbox d’intégration

1. Connectez-vous au tableau de bord du partenaire avec un compte d’administrateur général (c’est-à-dire, votre compte de partenaire principal).

2. Dans le menu **Paramètres** (icône représentant une roue dentée), choisissez **Paramètres partenaire**.

3. Dans la page **Paramètres du compte**, choisissez **Sandbox d’intégration**.

    >[!NOTE]
    >Si vous ne voyez pas l’option Sandbox d’intégration, il est possible que vous n’ayez pas de compte d’administrateur général. Il est aussi possible que vous utilisiez un compte de sandbox d’intégration et qu’un sandbox d’intégration ait déjà été configuré.

4. Entrez les informations de contact du compte d’administrateur du sandbox d’intégration. Ensuite, choisissez **Créer un compte**. Un message vous confirmant la création du compte s’affiche au bout de quelques minutes.

5. Une fois le message affiché, vous pouvez vous déconnecter du tableau de bord du partenaire.

6. Reconnectez-vous avec votre nouveau compte d’administrateur de sandbox d’intégration. Veillez à utiliser le format **username@domain** pour vos informations d’identification, ainsi que le mot de passe que vous venez de spécifier.

7. Choisissez **Configurer le compte** au-dessus de **Tâches actuelles** pour terminer la configuration du compte sandbox.

### <a name="enable-api-access"></a>Activer l’accès API

Une fois votre compte configuré, vous devez activer l’accès API avant de pouvoir utiliser le SDK de l’Espace partenaires avec le sandbox d’intégration. L’accès API doit être activé séparément pour votre compte de partenaire principal et votre compte de sandbox d’intégration.

1. Connectez-vous au tableau de bord du partenaire avec un compte d’administrateur général.

2. Dans le menu **Paramètres** (icône représentant une roue dentée), sélectionnez **Paramètres partenaire**.

3. Dans la page **Paramètres du compte**, choisissez **Gestion des applications**.

4. Si vous ne disposez d’aucune application existante, ajoutez une nouvelle application web. Si vous disposez d’une application web existante, choisissez le bouton **Ajouter une clé**.

5. Copiez les informations d’inscription de l’application (notamment la **clé** si vous créez une application web) et stockez-les dans un emplacement sécurisé.

6. Déconnectez-vous du tableau de bord du partenaire.

7. Reconnectez-vous avec votre compte de sandbox d’intégration. Répétez les étapes 2 à 5 pour activer l’accès API dans le sandbox d’intégration.

## <a name="write-and-test-code"></a>Écrire et tester du code

Vous pouvez écrire et tester du code dans le sandbox d’intégration. Vous aurez besoin des informations suivantes pour [configurer l’authentification de l’Espace partenaires](partner-center-authentication.md) auprès d’Azure AD.

| Type d’information | Emplacement de l’information |
| --------- | ------------- |
| ID de l’application/ID de client | Dans le menu **Paramètres** (icône représentant une roue dentée), sélectionnez **Paramètres partenaire**. Dans la page **Paramètres du compte**, sélectionnez **Gestion des applications**. L’ID d’application et l’ID client sont listés comme des **ID d’application inscrite**. |
| Clé | Si vous avez créé une application web dans la section [Activer l’accès API](#enable-api-access), il s’agit de la clé que vous avez enregistrée à l’étape 5. |
| domaine. | Domaine du sandbox d’intégration. |

## <a name="run-tested-code"></a>Exécuter le code testé

Pour utiliser votre solution avec des données client réelles, vous devez passer du compte de sandbox d’intégration au compte de partenaire principal.

Lorsque vous êtes prêt à utiliser votre code testé dans votre compte de partenaire principal, vous devez obtenir un jeton de sécurité Azure AD. Ce jeton de sécurité est basé sur l’application, la clé et le domaine de votre Espace partenaires (et non sur ceux de votre compte de sandbox d’intégration).

1. Suivez les étapes décrites dans [Authentification de l’Espace partenaires](partner-center-authentication.md) pour recevoir un jeton de sécurité Azure AD à l’aide des informations d’identification de votre Espace partenaires principal (vous avez déjà suivi ces étapes afin d’obtenir un jeton de sécurité Azure AD pour votre sandbox d’intégration).

2. Dans votre code, remplacez le jeton de sécurité d’intégration par le nouveau jeton de sécurité de votre compte de partenaire principal.
