---
title: Ressources de demande de service
description: Les partenaires peuvent traiter les demandes de service au nom de leurs partenaires pour signaler les services d’interruptions fournis par Microsoft ou pour demander un support technique qu’ils ne peuvent pas fournir.
ms.assetid: E9FBF7D8-A7E8-4DC6-B370-8339B9EE16B7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2154d9f166a5e3bac83b6fa57df81c47c715fb6b
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82119795"
---
# <a name="service-request-resources"></a>Ressources de demande de service

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les partenaires peuvent traiter les demandes de service au nom de leurs partenaires pour signaler les services d’interruptions fournis par Microsoft ou pour demander un support technique qu’ils ne peuvent pas fournir.

## <a name="servicerequest"></a>ServiceRequest

Décrit une demande de service déposée par un partenaire, y compris comment cette demande progresse.

| Propriété         | Type                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Intitulé            | string                                                        | Titre de la demande de service.                                                           |
| Description      | string                                                        | Description.                                                                     |
| severity         | string                                                        | Gravité : « inconnu », « critique », « modéré » ou « minimal ».                       |
| SupportTopicId   | string                                                        | ID de la rubrique de support.                                                         |
| SupportTopicName | string                                                        | Nom de la rubrique de support.                                                       |
| Id               | string                                                        | ID de la demande de service.                                                       |
| Statut           | string                                                        | État de la demande de service : « None », « Open », « Closed » ou « attention\_needed ». |
| Organisation     | [ServiceRequestOrganization](#servicerequestorganization)     | Organisation pour laquelle la demande de service est créée.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Contact principal sur la demande de service.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | « Dernière mise à jour par » permet de contacter les modifications apportées à la demande de service.                        |
| ProductName      | string                                                        | Nom du produit qui correspond à la demande de service.                     |
| ProductId        | string                                                        | ID du produit.                                                               |
| CreatedDate      | Date                                                          | Date de création de la demande de service.                                          |
| LastModifiedDate & | Date                                                          | Date à laquelle la demande de service a été modifiée pour la dernière fois.                                 |
| LastClosedDate   | Date                                                          | Date de la dernière fermeture de la demande de service.                                   |
| FileLinks        | Tableau de ressources [FileInfo](utility-resources.md#fileinfo) | Collection de liens de fichiers qui se rapportent à la demande de service.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Une note peut être ajoutée à une demande de service existante.                                  |
| Notes            | Tableau de [ServiceRequestNotes](#servicerequestnote)           | Collection de remarques ajoutées à la demande de service.                                  |
| CountryCode      | string                                                        | Pays correspondant à la demande de service.                                    |
| Attributs       | ResourceAttributes                                            | Attributs de métadonnées correspondant à la demande de service.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Décrit un contact qui crée ou modifie une demande de service.

| Propriété     | Type                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organisation | [ServiceRequestOrganization](#servicerequestorganization) | Organisation pour laquelle la demande de service est créée. |
| ContactId    | string                                                    | ID unique du contact.                               |
| LastName     | string                                                    | Nom du contact.                          |
| FirstName    | string                                                    | Prénom du contact.                         |
| E-mail        | string                                                    | Adresse de messagerie du contact.                              |
| PhoneNumber  | string                                                    | Numéro de téléphone du contact.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Décrit une note jointe à une demande de service.

| Propriété      | Type   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | Nom du créateur de la note.         |
| CreatedDate   | Date   | Date et heure de création de la note. |
| Texte          | string | Texte de la note.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Décrit l’Organisation pour laquelle la demande de service est créée.

| Propriété    | Type   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | string | ID unique de l’organisation.    |
| Nom        | string | Nom de l’organisation.         |
| PhoneNumber | string | Numéro de téléphone de l’organisation. |

## <a name="supporttopic"></a>SupportTopic

Décrit une rubrique de support. Les demandes de service spécifient une rubrique de support pour s’assurer qu’elles sont traitées rapidement et efficacement.

| Propriété    | Type               | Description                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Nom        | string             | Nom de la rubrique de support.                                |
| Description | string             | Description de la rubrique de support.                         |
| Id          | string             | ID unique de la rubrique de support.                           |
| Attributs  | ResourceAttributes | Attributs de métadonnées correspondant à la demande de service. |

