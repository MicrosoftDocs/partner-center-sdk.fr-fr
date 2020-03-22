---
title: Ressources de conversions
description: Les ressources de conversion prennent en charge la conversion d’un abonnement d’évaluation en abonnement payant.
ms.assetid: 4AE796E3-47D9-428B-8267-A5247B573E0C
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e91e79ce77ac020495c2d09a4bf33dd947231dec
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082846"
---
# <a name="conversions-resources"></a>Ressources de conversions

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les ressources de conversion prennent en charge la conversion d’un abonnement d’évaluation en abonnement payant.

## <a name="conversion"></a>Conversion

Contient les informations utilisées pour convertir un abonnement d’évaluation en abonnement payant.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| offerId | chaîne | Identificateur de l’offre d’origine de l’offre d’essai. |
| targetOfferId | chaîne | Identificateur de l’offre de l’offre cible. |
| orderId | chaîne | Identificateur de l’ordre. |
| quantity | int | Nombre de licences. La valeur par défaut est le nombre de licences dans l’abonnement d’évaluation. |
| BillingCycle | chaîne | Indique la fréquence à laquelle le partenaire est facturé pour l’abonnement. Valeurs possibles : **mensuelle** (le partenaire est facturé mensuellement), **annuelle** (le partenaire est facturé annuellement) ou **None** (le partenaire n’est pas facturé. Utilisé pour les abonnements d’évaluation). |

## <a name="conversionerror"></a>ConversionError

Représente une erreur qui s’est produite pendant la conversion.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| code | chaîne | Code d’erreur associé au problème. Valeurs possibles : **other** (erreur générale), **ConversionsNotFound** (impossible de trouver les conversions de l’abonnement d’évaluation vers lequel effectuer la conversion).
| description | chaîne | Texte convivial qui décrit le problème. |

## <a name="conversionresult"></a>ConversionResult

Représente le résultat de la conversion d’un abonnement.

| Propriété       | Type                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | chaîne                              | Identificateur d’abonnement.                                           |
| offerId        | chaîne                              | Identificateur d’offre d’origine.                                         |
| targetOfferId  | chaîne                              | Identificateur de l’offre de l’offre cible.                             |
| erreur          | [ConversionError](#conversionerror) | Erreur rencontrée lors de la tentative de conversion, le cas échéant. |