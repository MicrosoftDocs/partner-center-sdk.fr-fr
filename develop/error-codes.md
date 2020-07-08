---
title: Codes d’erreur REST de l’Espace partenaires
description: Description des codes d’erreur et des réponses de réussite à partir des API de l’espace partenaires.
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b75f7fa6b9b82c2b1744a21fa0dbac95aa7c7acd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093998"
---
# <a name="partner-center-rest-error-codes"></a>Codes d’erreur REST de l’Espace partenaires

**S’applique à :**

- Espace partenaires
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
| code        | string | Toujours retourné. Indique le type d’erreur qui s’est produit. Non Null.                                                                                  |
| description | string | Toujours retourné. Décrit l’erreur et fournit des informations de débogage supplémentaires. Non Null, non vide. La longueur maximale est de 1 024 caractères. |
| data        | tableau  | Retourné uniquement pour certains types d’erreur. Liste d’objets d’erreur.                                                                                           |
| source      | string | Toujours retourné. Source de l’erreur.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
}
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```
