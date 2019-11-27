---
title: Ressources de l’accord
description: La ressource de contrat représente un contrat de client Microsoft Cloud.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2cf620d63da14e014a17017006346f80a7a3fe4c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489259"
---
# <a name="agreement-resources"></a>Ressources de l’accord

S’applique à :

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
| IDutilisateur         | chaîne                         | Identificateur d’objet de l’utilisateur connecté dans le locataire partenaire qui fournit la confirmation pour le compte de l’organisation partenaire. Lorsque vous utilisez l’authentification d’application + utilisateur pour créer une ressource de contrat, l’espace partenaires dérive automatiquement la valeur de l’attribut **userid** du jeton App + User.                                                                             |
| PrimaryContact | [Communiquer](./utility-resources.md#contact) | Informations sur l’utilisateur de l’organisation client qui a accepté le contrat de Microsoft Cloud, notamment les suivants : **FirstName**, **LastName**, **email**et **phoneNumber** (facultatif). |
| dateAgreed     | chaîne au format date/heure UTC | Date à laquelle le client a accepté le contrat.                                 |
| templateId     |chaîne                          | Identificateur unique de l’accord accepté par le client. |
| type           |chaîne                          | Type de contrat. Actuellement, les valeurs prises en charge incluent **MicrosoftCloudAgreement** et **MicrosoftCustomerAgreement**.|
| agreementLink  | chaîne                         | URL du modèle d’accord.                                                    |
