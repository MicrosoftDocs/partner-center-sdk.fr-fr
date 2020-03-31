---
title: Codes d’erreur REST de l’espace partenaires
description: Description des codes d’erreur et des réponses de réussite à partir des API de l’espace partenaires.
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2bb945de632b0bf18eea73db739ad0aa6085eecc
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415644"
---
# <a name="partner-center-rest-error-codes"></a>Codes d’erreur REST de l’espace partenaires

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les API REST de l’espace partenaires retournent un objet JSON qui contient un code d’État. Ce code indique si votre demande a réussi ou a échoué.

## <a name="success-responses"></a>Réponses de réussite

Un code d’état **2xx** indique que la demande du client a été correctement reçue, comprise et acceptée.

## <a name="error-codes"></a>Codes d’erreur

Les codes d’état **4xx** et **5xx** suivants indiquent une erreur :

- 400 : requête incorrecte
- 401 : non autorisé
- 403 : interdit
- 404 : introuvable
- 405 : méthode non autorisée
- 406 : non acceptable
- 409 : conflit, code d’erreur
- 412 : échec de la précondition
- 429 : demandes trop nombreuses
- 500 : erreur interne du serveur
- 501 : non implémenté
- 502 : passerelle incorrecte
- 503 : service non disponible
- 504 : délai d’expiration de la passerelle

## <a name="error-responses"></a>Réponses d’erreur

Toute réponse avec un code d’état **4xx** ou **5xx** contient un message d’erreur avec des détails supplémentaires sur la ou les conditions d’erreur rencontrées.

Le tableau et l’exemple de code suivants décrivent le schéma d’une réponse d’erreur :

| Nom        | Type   | Description                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | chaîne | Toujours retourné. Indique le type d’erreur qui s’est produit. Non Null.                                                                                  |
| description | chaîne | Toujours retourné. Décrit l’erreur et fournit des informations de débogage supplémentaires. Non Null, non vide. La longueur maximale est de 1 024 caractères. |
| data        | array  | Retourné uniquement pour certains types d’erreur. Liste d’objets d’erreur.                                                                                           |
| source      | chaîne | Toujours retourné. Source de l’erreur.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```
