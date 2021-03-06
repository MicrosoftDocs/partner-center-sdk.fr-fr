---
title: Ajouter un domaine vérifié pour un client
description: Ajoutez un domaine vérifié à la liste des domaines approuvés pour un client dans l’espace partenaires.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d1503506d520671834c6290cddd487fc471090c2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095424"
---
# <a name="add-a-verified-domain-for-a-customer"></a>Ajouter un domaine vérifié pour un client

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment ajouter un domaine vérifié à la liste des domaines approuvés pour un client existant.

## <a name="prerequisites"></a>Prérequis

- Vous devez être un partenaire qui est un bureau d’enregistrement de domaines.

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="adding-a-verified-domain"></a>Ajout d’un domaine vérifié

Si vous êtes un partenaire qui est un bureau d’enregistrement de domaines, vous pouvez utiliser l' `verifieddomain` API pour poster une nouvelle ressource de [domaine](#domain) dans la liste des domaines d’un client existant. Pour ce faire, identifiez le client à l’aide de son CustomerTenantId. Spécifiez une valeur pour la propriété VerifiedDomainName. Transmettez une ressource de [domaine](#domain) dans la demande avec les propriétés Name, Capability, AuthenticationType, Status et VerificationMethod requises incluses. Pour spécifier que le nouveau [domaine](#domain) est un domaine fédéré, définissez la propriété AuthenticationType dans la ressource de [domaine](#domain) sur `Federated` et incluez une ressource [DomainFederationSettings](#domain-federation-settings) dans la demande. Si la méthode réussit, la réponse inclut une ressource de [domaine](#domain) pour le nouveau domaine vérifié.

### <a name="custom-verified-domains"></a>Domaines vérifiés personnalisés

Lorsque vous ajoutez un domaine vérifié personnalisé, un domaine qui n’est pas inscrit sur **onmicrosoft.com**, vous devez définir la propriété [CustomerUser. immutableId](user-resources.md#customeruser) sur une valeur d’ID unique pour le client pour lequel vous ajoutez le domaine. Cet identificateur unique est requis pendant le processus de validation lors de la vérification du domaine. Pour plus d’informations sur les comptes d’utilisateur client, voir [créer des comptes d’utilisateur pour un client](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{CustomerTenantId}/verifieddomain http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client pour lequel vous ajoutez un domaine vérifié.

| Name                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | O        | La valeur est un GUID mis en forme **CustomerTenantId** qui vous permet de spécifier un client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Name                                                  | Type   | Obligatoire                                      | Description                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | Yes                                           | Nom de domaine vérifié. |
| [Domaine](#domain)                                     | object | Oui                                           | Contient les informations de domaine. |
| [DomainFederationSettings](#domain-federation-settings) | object | Oui (si AuthenticationType = `Federated` )     | Paramètres de Fédération de domaine à utiliser si le domaine est un domaine `Federated` et non un `Managed` domaine. |

### <a name="domain"></a>Domain

Ce tableau décrit les propriétés de **domaine** obligatoires et facultatives dans le corps de la demande.

| Name               | Type                                     | Obligatoire | Description                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | string           | Yes      | Définit si le domaine est un domaine `Managed` ou un `Federated` domaine. Valeurs prises en charge : `Managed` , `Federated` .|
| Fonctionnalité                                            | string           | Yes      | Spécifie la fonctionnalité de domaine. Par exemple, `Email`.                  |
| IsDefault                                             | valeur booléenne Nullable | No       | Indique si le domaine est le domaine par défaut pour le locataire. Valeurs prises en charge : `True` , `False` , `Null` .        |
| IsInitial                                             | valeur booléenne Nullable | No       | Indique si le domaine est un domaine initial. Valeurs prises en charge : `True` , `False` , `Null` .                       |
| Nom                                                  | string           | Yes      | Nom du domaine.                                                          |
| RootDomain                                            | string           | No       | Nom du domaine racine.                                              |
| Statut                                                | string           | Oui      | État du domaine. Par exemple, `Verified`. Valeurs prises en charge : `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | string           | Oui      | Type de méthode de vérification du domaine. Valeurs prises en charge : `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Paramètres de Fédération de domaine

Ce tableau décrit les propriétés **DomainFederationSettings** obligatoires et facultatives dans le corps de la demande.

| Nom   | Type   | Obligatoire | Description                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | string           | No      | URI d’ouverture de session utilisé par les clients enrichis. Cette propriété est l’URL d’authentification STS du partenaire. |
| DefaultInteractiveAuthenticationMethod | string           | No      | Indique la méthode d’authentification par défaut qui doit être utilisée lorsqu’une application exige que l’utilisateur dispose d’une connexion interactive. |
| FederationBrandName                    | string           | No      | Nom de la désignation de la Fédération.        |
| IssuerUri                              | string           | Oui     | Nom de l’émetteur des certificats.                        |
| LogOffUri                              | string           | Oui     | URI de fermeture de session. Cette propriété décrit l’URI de déconnexion du domaine fédéré.        |
| MetadataExchangeUri                    | string           | No      | URL qui spécifie le point de terminaison d’échange de métadonnées utilisé pour l’authentification à partir d’applications clientes riches. |
| NextSigningCertificate                 | string           | No      | Le certificat utilisé pour la prochaine version du service ADFS v2 pour signer les revendications. Cette propriété est une représentation encodée en base64 du certificat. |
| OpenIdConnectDiscoveryEndpoint         | string           | No      | Le point de terminaison de découverte OpenID Connect du STS IDP. |
| PassiveLogOnUri                        | string           | Oui     | URI d’ouverture de session utilisé par les anciens clients passifs. Cette propriété correspond à l’adresse d’envoi des demandes de connexion fédérées. |
| PreferredAuthenticationProtocol        | string           | Oui     | Format du jeton d’authentification. Par exemple, `WsFed`. Valeurs prises en charge : `WsFed` ,`Samlp` |
| PromptLoginBehavior                    | string           | Oui     | Type de comportement de connexion prompt.  Par exemple, `TranslateToFreshPasswordAuth`. Valeurs prises en charge : `TranslateToFreshPasswordAuth` , `NativeSupport` ,`Disabled` |
| SigningCertificate                     | string           | Oui     | Certificat actuellement utilisé par le STS v2 pour signer des revendications. Cette propriété est une représentation encodée en base64 du certificat. |
| SigningCertificateUpdateStatus         | string           | No      | Indique l’état de mise à jour du certificat de signature. |
| SigningCertificateUpdateStatus         | valeur booléenne Nullable | No      | Indique si le STS IDP prend en charge MFA. Valeurs prises en charge : `True` , `False` , `Null` .|

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette API retourne une ressource de [domaine](#domain) pour le nouveau domaine vérifié.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```
