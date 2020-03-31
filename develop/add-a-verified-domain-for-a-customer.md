---
title: Ajouter un domaine vérifié pour un client
description: Ajoutez un domaine vérifié à la liste des domaines approuvés pour un client dans l’espace partenaires.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 89ff3dd9ad8d752f559f23a886d632f60b846eac
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412603"
---
# <a name="add-a-verified-domain-for-a-customer"></a>Ajouter un domaine vérifié pour un client

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment ajouter un domaine vérifié à la liste des domaines approuvés pour un client existant.

## <a name="prerequisites"></a>Composants requis

- Vous devez être un partenaire qui est un bureau d’enregistrement de domaines.
- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Un ID de client (**CustomerTenantId**). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant **compte**, puis en enregistrant son ID Microsoft.

## <a name="adding-a-verified-domain"></a>Ajout d’un domaine vérifié

Si vous êtes un partenaire qui est un bureau d’enregistrement de domaines, vous pouvez utiliser l’API verifieddomain pour poster une nouvelle ressource de [domaine](#domain) dans la liste des domaines d’un client existant. Pour ce faire, identifiez le client à l’aide de son CustomerTenantId, spécifiez une valeur pour la propriété VerifiedDomainName et transmettez une ressource de [domaine](#domain) dans la demande avec les propriétés Name, Capacity, AuthenticationType, Status et VerificationMethod requises incluses. Pour spécifier que le nouveau [domaine](#domain) est un domaine fédéré, définissez la propriété AuthenticationType dans la ressource de [domaine](#domain) sur « Federated », puis incluez une ressource [DomainFederationSettings](#domain-federation-settings) dans la demande. Si la méthode réussit, la réponse inclut une ressource de [domaine](#domain) pour le nouveau domaine vérifié.

### <a name="custom-verified-domains"></a>Domaines vérifiés personnalisés

Lorsque vous ajoutez un domaine vérifié personnalisé, un domaine qui n’est pas inscrit sur **onmicrosoft.com**, vous devez définir la propriété [CustomerUser. immutableId](user-resources.md#customeruser) sur une valeur d’ID unique pour le client pour lequel vous ajoutez le domaine. Cet identificateur unique est requis pendant le processus de validation lors de la vérification du domaine. Pour plus d’informations sur les comptes d’utilisateur client, voir [créer des comptes d’utilisateur pour un client](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{CustomerTenantId}/verifieddomain http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client pour lequel vous ajoutez un domaine vérifié.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | La valeur est un GUID mis en forme **CustomerTenantId** qui vous permet de spécifier un client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom                                                  | Type   | Obligatoire                                      | Description                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | chaîne | Oui                                           | Nom de domaine vérifié. |
| [Domain](#domain)                                     | objet | Oui                                           | Contient les informations de domaine. |
| [DomainFederationSettings](#domain-federation-settings) | objet | Oui (si AuthenticationType = "Federated")     | Paramètres de Fédération de domaine à utiliser si le domaine est un domaine « fédéré » et non un domaine « géré ». |

#### <a name="domain"></a>domaine.

Ce tableau décrit les propriétés de **domaine** obligatoires et facultatives dans le corps de la demande.

| Nom               | Type                                     | Obligatoire | Description                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | chaîne           | Oui      | Définit si le domaine est un domaine « géré » ou un domaine « fédéré ». Valeurs prises en charge : Managed, Federated.|
| Capability                                            | chaîne           | Oui      | Spécifie la fonctionnalité de domaine. Par exemple, « email ».                  |
| IsDefault                                             | valeur booléenne Nullable | Non       | Indique si le domaine est le domaine par défaut pour le locataire. Valeurs prises en charge : true, false, null.        |
| IsInitial                                             | valeur booléenne Nullable | Non       | Indique si le domaine est un domaine initial. Valeurs prises en charge : true, false, null.                       |
| Nom                                                  | chaîne           | Oui      | Nom du domaine.                                                          |
| RootDomain                                            | chaîne           | Non       | Nom du domaine racine.                                              |
| Statut                                                | chaîne           | Oui      | État du domaine. Par exemple, « vérifié ». Valeurs prises en charge : unverified, Verified, PendingDeletion.                               |
| VerificationMethod                                    | chaîne           | Oui      | Type de méthode de vérification du domaine. Valeurs prises en charge : None, DnsRecord, email.                                    |

##### <a name="domain-federation-settings"></a>Paramètres de Fédération de domaine

Ce tableau décrit les propriétés **DomainFederationSettings** obligatoires et facultatives dans le corps de la demande.

| Nom   | Type   | Obligatoire | Description                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | chaîne           | Non      | URI d’ouverture de session utilisé par les clients enrichis. Il s’agit de l’URL d’authentification STS du partenaire. |
| DefaultInteractiveAuthenticationMethod | chaîne           | Non      | Indique la méthode d’authentification par défaut qui doit être utilisée lorsqu’une application exige que l’utilisateur dispose d’une connexion interactive. |
| FederationBrandName                    | chaîne           | Non      | Nom de la désignation de la Fédération.        |
| IssuerUri                              | chaîne           | Oui     | Nom de l’émetteur des certificats.                        |
| LogOffUri                              | chaîne           | Oui     | URI de fermeture de session. Cela décrit l’URI de déconnexion du domaine fédéré.        |
| MetadataExchangeUri                    | chaîne           | Non      | URL qui spécifie le point de terminaison d’échange de métadonnées utilisé pour l’authentification à partir d’applications clientes riches. |
| NextSigningCertificate                 | chaîne           | Non      | Le certificat utilisé pour la prochaine version du service ADFS v2 pour signer les revendications. Il s’agit d’une représentation codée en base64 du certificat. |
| OpenIdConnectDiscoveryEndpoint         | chaîne           | Non      | Le point de terminaison de découverte OpenID Connect du STS IDP. |
| PassiveLogOnUri                        | chaîne           | Oui     | URI d’ouverture de session utilisé par les anciens clients passifs. Il s’agit de l’adresse pour envoyer des demandes de connexion fédérées. |
| PreferredAuthenticationProtocol        | chaîne           | Oui     | Format du jeton d’authentification. Par exemple, « WsFed ». Valeurs prises en charge : WsFed, texte samlp |
| PromptLoginBehavior                    | chaîne           | Oui     | Type de comportement de connexion prompt.  Par exemple, « TranslateToFreshPasswordAuth ». Valeurs prises en charge : TranslateToFreshPasswordAuth, NativeSupport, Disabled |
| SigningCertificate                     | chaîne           | Oui     | Certificat actuellement utilisé par le STS v2 pour signer des revendications. Il s’agit d’une représentation codée en base64 du certificat. |
| SigningCertificateUpdateStatus         | chaîne           | Non      | Indique l’état de mise à jour du certificat de signature. |
| SigningCertificateUpdateStatus         | valeur booléenne Nullable | Non      | Indique si le STS IDP prend en charge MFA. Valeurs prises en charge : true, false, null.|

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