---
title: Service request resources
description: Partners can file service requests on behalf of their partners to report disruptions services provided by Microsoft or to request other technical support that they are incapable of providing.
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
# <a name="service-request-resources"></a>Service request resources


**Applies To**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Partners can file service requests on behalf of their partners to report disruptions services provided by Microsoft or to request other technical support that they are incapable of providing.

## <a name="span-idservicerequestspan-idservicerequestspan-idservicerequestservicerequest"></a><span id="ServiceRequest"/><span id="servicerequest"/><span id="SERVICEREQUEST"/>ServiceRequest


Describes a service request filed by a partner, including how that request is progressing.

| Propriété         | Tapez                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Title            | chaîne                                                        | The service request title.                                                           |
| Description      | chaîne                                                        | The description.                                                                     |
| Sévérité         | chaîne                                                        | The severity: "unknown", "critical", "moderate", or "minimal".                       |
| SupportTopicId   | chaîne                                                        | The id of the support topic.                                                         |
| SupportTopicName | chaîne                                                        | The name of the support topic.                                                       |
| Id               | chaîne                                                        | The id of the service request.                                                       |
| le statut           | chaîne                                                        | The status of the service request: "none", "open", "closed", or "attention\_needed". |
| Organisation     | [ServiceRequestOrganization](#servicerequestorganization)     | Organization for which the service request is created.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primary Contact on the service request.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Last Updated By" contact for changes to the service request.                        |
| ProductName      | chaîne                                                        | The name of the product that corresponds to the service request.                     |
| ProductId        | chaîne                                                        | The id of the product.                                                               |
| CreatedDate      | date                                                          | The date of the service request's creation.                                          |
| LastModifiedDate | date                                                          | The date that the service request was last modified.                                 |
| LastClosedDate   | date                                                          | The date that the service request was last closed.                                   |
| FileLinks        | array of [FileInfo](utility-resources.md#fileinfo) resources | The collection of File Links that pertain to the service request.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | A note can be added to an existing service request.                                  |
| Notes            | array of [ServiceRequestNotes](#servicerequestnote)           | A collection of notes added to the service request.                                  |
| CountryCode      | chaîne                                                        | The country corresponding to the service request.                                    |
| Attributs       | ResourceAttributes                                            | The metadata attributes corresponding to the service request.                        |

 

## <a name="span-idservicerequestcontactspan-idservicerequestcontactspan-idservicerequestcontactservicerequestcontact"></a><span id="ServiceRequestContact"/><span id="servicerequestcontact"/><span id="SERVICEREQUESTCONTACT"/>ServiceRequestContact


Describes a contact that creates or modifies a service request.

| Propriété     | Tapez                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organisation | [ServiceRequestOrganization](#servicerequestorganization) | Organization for which the service request is created. |
| ContactId    | chaîne                                                    | The contact's unique id.                               |
| LastName     | chaîne                                                    | The last name of the contact.                          |
| Prénom    | chaîne                                                    | The first name of the contact.                         |
| E-mail        | chaîne                                                    | The email of the contact.                              |
| PhoneNumber  | chaîne                                                    | The phone number of the contact.                       |

 

## <a name="span-idservicerequestnotespan-idservicerequestnotespan-idservicerequestnoteservicerequestnote"></a><span id="ServiceRequestNote"/><span id="servicerequestnote"/><span id="SERVICEREQUESTNOTE"/>ServiceRequestNote


Describes a note attached to a service request.

| Propriété      | Tapez   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | chaîne | The name of the creator of the note.         |
| CreatedDate   | date   | The date and time when the note was created. |
| Text          | chaîne | The text of the note.                        |

 

## <a name="span-idservicerequestorganizationspan-idservicerequestorganizationspan-idservicerequestorganizationservicerequestorganization"></a><span id="ServiceRequestOrganization"/><span id="servicerequestorganization"/><span id="SERVICEREQUESTORGANIZATION"/>ServiceRequestOrganization


Describes the organization for which the service request is created.

| Propriété    | Tapez   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | chaîne | The unique id of the organization.    |
| Nom        | chaîne | The name of the organization.         |
| PhoneNumber | chaîne | The phone number of the organization. |

 

## <a name="span-idsupporttopicspan-idsupporttopicspan-idsupporttopicsupporttopic"></a><span id="SupportTopic"/><span id="supporttopic"/><span id="SUPPORTTOPIC"/>SupportTopic


Describes a support topic. Service requests specify a support topic to ensure that they are processed quickly and effectively.

| Propriété    | Tapez               | Description                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Nom        | chaîne             | The name of the support topic.                                |
| Description | chaîne             | The description of the support topic.                         |
| Id          | chaîne             | The unique id of the support topic.                           |
| Attributs  | ResourceAttributes | The metadata attributes corresponding to the service request. |

 

 

 




