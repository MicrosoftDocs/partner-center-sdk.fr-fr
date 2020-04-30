---
title: Guide de démarrage rapide du créateur de vitrine pour les clients fournisseurs de solutions cloud
description: Créez une place de marché en ligne pour vendre des offres de fournisseur de solutions Cloud à l’aide du générateur de vitrine client du CSP.
ms.assetid: 333EE80D-E49E-4E89-87FB-3F02AC48C236
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ac3d053e8e6d6684cf9583c57e388da828bc8442
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155311"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Guide de démarrage rapide du créateur de vitrine pour les clients fournisseurs de solutions cloud

**S’applique à :**

- Espace partenaires

Créez une place de marché en ligne pour vendre des offres de fournisseur de solutions Cloud à l’aide du générateur de vitrine client du CSP.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Présentation du générateur de vitrine client du fournisseur de solutions Cloud

Le générateur de vitrine du client CSP aide les partenaires à créer facilement une place de marché en ligne pour vendre des offres CSP à leurs clients. La plupart des partenaires et petites entreprises veulent se concentrer sur la vente plutôt que sur le développement d’une place de marché en ligne. L’exemple d’application du kit de développement logiciel (SDK) Partner Center nécessite des compétences en développement de logiciels pour créer et déployer un site Web. Avec le générateur de vitrine du client CSP, vous pouvez créer rapidement et facilement votre propre site Web. Vous pouvez également télécharger le site Web en tant qu’exemple de code ou le déployer directement dans votre abonnement Azure avec un site Web prêt à l’emploi.

Ce site Web est entièrement détenu, pris en charge et géré par les partenaires, et Microsoft ne collecte pas de données ou de données de télémétrie à partir du site Web. Le générateur de vitrine du client CSP crée un site Web pour le partenaire qui est entièrement conforme à la norme de paiement de la [carte de paiement](https://www.pcisecuritystandards.org/) (PCI DSS).

Le code du générateur de vitrine du client CSP est soumis à la licence disponible dans le [CLUF du kit de développement logiciel (SDK) de l’espace partenaires](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

>[!NOTE]
>Vous êtes responsable de la gestion et de la maintenance des sites Web de vitrine, ainsi que des problèmes qui peuvent résulter de la création d’un site Web. Lisez et comprenez les termes du [CLUF du kit de développement logiciel (SDK) de l’espace partenaires](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

Pour plus d’informations, consultez également les articles suivants : [vitrine Web du client CSP](csp-customer-web-storefront.md) et [application de test](console-test-app.md)de la console.

## <a name="considerations"></a>Considérations

Le générateur de vitrine client du fournisseur de solutions Cloud est conçu pour créer rapidement un site Web. Tenez compte des points suivants lors de votre planification :

- Une fois le déploiement effectué, Microsoft et l’espace partenaires ne disposent pas d’une copie du site Web partenaire ni des informations ajoutées dans le générateur de vitrine client du fournisseur de solutions.

- L’espace partenaires peut uniquement déployer un site Web de vitrine du client CSP sur les abonnements Azure d’un partenaire.

- Ce site Web, une fois déployé, est entièrement détenu et géré par le partenaire. Microsoft n’a pas accès à ce site Web ou à toutes les données relatives au site Web. Les partenaires sont responsables de la maintenance et de la gestion du site Web. Microsoft ne fournira pas de site Web en direct ou autre support technique lié au générateur de vitrine client du fournisseur de solutions client ou à un site Web créé à l’aide du générateur de vitrine client du fournisseur de solutions.

- L’espace partenaires ne peut pas accéder directement à ce site Web ou le mettre à niveau avec des fonctionnalités SDK ou API nouvelles ou modifiées. Toutes les nouvelles fonctionnalités ou améliorations doivent être détenues, développées et gérées par des partenaires, y compris l’ajout de nouvelles fonctionnalités d’API ou de kit de développement logiciel (SDK) de l’espace partenaires.

- Ce générateur de vitrine du client CSP offre actuellement la possibilité de configurer le paiement sur un compte PayPal Pro/PayU Money (pour l’Inde). Si les partenaires doivent modifier le processeur de paiement, ils devront modifier le code pour prendre en charge leur mode de paiement préféré.

- Toutes les informations relatives au paiement ajoutées dans le générateur de vitrine client du fournisseur de solutions n’est pas stockée ou conservée dans l’espace partenaires.

- La configuration de paiement PayPal fonctionnera dans toutes les zones géographiques où PayPal sera disponible. La disponibilité et le support PayPal sont contrôlés uniquement par PayPal et peuvent être interrompus à tout moment par PayPal.

- La configuration de paiement PayU fonctionne uniquement en Inde. La disponibilité et le support PayU sont contrôlés uniquement par PayU et peuvent être abandonnés à tout moment par PayU.

- Lisez et comprenez les termes du [CLUF du kit de développement logiciel (SDK) de l’espace partenaires](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

## <a name="using-the-csp-customer-storefront-builder"></a>Utilisation du générateur de vitrine client du fournisseur de solutions Cloud

Les administrateurs du partenaire CSP de l’espace partenaires peuvent déployer une boutique client CSP directement à partir de l’espace partenaires. Avec un minimum d’efforts, un nouveau site Web peut être déployé sur le locataire du partenaire. Une fois déployés, les partenaires peuvent utiliser le site Web pour configurer la personnalisation, les offres et les informations relatives aux paiements, puis partager l’adresse URL du site Web avec les clients.

Le processus de création d’un site Web de vitrine consiste à :

1. [Déployer le site Web](#deploy)

2. [Configurer la vitrine](#configure)

3. [Transact sur la vitrine](#transact)

### <a name="deploy"></a>Déployer

Options de déploiement :

- Téléchargez l’exemple de code de la boutique de l' [espace partenaires](https://github.com/Microsoft/Partner-Center-Storefront) à partir de GitHub
- Intégrer avec Azure pour déployer le site Web configuré
- Déployez sur un abonnement existant ou apportez votre propre abonnement

### <a name="configure"></a>Configurer

Aucune compétence de développement n’est requise pour personnaliser une vitrine.

Connectez-vous avec vos informations d’identification d’administrateur de l’espace partenaires pour configurer :

- **Personnalisation**: nom de l’entreprise, logo, contacts et bien plus encore.

- **Offres**: afficher toutes les offres CSP. Vous pouvez sélectionner les offres qui peuvent être visualisées et achetées par vos clients. Vous pouvez également personnaliser les informations d’offre et ajouter votre prix.

- **Configuration de paiement PayPal**: ajoutez vos informations de compte de paiement Paypal. Si vous n’avez pas de compte PayPal, vous pouvez [https://www.paypal.com](https://www.paypal.com) visiter et créer un nouveau compte. Ce compte sera utilisé pour PayPal pour créditer les paiements effectués par les clients. *Microsoft n’est pas responsable de la relation entre les partenaires et PayPal. L’utilisation de PayPal peut obliger les clients du partenaire ou du partenaire à accepter des conditions supplémentaires.*

- (*Pour l’Inde*) **Configuration de paiement PayU**: ajoutez vos informations de compte de paiement PayU Money. Si vous n’avez pas de compte PayU Money, vous pouvez [https://www.payumoney.com/](https://www.payumoney.com/) visiter et créer un nouveau compte. Ce compte sera utilisé par PayU pour créditer les paiements effectués par les clients. *Microsoft n’est pas responsable de la relation entre les partenaires et PayU. L’utilisation de PayU peut obliger les clients du partenaire ou du partenaire à accepter des conditions supplémentaires.*

### <a name="transact"></a>Transaction

- Après le déploiement, les clients peuvent acheter et traiter immédiatement.

- Les clients peuvent acheter directement à partir du portail partenaires intégré au kit de développement logiciel (SDK) de l’espace partenaires.

#### <a name="customer-countries"></a>Pays clients

Les clients peuvent appartenir à ces pays :

| Indicatif de pays | Nom du pays   |
|--------------|----------------|
| AU           | Australie      |
| AT           | Autriche        |
| BE           | Belgique        |
| BG           | Bulgarie       |
| CA           | Canada         |
| HR           | Croatie        |
| CY           | Chypre         |
| CZ           | République tchèque |
| DK           | Danemark        |
| EE           | Estonie        |
| FI           | Finlande        |
| FR           | France         |
| DE           | Allemagne        |
| GR           | Grèce         |
| HU           | Hongrie        |
| IS           | Islande        |
| IN           | Inde          |
| IE           | Irlande        |
| IT           | Italie          |
| JP           | Japon          |
| LV           | Lettonie         |
| LI           | Liechtenstein  |
| LT           | Lituanie      |
| LU           | Luxembourg     |
| MT           | Malte          |
| MC           | Monaco         |
| NL           | Pays-Bas    |
| NZ           | Nouvelle-Zélande    |
| Non           | Norvège         |
| PO           | Pologne         |
| PT           | Portugal       |
| RO           | Roumanie        |
| SK           | Slovaquie       |
| SL           | Slovénie       |
| ES           | Espagne          |
| SE           | Suède         |
| CH           | Suisse    |
| Go           | Royaume-Uni |
| US           | États-Unis  |

## <a name="partner-experience-scenarios"></a>Scénarios d’expérience partenaire

### <a name="deployment-scenario"></a>Scénario de déploiement

Pour déployer une vitrine cliente améliorée ou personnalisée :

- Téléchargez l’exemple de code de la boutique de l' [espace partenaires](https://github.com/Microsoft/Partner-Center-Storefront) pour effectuer des personnalisations supplémentaires.

- Utilisez Microsoft Visual Studio 2015 (ou version ultérieure) pour développer.

- Générez des modifications supplémentaires et des améliorations (notamment les autorisations, les certifications, les modifications de manifeste et d’autres éléments).

### <a name="configuration-scenario"></a>Scénario de configuration

- Le site Web nouvellement créé est lié à un locataire partenaire et a accès à tous les comptes d’administrateur de ce locataire partenaire.

  - Les partenaires peuvent se connecter à ce nouveau site Web à l’aide de leurs informations d’identification d’administrateur de l’espace partenaires.

- L’application vitrine prend actuellement en charge le français, l’espagnol, le néerlandais, l’allemand, le japonais et l’anglais. (L’anglais sert de langue de secours.)

  - La vitrine configure les paramètres régionaux en utilisant les paramètres régionaux par défaut du partenaire à partir du profil du partenaire dans l’espace partenaires. Ces paramètres régionaux sont utilisés pour configurer les devises, les formats de date et les offres localisées dans le référentiel.

- Les partenaires peuvent configurer la personnalisation, les offres et les informations de paiement PayPal ou PayU (pour l’Inde).

- Les partenaires peuvent mettre à jour le nom de la société, le logo de l’entreprise, l’image d’en-tête, les contacts commerciaux et de support, etc.

- Les partenaires peuvent voir toutes les offres CSP disponibles sur la base de leur territoire.

  - Les partenaires peuvent choisir les offres qu’ils souhaitent présenter à tous leurs clients.

  - Un partenaire CSP peut sélectionner une ou plusieurs offres et mettre à jour le nom, la quantité, la description de la fonctionnalité et le prix.
  - Le prix est le prix annuel. Les clients s’abonnent annuellement.

- Les partenaires peuvent à tout moment configurer des transactions pré-approuvées pour (a) tous les clients actuels et futurs ou (b) des clients spécifiques.

  - Les clients préapprouvés ne sont pas tenus de payer sur le portail lorsqu’ils ajoutent de nouveaux abonnements, achètent des sièges supplémentaires à des abonnements existants ou renouvellent un abonnement.

  - Les clients préapprouvés ne seront pas redirigés vers PayPal ou PayU (pour l’Inde) à des fins de paiement durant ces transactions.

  - Les transactions pré-approuvées du client permettent à un partenaire d’effectuer une facturation et une facturation hors connexion à leurs clients préapprouvés.

- Un partenaire CSP peut entrer les informations de son compte PayPal, telles que l’ID client et le secret PayPal. Un partenaire CSP peut également choisir s’il souhaite effectuer un test à l’aide d’un bac à sable (sandbox) ou d’un compte Live.

  - Les partenaires peuvent trouver ces informations [https://developer.paypal.com/](https://developer.paypal.com/) dans **mes applications & informations d’identification**. Vous pouvez également obtenir ces informations à partir d’une application actuelle ou en créant une nouvelle application dans PayPal.
  - Créez un nouveau compte PayPal si vous n’en avez pas déjà un. Ce compte sera utilisé pour PayPal pour créditer les paiements effectués par les clients.

    - Pour ouvrir un compte professionnel PayPal, consultez [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register).

    - Pour créer un compte PayPal sandbox, [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/)consultez.

- (Pour l’Inde) un partenaire CSP peut entrer les informations de son compte PayU Money, telles que l’ID client PayU et le mot de passe. Les partenaires peuvent obtenir plus d' [https://developer.payumoney.com/](https://developer.payumoney.com/)informations sur.

  - Créez un compte PayU Money si vous n’en avez pas déjà un. Pour ouvrir un compte PayU Money, visitez [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/). Ce compte sera utilisé par PayU pour créditer les paiements effectués par les clients.

## <a name="customer-experience-scenarios"></a>Scénarios de l’expérience utilisateur

### <a name="new-customer-sign-up-scenario"></a>Scénario d’inscription à un nouveau client

- Par défaut, le site Web est disponible publiquement et affiche le catalogue du partenaire sur la page d’accueil.

- Les clients peuvent désormais appartenir à un grand nombre de [pays clients](#customer-countries).

- L’accent est mis sur les pays de l’Association européenne de libre-échange (AELE), Amérique du Nord, le Japon, l’Inde, l’Australie et la Nouvelle-Zélande.
  - Cette fonctionnalité utilise la prise en charge des autorisations régionales dans le kit de développement logiciel (SDK) de l’espace partenaires.

- Les clients peuvent sélectionner une offre dans le catalogue à acheter.
  - Ils peuvent ajouter leur nom de client, leur adresse et les informations relatives au domaine.

- Les clients sont dirigés vers l’expérience d’extraction PayPal ou PayU (pour l’Inde). Les clients peuvent fournir un paiement à l’aide des éléments suivants :
  - Son compte PayPal ou PayU (pour l’Inde) existant
  - Instruments de financement pris en charge dans leur pays par PayPal ou PayU (pour l’Inde). Celles-ci peuvent inclure des cartes de crédit, des cartes de débit et des comptes bancaires, le cas échéant.

- Un locataire client est créé pour ce client. Une fois l’ordre des locataires créé, les clients sont fournis avec le nom d’utilisateur, le mot de passe et les détails de l’abonnement.
  - Les clients peuvent enregistrer le nom d’utilisateur et le mot de passe pour rester connecté pour d’autres achats.
  - Chaque abonnement est acheté pendant un an et les clients peuvent le renouveler dans les 30 jours précédant la date de fin de l’abonnement.

### <a name="view-prior-purchases-scenario"></a>Afficher le scénario d’achats antérieurs

- Le client se connecte avec le nom d’utilisateur et le mot de passe du locataire client et accède à la section **Mes commandes** .

- Les clients peuvent accéder à la page **Mes commandes** où ils peuvent consulter les abonnements achetés et effectuer des mises à jour si nécessaire.

- Les clients peuvent accéder à la page **mes abonnements** où ils peuvent afficher tous les abonnements (basés sur des licences et basés sur l’utilisation), y compris ceux qui sont conservés dans l’espace partenaires.

### <a name="add-seats-to-existing-subscriptions-scenario"></a>Ajouter des sièges à un scénario d’abonnements existants

- Dans la section **Mes commandes** , les clients peuvent ajouter des sièges à des abonnements existants. Les clients peuvent ajouter des sièges à tout moment pendant l’année d’un abonnement.

- Chaque siège ajouté ne change pas la date de fin de l’abonnement. Toutefois, le prix de l’abonnement change en fonction de la date à laquelle vous ajoutez le siège et de la date de l’année. La tarification est calculée au prorata sur une base quotidienne pour ne payer que les jours restants de l’année.

### <a name="add-more-subscriptions-scenario"></a>Ajouter d’autres scénarios d’abonnements

- Les clients peuvent acheter n’importe quel nombre d’abonnements à tout moment à partir de la section **Ajouter des abonnements** sous **Mes commandes**.

- Un client peut sélectionner un abonnement, ajouter une quantité et payer pour terminer la transaction et commencer à utiliser immédiatement l’abonnement. Si un client est un client pré-approuvé, l’abonnement peut être utilisé immédiatement et une facture est envoyée au client pour le paiement.

### <a name="renew-subscription-scenario"></a>Scénario de renouvellement d’abonnement

- Un client peut renouveler un abonnement au cours des 30 derniers jours précédant la date de fin de l’abonnement.

- Cela est disponible uniquement au cours des 30 derniers jours.

- Si elle n’est pas renouvelée au cours des 30 derniers jours, l’abonnement est supprimé de la liste des abonnements pour ce locataire client.

- Vous ne pouvez pas mettre à jour la quantité pendant le renouvellement.

### <a name="payments-scenario"></a>Scénario de paiements

- Si le client est pré-approuvé pour les transactions par l’administrateur, l’expérience de paiement n’est pas présentée dans les scénarios ci-dessus. Au lieu de cela, le partenaire peut envoyer la facture de paiement au client préalablement approuvé.

- Pour tous les nouveaux achats, vous pouvez ajouter des sièges, ajouter des abonnements et les renouveler. Un client peut payer un partenaire à l’aide de ce site Web via PayPal ou PayU (pour l’Inde).

- Ce site Web est intégré à PayPal ou PayU (pour l’Inde) et permet aux partenaires d’accepter des paiements de la part de leurs clients. PayPal ou PayU (pour l’Inde) crédite ce montant dans le compte d’un partenaire. PayPal ou PayU (pour l’Inde) la gestion des comptes bancaires est en dehors de ce site Web et est gérée respectivement sur PayPal.com ou PayUmoney.com.

- Cela dépend des partenaires qui configurent leur configuration de paiement PayPal orPayU (pour l’Inde) sur PayPal.com ou PayUmoney.com. Microsoft n’enregistre pas ces informations ou les transactions de paiement réelles résultant de l’utilisation de cette option.

### <a name="prorated-pricing-scenario"></a>Scénario de tarification au prorata

- Ce site Web prend en charge le tarif au prorata dans les cas où les clients ajoutent des sièges à un abonnement existant.

- Chaque abonnement expire au bout d’un an et ne peut pas être modifié une fois l’abonnement acheté.

- La date de fin de l’abonnement n’est pas modifiée par l’ajout de sièges supplémentaires. Les clients sont facturés pour le nombre de jours restants jusqu’à la date de fin. Par exemple, si le coût d’un abonnement est de $365, et que vous ajoutez un autre siège le deuxième jour, le prix du nouveau siège sera de $364. Si vous ajoutez un autre siège 10 jours plus tard, le prix sera de $354.
