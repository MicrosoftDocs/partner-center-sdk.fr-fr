---
title: Développement pour l’espace partenaires pour les clouds Microsoft nationaux
description: Différences du kit de développement logiciel (SDK) de l’espace partenaires lors du développement de pour les clouds Microsoft nationaux.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.assetid: 13D45776-4837-48F5-AB8B-605FD1D3D52D
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c2f8e9e61c02b037b817305989bbad430c6fd579
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154231"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Développement pour l’espace partenaires pour les clouds Microsoft nationaux

**S’applique à :**

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’espace partenaires possède un ensemble de documents SDK. Toutefois, certaines fonctionnalités peuvent ne pas être disponibles dans les versions de l’espace partenaires pour les clouds nationaux Microsoft.

Les développeurs doivent tenir compte des modifications apportées au kit de développement logiciel (SDK) pour les versions suivantes de l’espace partenaires :

- [Espace partenaires géré par 21Vianet](#partner-center-operated-by-21vianet)
- [Espace partenaires de Microsoft Cloud Germany](#partner-center-for-microsoft-cloud-germany)
- [Espace partenaires de Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Chaque article du kit de développement logiciel (SDK) Partner Center répertorie les versions appropriées de l’espace partenaires. Chaque article de référence géré répertorie également les versions appropriées de l’espace partenaires dans la section **Configuration requise** .

## <a name="partner-center-operated-by-21vianet"></a>Espace partenaires géré par 21Vianet

Les différences entre *l’espace partenaires et* l' *espace partenaires géré par 21ViaNet* sont les suivantes :

- Vous ne pouvez pas réinitialiser par programmation un mot de passe pour un utilisateur client ou un utilisateur partenaire complet.

- Les abonnements à Azure ne sont pas disponibles.

- Vous ne pouvez pas gérer les licences pour l’utilisateur de votre client. Au lieu de cela, vos clients doivent utiliser le centre d’administration Office 365 pour gérer leurs licences.

- Toutes les demandes de support sont gérées via l’espace partenaires géré par 21Vianet. Les demandes de service et les mises à jour de service ne s’appliquent pas.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Espace partenaires de Microsoft Cloud Germany

> [!IMPORTANT]
> En fonction de l’évolution des besoins des clients, notre stratégie de Cloud pour l’Allemagne se concentrera sur la livraison des nouvelles régions Cloud en Allemagne qui sont cohérentes avec notre offre Cloud mondiale. Dans cette optique, nous n’accepterons plus de nouveaux clients ou nous ne déploierons plus de nouveaux services à partir de Microsoft Cloud actuellement disponible en Allemagne. Les clients existants peuvent continuer à utiliser les services Cloud actuels actuellement disponibles, que nous allons conserver avec les mises à jour de sécurité nécessaires.
>
> Dorénavant, les nouveaux clients ont la possibilité d’utiliser les régions européennes actuellement disponibles ou les nouvelles régions d’Allemagne lorsqu’elles seront disponibles. Pour plus d’informations, consultez [Microsoft offrira des services de cloud à partir de nouveaux centres de données en Allemagne](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Les *différences entre l’espace partenaires* et l' *espace partenaires pour Microsoft Cloud Allemagne* sont les suivantes :

- Les partenaires ne peuvent pas créer d’utilisateurs pour l’organisation de leur client ou attribuer des rôles.
  - Les partenaires peuvent lire les champs, mais ils ne peuvent pas les écrire ou les mettre à jour.
  - Les partenaires doivent créer ou mettre à jour manuellement les utilisateurs de leurs clients dans le centre d’administration Office 365 ou via le Portail Azure. Consultez [Azure Active Directory documentation](https://docs.microsoft.com/azure/active-directory/).

- Vous ne pouvez pas gérer les licences des utilisateurs de vos clients à l’aide de l’espace partenaires pour Microsoft Cloud portail ou les API Allemagne. Au lieu de cela, vous devez utiliser le centre d’administration Office 365 ou la gestion des licences Azure active directement Group (bientôt disponible) pour gérer leurs licences.
  - (Facultatif) vous pouvez utiliser Azure AD API Graph. Voir [Ajouter ou supprimer des licences d’un utilisateur](https://msdn.microsoft.com/library/azure/ad/graph/api/functions-and-actions#assignLicense). Pour l’espace partenaires pour Microsoft Cloud Allemagne, veillez à utiliser le point `https://graph.cloudapi.de` de terminaison `https://graph.windows.net`Graph au lieu de.

- Vous ne pouvez pas réinitialiser par programmation un mot de passe pour un utilisateur client ou un utilisateur partenaire complet. Utilisez le centre d’administration Office 365 ou Portail Azure. Consultez [Réinitialiser le mot de passe d’un utilisateur dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-users-reset-password-azure-portal/). Pour l’étape 1, vous devez vous connecter au Portail Azure pour Microsoft Cloud Allemagne.

- Les développeurs doivent inscrire manuellement leur ID d’application pour intégrer les fonctionnalités du kit de développement logiciel (SDK) de l’API de l’espace partenaires dans leur application pour l’espace partenaires pour Microsoft Cloud Allemagne. Pour plus d’informations, consultez [inscrire les détails de l’application pour l’espace partenaires pour Microsoft national Cloud](https://docs.microsoft.com/partner-center/develop/create-apps-for-partner-center-for-microsoft-national-clouds).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Espace partenaires de Microsoft Cloud for US Government

Les *différences entre l’espace partenaires* et l' *espace partenaires pour Microsoft Cloud pour les administrations américaines* sont les suivantes :

- Les abonnements Office 365 ne sont actuellement pas disponibles pour l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis.

- Les partenaires existants qui prennent en charge Microsoft Cloud pour le gouvernement des États-Unis doivent créer de nouveaux comptes dans l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis.

- Les Microsoft Cloud pour les clients du gouvernement des États-Unis doivent faire une transaction avec un seul partenaire.
  - Les relations multicanaux et multipartenaires et de demande avec un client existant au sein de Microsoft Cloud pour les scénarios gouvernementaux des États-Unis ne s’appliquent pas. Cette limitation est due au fait qu’Office 365 n’est pas disponible actuellement.

- Les partenaires ne peuvent pas créer d’utilisateurs pour l’organisation de leur client ou attribuer des rôles.
  - Les partenaires peuvent lire les champs, mais ils ne peuvent pas les écrire ou les mettre à jour. Les partenaires doivent créer ou mettre à jour manuellement les utilisateurs de leurs clients dans le Portail Azure. Consultez [Azure Active Directory documentation](https://docs.microsoft.com/azure/active-directory/).

- Vous ne pouvez pas réinitialiser par programmation un mot de passe pour un utilisateur client ou un utilisateur partenaire complet. utilisez le portail Azure. Consultez [Réinitialiser le mot de passe d’un utilisateur dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-users-reset-password-azure-portal). Pour l’étape 1, vous devez vous connecter au Portail Azure pour Microsoft Cloud pour le gouvernement des États-Unis.

- Les points de terminaison REST de l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis sont `https://api.partnercenter.microsoft.com`les mêmes que pour l’espace partenaires :.

- Les développeurs doivent inscrire manuellement leur ID d’application pour intégrer les fonctionnalités du kit de développement logiciel (SDK) d’API de l’espace partenaires dans leur application pour l’espace partenaires pour Microsoft Cloud pour le gouvernement des États-Unis. Pour plus d’informations, consultez [inscrire les détails de l’application pour l’espace partenaires pour Microsoft national Cloud](https://docs.microsoft.com/partner-center/develop/create-apps-for-partner-center-for-microsoft-national-clouds).
