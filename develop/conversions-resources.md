---
title: Ressources de conversions
description: Les ressources de conversion prennent en charge la conversion d’un abonnement d’évaluation en abonnement payant.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 10526af03ee66b81d790816dfa9925c28e410114
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096388"
---
# <a name="conversions-resources"></a>Ressources de conversions

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les ressources de conversion prennent en charge la conversion d’un abonnement d’évaluation en abonnement payant.

## <a name="conversion"></a>Conversion

Contient les informations utilisées pour convertir un abonnement d’évaluation en abonnement payant.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| offerId | string | Identificateur de l’offre d’origine de l’offre d’essai. |
| targetOfferId | string | Identificateur de l’offre de l’offre cible. |
| orderId | string | Identificateur de l’ordre. |
| quantité | int | Nombre de licences. La valeur par défaut est le nombre de licences dans l’abonnement d’évaluation. |
| billingCycle | string | Indique la fréquence à laquelle le partenaire est facturé pour l’abonnement. Valeurs possibles : **mensuelle** (le partenaire est facturé mensuellement), **annuelle** (le partenaire est facturé annuellement) ou **None** (le partenaire n’est pas facturé. Utilisé pour les abonnements d’évaluation). |

## <a name="conversionerror"></a>ConversionError

Représente une erreur qui s’est produite pendant la conversion.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| code | string | Code d’erreur associé au problème. Valeurs possibles : **other** (erreur générale), **ConversionsNotFound** (impossible de trouver les conversions de l’abonnement d’évaluation vers lequel effectuer la conversion).
| description | string | Texte convivial qui décrit le problème. |

## <a name="conversionresult"></a>ConversionResult

Représente le résultat de la conversion d’un abonnement.

| Propriété       | Type                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | Identificateur de l’abonnement.                                           |
| offerId        | string                              | Identificateur d’offre d’origine.                                         |
| targetOfferId  | string                              | Identificateur de l’offre de l’offre cible.                             |
| erreur          | [ConversionError](#conversionerror) | Erreur rencontrée lors de la tentative de conversion, le cas échéant. |