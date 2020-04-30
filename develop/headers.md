---
title: En-têtes REST de l’Espace partenaires
description: Les en-têtes de requête et de réponse HTTP suivants sont pris en charge par l’API REST de l’espace partenaires.
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5ec3532ed30b3a9ff933bbda4e4923862091c895
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157141"
---
# <a name="partner-center-rest-headers"></a>En-têtes REST de l’Espace partenaires

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les en-têtes de requête et de réponse HTTP suivants sont pris en charge par l’API REST de l’espace partenaires. Tous les appels d’API n’acceptent pas tous les en-têtes.

## <a name="rest-request-headers"></a>En-têtes de demande REST

Les en-têtes de requête HTTP suivants sont pris en charge par l’API REST de l’espace partenaires.

| En-tête                       | Description                                                                                                                                                                                                                                                                            | Type de valeur |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Autorisation :               | Obligatoire. Jeton d’autorisation au format de &lt;jeton&gt; de porteur.                                                                                                                                                                                                                    | string     |
| Valide                      | Spécifie le type de demande et de réponse, « application/json ».                                                                                                                                                                                                                           | string     |
| MS-RequestId :                | Identificateur unique de l’appel, utilisé pour garantir la présence d'un ID (id-potency). En cas de dépassement du délai d’attente, l’appel de nouvelle tentative doit inclure la même valeur. Lors de la réception d’une réponse (réussite ou échec métier), la valeur doit être réinitialisée pour l’appel suivant.                                            | GUID       |
| MS-CorrelationId :            | Identificateur unique de l’appel, utile dans les journaux et les suivis réseau pour la résolution des erreurs. La valeur doit être réinitialisée pour chaque appel. Toutes les opérations doivent inclure cet en-tête. Pour plus d’informations, consultez les informations d’ID de corrélation dans [test et Debug](test-and-debug.md). | GUID       |
| MS-Contract-version :         | Obligatoire. Spécifie la version de l’API demandée ; en général, API-version : v1, sauf indication contraire dans la section [scénarios](scenarios.md) .                                                                                                                                  | string     |
| If-Match:                    | Utilisé pour le contrôle d’accès concurrentiel. Certains appels d’API nécessitent la transmission de l’ETag via l’en-tête If-Match. L’ETag étant généralement définie sur la ressource, elle doit obtenir (GET) la plus récente. Pour plus d’informations, consultez les informations sur l’ETag dans [test et débogage](test-and-debug.md).                | string     |
| MS-PartnerCenter-application | facultatif. Spécifie le nom de l’application qui utilise l’API REST de l’espace partenaires.                                                                                                                                                                                             | string     |
| Paramètres régionaux X :                    | facultatif. Spécifie la langue dans laquelle les tarifs sont retournés. La valeur par défaut est « en-US ». Pour obtenir la liste des valeurs prises en charge, consultez [langues et paramètres régionaux pris en charge par l’espace partenaires](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | string     |

## <a name="rest-response-headers"></a>En-têtes de réponse REST

Les en-têtes de réponse HTTP suivants peuvent être retournés par l’API REST de l’espace partenaires.

| En-tête            | Description                                                                                                                                                                                                                                 | Type de valeur |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Valide           | Spécifie le type de demande et de réponse, « application/json ».                                                                                                                                                                                | string     |
| MS-RequestId :     | Identificateur unique de l’appel, utilisé pour garantir la présence d'un ID (id-potency). En cas de dépassement du délai d’attente, l’appel de nouvelle tentative doit inclure la même valeur. Lors de la réception d’une réponse (réussite ou échec métier), la valeur doit être réinitialisée pour l’appel suivant. | GUID       |
| MS-CorrelationId : | Identificateur unique pour l’appel. Cette valeur est utile pour le dépannage des journaux et des traces réseau pour trouver l’erreur. La valeur doit être réinitialisée pour chaque appel. Toutes les opérations doivent inclure cet en-tête.                                                       | GUID       |
