---
title: Ressources de l’accord
description: La ressource de contrat représente un contrat de client Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e59debb59700f7d2d4f0eba9dc156c325b3688d
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022666"
---
# <a name="agreement-resources"></a>Ressources de l’accord

**S’applique à :**

- Espace partenaires

La ressource d' **accord** est actuellement prise en charge par l’espace partenaires dans le cloud public Microsoft uniquement. Elle ne s’applique pas aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La ressource de **contrat** représente un contrat de client Microsoft Cloud.

## <a name="agreement"></a>Contrat

La ressource de **contrat** représente les détails de la certification fournie par le partenaire.

| Propriété       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | Identificateur d’objet de l’utilisateur connecté dans le locataire partenaire qui fournit la confirmation pour le compte de l’organisation partenaire. Lorsque vous utilisez l’authentification d’application + utilisateur pour créer une ressource de contrat, l’espace partenaires dérive automatiquement la valeur de l’attribut **userid** du jeton App + User.                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | Informations sur l’utilisateur de l’organisation client qui a accepté le contrat, y compris : **FirstName**, **LastName**, **email**et **phoneNumber** (facultatif). |
| dateAgreed     | Chaîne au format date/heure UTC | Date à laquelle le client a accepté le contrat.                                 |
| templateId     |string                          | Identificateur unique de l’accord accepté par le client. |
| type           |string                          | Type de contrat. Actuellement, les valeurs prises en charge incluent **MicrosoftCloudAgreement** et **MicrosoftCustomerAgreement**.|
| agreementLink  | string                         | URL du modèle d’accord.                                                    |
