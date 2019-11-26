---
title: Conversions resources
description: Conversion resources support the conversion of a trial subscription to a paid subscription.
ms.assetid: 4AE796E3-47D9-428B-8267-A5247B573E0C
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e91e79ce77ac020495c2d09a4bf33dd947231dec
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488899"
---
# <a name="conversions-resources"></a>Conversions resources

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Conversion resources support the conversion of a trial subscription to a paid subscription.

## <a name="conversion"></a>Conversion

Contains information used to convert a trial subscription to a paid subscription.

| Propriété | Tapez | Description |
| -------- | ---- | ----------- |
| offerId | chaîne | The offer identifier of the original, trial offer. |
| targetOfferId | chaîne | The offer identifier for the target offer. |
| orderId | chaîne | The order identifier. |
| quantity | entier | The number of licenses. The default is the number of licenses in the trial subscription. |
| billingCycle | chaîne | Indicates how often the partner is charged for the subscription. Possible values: **Monthly** (partner is billed monthly), **Annual** (partner is billed annually), or **None** (Partner isn't billed. Used for trial subscriptions). |

## <a name="conversionerror"></a>ConversionError

Represents an error that occurred during conversion.

| Propriété | Tapez | Description |
| -------- | ---- | ----------- |
| code | chaîne | The error code associated with the issue. Possible values: **Other** (general error), **ConversionsNotFound** (can't find any conversions for the trial subscription to convert to).
| description | chaîne | The friendly text describing the issue. |

## <a name="conversionresult"></a>ConversionResult

Represents the result of performing a subscription conversion.

| Propriété       | Tapez                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | chaîne                              | The subscription identifier.                                           |
| offerId        | chaîne                              | The original offer identifier.                                         |
| targetOfferId  | chaîne                              | The offer identifier for the target offer.                             |
| erreur          | [ConversionError](#conversionerror) | The error encountered while attempting the conversion, if applicable.. |