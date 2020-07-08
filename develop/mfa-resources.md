---
title: Ressources des exigences de sécurité des partenaires
description: Comprenez les détails de l’adoption de l’authentification multifacteur (MFA) pour répondre aux exigences de sécurité des partenaires.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094760"
---
# <a name="partner-security-requirements-resources"></a>Ressources des exigences de sécurité des partenaires

**S’applique à :**

- Espace partenaires

Cet article vous aide à comprendre les détails de l’adoption de l’authentification multifacteur (MFA) pour aider votre organisation à respecter l’état des conditions de sécurité des partenaires. 

## <a name="portal-request-without-mfa"></a>Demande de portail sans MFA

Indiquer un utilisateur qui accède au portail de l’espace partenaires sans authentification MFA.

| Propriété                            | Type            | Description                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | string          | ID de l’objet utilisateur                        |
| TenantId                            | string          | ID de locataire CSP                         |
| Nomenclature                                 | string          | Nom d’utilisateur principal                   |
| LastNonMfaCompliantLoginDateTime    | DATETIME        | Heure de la dernière connexion de l’utilisateur sans authentification MFA |


## <a name="api-request-summarized-by-application"></a>Demande d’API résumée par l’application

Résumé de la demande d’API faite par les informations d’identification de l’application et de l’utilisateur, agrégées par date de demande et ID d’application.

| Propriété                            | Type            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | DATETIME        | Date de requête de l’API          |
| MfaCompliantRequestCount            | long            | Nombre de demandes avec MFA    |
| TotalRequestCount                   | long            | Nombre total de demandes       |
| ApplicationId                       | string          | Identificateur de l'application.        |
| ApplicationName                     | string          | Nom de l’application      |


## <a name="api-request-details"></a>Détails de la demande d’API

Demande d’API effectuée par les informations d’identification de l’utilisateur et de l’application. 

| Propriété                            | Type            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| RequestId                           | string          | MS-RequestId                             |
| CorrelationId                       | string          | MS-CorrelationId                         |
| NomOpération                       | string          | Le chemin d’accès de l’API avec la méthode de demande         |
| RequestDateTime                     | DateTime        | Heure de la demande d’API                     |
| IpAddress                           | string          | Adresse IP source                        |
| ObjectId                            | string          | ID de l’objet utilisateur                           |
| TenantId                            | string          | ID de locataire CSP                            |
| Nomenclature                                 | string          | Nom d’utilisateur principal                      |
| ApplicationId                       | string          | Votre application.                         |
| MfaCompliant                        | bool            | Indiquer la demande avec ou sans MFA |
