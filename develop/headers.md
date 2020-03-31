---
title: En-têtes REST de l’espace partenaires
description: Les en-têtes de requête et de réponse HTTP suivants sont pris en charge par l’API REST de l’espace partenaires.
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e58c10b43021d344e2dbe0ba5b6b698c04d0124e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416556"
---
# <a name="partner-center-rest-headers"></a>En-têtes REST de l’espace partenaires


**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les en-têtes de requête et de réponse HTTP suivants sont pris en charge par l’API REST de l’espace partenaires. Tous les appels d’API n’acceptent pas tous les en-têtes.

## <a name="span-idrequest_headersspan-idrequest_headersspan-idrequest_headersrequest-headers"></a><span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>en-têtes de demande


Les en-têtes de requête HTTP suivants sont pris en charge par l’API REST de l’espace partenaires.

| En-tête                       | Description                                                                                                                                                                                                                                                                            | Type de valeur |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Autorisation :               | Obligatoire. Jeton d’autorisation au format de &lt;jeton&gt; de porteur.                                                                                                                                                                                                                    | chaîne     |
| Valide                      | Spécifie le type de demande et de réponse, « application/json ».                                                                                                                                                                                                                           | chaîne     |
| MS-RequestId :                | Identificateur unique de l’appel, utilisé pour garantir la présence d'un ID (id-potency). En cas de délai d’expiration, l’appel de nouvelle tentative doit inclure la même valeur. Lors de la réception d’une réponse (réussite ou échec métier), la valeur doit être réinitialisée pour l’appel suivant.                                            | GUID       |
| MS-CorrelationId :            | Identificateur unique de l’appel, utile dans les journaux et les suivis réseau pour la résolution des erreurs. La valeur doit être réinitialisée pour chaque appel. Toutes les opérations doivent inclure cet en-tête. Pour plus d’informations, consultez les informations d’ID de corrélation dans [test et Debug](test-and-debug.md). | GUID       |
| MS-Contract-version :         | Obligatoire. Spécifie la version de l’API demandée ; en général, API-version : v1, sauf indication contraire dans la section [scénarios](scenarios.md) .                                                                                                                                  | chaîne     |
| If-Match:                    | Utilisé pour le contrôle d’accès concurrentiel. Certains appels d’API nécessitent la transmission de l’ETag via l’en-tête If-Match. L’ETag étant généralement définie sur la ressource, elle doit obtenir (GET) la plus récente. Pour plus d’informations, consultez les informations sur l’ETag dans [test et débogage](test-and-debug.md).                | chaîne     |
| MS-PartnerCenter-application | Ce paramètre est facultatif. Spécifie le nom de l’application qui utilise l’API REST de l’espace partenaires.                                                                                                                                                                                             | chaîne     |
| Paramètres régionaux X :                    | Ce paramètre est facultatif. Spécifie la langue dans laquelle les tarifs sont retournés. La valeur par défaut est « en-US ». Pour obtenir la liste des valeurs prises en charge, consultez [langues et paramètres régionaux pris en charge par l’espace partenaires](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | chaîne     |

 

## <a name="span-idresponse_headersspan-idresponse_headersspan-idresponse_headersresponse-headers"></a><span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>en-têtes de réponse


Les en-têtes de réponse HTTP suivants peuvent être retournés par l’API REST de l’espace partenaires.

| En-tête            | Description                                                                                                                                                                                                                                 | Type de valeur |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Valide           | Spécifie le type de demande et de réponse, « application/json ».                                                                                                                                                                                | chaîne     |
| MS-RequestId :     | Identificateur unique de l’appel, utilisé pour garantir la présence d'un ID (id-potency). En cas de délai d’expiration, l’appel de nouvelle tentative doit inclure la même valeur. Lors de la réception d’une réponse (réussite ou échec métier), la valeur doit être réinitialisée pour l’appel suivant. | GUID       |
| MS-CorrelationId : | Identificateur unique de l’appel, utile dans les journaux et les suivis réseau pour la résolution des erreurs. La valeur doit être réinitialisée pour chaque appel. Toutes les opérations doivent inclure cet en-tête.                                                       | GUID       |

 

 

 




