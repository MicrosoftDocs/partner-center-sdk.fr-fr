---
title: Ressources de demande de service
description: Les partenaires peuvent traiter les demandes de service au nom de leurs partenaires pour signaler les services d’interruptions fournis par Microsoft ou pour demander un support technique qu’ils ne peuvent pas fournir.
ms.assetid: E9FBF7D8-A7E8-4DC6-B370-8339B9EE16B7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e1fab576e69242a50549efc719f98eafad1ad9de
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488049"
---
# <a name="service-request-resources"></a>Ressources de demande de service


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les partenaires peuvent traiter les demandes de service au nom de leurs partenaires pour signaler les services d’interruptions fournis par Microsoft ou pour demander un support technique qu’ils ne peuvent pas fournir.

## <a name="span-idservicerequestspan-idservicerequestspan-idservicerequestservicerequest"></a><span id="ServiceRequest"/><span id="servicerequest"/><span id="SERVICEREQUEST"/>ServiceRequest


Décrit une demande de service déposée par un partenaire, y compris comment cette demande progresse.

| Propriété         | Type                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Titre            | chaîne                                                        | Titre de la demande de service.                                                           |
| Description      | chaîne                                                        | Description.                                                                     |
| Sévérité         | chaîne                                                        | Gravité : « inconnu », « critique », « modéré » ou « minimal ».                       |
| SupportTopicId   | chaîne                                                        | ID de la rubrique de support.                                                         |
| SupportTopicName | chaîne                                                        | Nom de la rubrique de support.                                                       |
| Id               | chaîne                                                        | ID de la demande de service.                                                       |
| État           | chaîne                                                        | État de la demande de service : « None », « Open », « Closed » ou « attention\_needed ». |
| Organisation     | [ServiceRequestOrganization](#servicerequestorganization)     | Organisation pour laquelle la demande de service est créée.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Contact principal sur la demande de service.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | « Dernière mise à jour par » permet de contacter les modifications apportées à la demande de service.                        |
| ProductName      | chaîne                                                        | Nom du produit qui correspond à la demande de service.                     |
| ProductId        | chaîne                                                        | ID du produit.                                                               |
| CreatedDate      | date                                                          | Date de création de la demande de service.                                          |
| LastModifiedDate & | date                                                          | Date à laquelle la demande de service a été modifiée pour la dernière fois.                                 |
| LastClosedDate   | date                                                          | Date de la dernière fermeture de la demande de service.                                   |
| FileLinks        | Tableau de ressources [FileInfo](utility-resources.md#fileinfo) | Collection de liens de fichiers qui se rapportent à la demande de service.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Une note peut être ajoutée à une demande de service existante.                                  |
| Remarques            | Tableau de [ServiceRequestNotes](#servicerequestnote)           | Collection de remarques ajoutées à la demande de service.                                  |
| CountryCode      | chaîne                                                        | Pays correspondant à la demande de service.                                    |
| Attributs       | ResourceAttributes                                            | Attributs de métadonnées correspondant à la demande de service.                        |

 

## <a name="span-idservicerequestcontactspan-idservicerequestcontactspan-idservicerequestcontactservicerequestcontact"></a><span id="ServiceRequestContact"/><span id="servicerequestcontact"/><span id="SERVICEREQUESTCONTACT"/>ServiceRequestContact


Décrit un contact qui crée ou modifie une demande de service.

| Propriété     | Type                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organisation | [ServiceRequestOrganization](#servicerequestorganization) | Organisation pour laquelle la demande de service est créée. |
| ContactId    | chaîne                                                    | ID unique du contact.                               |
| LastName     | chaîne                                                    | Nom du contact.                          |
| Prénom    | chaîne                                                    | Prénom du contact.                         |
| E-mail        | chaîne                                                    | Adresse de messagerie du contact.                              |
| PhoneNumber  | chaîne                                                    | Numéro de téléphone du contact.                       |

 

## <a name="span-idservicerequestnotespan-idservicerequestnotespan-idservicerequestnoteservicerequestnote"></a><span id="ServiceRequestNote"/><span id="servicerequestnote"/><span id="SERVICEREQUESTNOTE"/>ServiceRequestNote


Décrit une note jointe à une demande de service.

| Propriété      | Type   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | chaîne | Nom du créateur de la note.         |
| CreatedDate   | date   | Date et heure de création de la note. |
| Text          | chaîne | Texte de la note.                        |

 

## <a name="span-idservicerequestorganizationspan-idservicerequestorganizationspan-idservicerequestorganizationservicerequestorganization"></a><span id="ServiceRequestOrganization"/><span id="servicerequestorganization"/><span id="SERVICEREQUESTORGANIZATION"/>ServiceRequestOrganization


Décrit l’Organisation pour laquelle la demande de service est créée.

| Propriété    | Type   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | chaîne | ID unique de l’organisation.    |
| Nom        | chaîne | Nom de l’organisation.         |
| PhoneNumber | chaîne | Numéro de téléphone de l’organisation. |

 

## <a name="span-idsupporttopicspan-idsupporttopicspan-idsupporttopicsupporttopic"></a><span id="SupportTopic"/><span id="supporttopic"/><span id="SUPPORTTOPIC"/>SupportTopic


Décrit une rubrique de support. Les demandes de service spécifient une rubrique de support pour s’assurer qu’elles sont traitées rapidement et efficacement.

| Propriété    | Type               | Description                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Nom        | chaîne             | Nom de la rubrique de support.                                |
| Description | chaîne             | Description de la rubrique de support.                         |
| Id          | chaîne             | ID unique de la rubrique de support.                           |
| Attributs  | ResourceAttributes | Attributs de métadonnées correspondant à la demande de service. |

 

 

 




