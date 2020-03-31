---
title: Ressources de l’accord
description: La ressource de contrat représente un contrat de client Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 105855b5e0881abd3e44ba784182ecb606b95093
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413291"
---
# <a name="agreement-resources"></a>Ressources de l’accord

S'applique à :

- Centre pour partenaires

La ressource d' **accord** est actuellement prise en charge par l’espace partenaires dans le cloud public Microsoft uniquement. Elle n’est pas applicable aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La ressource de **contrat** représente un contrat de client Microsoft Cloud.

## <a name="agreement"></a>Contrat

La ressource de **contrat** représente les détails de la certification fournie par le partenaire.

| Propriété       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| IDutilisateur         | chaîne                         | Identificateur d’objet de l’utilisateur connecté dans le locataire partenaire qui fournit la confirmation pour le compte de l’organisation partenaire. Lorsque vous utilisez l’authentification d’application + utilisateur pour créer une ressource de contrat, l’espace partenaires dérive automatiquement la valeur de l’attribut **userid** du jeton App + User.                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | Informations sur l’utilisateur de l’organisation client qui a accepté le contrat, y compris : **FirstName**, **LastName**, **email**et **phoneNumber** (facultatif). |
| dateAgreed     | Chaîne au format date/heure UTC | Date à laquelle le client a accepté le contrat.                                 |
| templateId     |chaîne                          | Identificateur unique de l’accord accepté par le client. |
| type           |chaîne                          | Type de contrat. Actuellement, les valeurs prises en charge incluent **MicrosoftCloudAgreement** et **MicrosoftCustomerAgreement**.|
| agreementLink  | chaîne                         | URL du modèle d’accord.                                                    |
