---
title: En-têtes REST de l’espace partenaires
description: Les en-têtes de requête et de réponse HTTP suivants sont pris en charge par l’API REST de l’espace partenaires.
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f5adf9a458148c1e68cf17a3014cb1931e8860be
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487109"
---
# <a name="partner-center-rest-headers"></a>En-têtes REST de l’espace partenaires


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les en-têtes de requête et de réponse HTTP suivants sont pris en charge par l’API REST de l’espace partenaires. Tous les appels d’API n’acceptent pas tous les en-têtes.

## <a name="span-idrequest_headersspan-idrequest_headersspan-idrequest_headersrequest-headers"></a><span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>en-têtes de demande


Les en-têtes de requête HTTP suivants sont pris en charge par l’API REST de l’espace partenaires.

| En-tête                       | Description                                                                                                                                                                                                                                                                            | Type de valeur |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| L'               | Obligatoire. Le jeton d’autorisation au format porteur &lt;jeton&gt;.                                                                                                                                                                                                                    | chaîne     |
| Valide                      | Spécifie le type de demande et de réponse, « application/JSON ».                                                                                                                                                                                                                           | chaîne     |
| MS-RequestId :                | Identificateur unique de l’appel, utilisé pour garantir l’ID-potence. Dans le cas d’un délai d’attente, l’appel de nouvelle tentative doit inclure la même valeur. Lors de la réception d’une réponse (réussite ou échec de l’entreprise), la valeur doit être réinitialisée pour l’appel suivant.                                            | GUID       |
| MS-CorrelationId :            | Identificateur unique de l’appel, utile dans les journaux et les suivis réseau pour la résolution des erreurs. La valeur doit être réinitialisée pour chaque appel. Toutes les opérations doivent inclure cet en-tête. Pour plus d’informations, consultez les informations d’ID de corrélation dans [test et Debug](test-and-debug.md). | GUID       |
| MS-Contract-version :         | Obligatoire. Spécifie la version de l’API demandée ; en général, API-version : v1, sauf indication contraire dans la section [scénarios](scenarios.md) .                                                                                                                                  | chaîne     |
| If-Match :                    | Utilisé pour le contrôle d’accès concurrentiel. Certains appels d’API requièrent la transmission de l’ETag via l’en-tête If-Match. L’ETag est généralement sur la ressource et, par conséquent, requiert la mise à jour de la dernière version. Pour plus d’informations, consultez les informations sur l’ETag dans [test et débogage](test-and-debug.md).                | chaîne     |
| MS-PartnerCenter-application | Facultatif. Spécifie le nom de l’application qui utilise l’API REST de l’espace partenaires.                                                                                                                                                                                             | chaîne     |
| Paramètres régionaux X :                    | Facultatif. Spécifie la langue dans laquelle les tarifs sont retournés. La valeur par défaut est « en-US ». Pour obtenir la liste des valeurs prises en charge, consultez [langues et paramètres régionaux pris en charge par l’espace partenaires](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | chaîne     |

 

## <a name="span-idresponse_headersspan-idresponse_headersspan-idresponse_headersresponse-headers"></a><span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>en-têtes de réponse


Les en-têtes de réponse HTTP suivants peuvent être retournés par l’API REST de l’espace partenaires.

| En-tête            | Description                                                                                                                                                                                                                                 | Type de valeur |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Valide           | Spécifie le type de demande et de réponse, « application/JSON ».                                                                                                                                                                                | chaîne     |
| MS-RequestId :     | Identificateur unique de l’appel, utilisé pour garantir l’ID-potence. Dans le cas d’un délai d’attente, l’appel de nouvelle tentative doit inclure la même valeur. Lors de la réception d’une réponse (réussite ou échec de l’entreprise), la valeur doit être réinitialisée pour l’appel suivant. | GUID       |
| MS-CorrelationId : | Identificateur unique de l’appel, utile pour les journaux et les suivis réseau pour la résolution des erreurs. La valeur doit être réinitialisée pour chaque appel. Toutes les opérations doivent inclure cet en-tête.                                                       | GUID       |

 

 

 




