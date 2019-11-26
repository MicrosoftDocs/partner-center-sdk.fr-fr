---
title: Webhooks de l’espace partenaires
description: Les webhooks permettent aux partenaires de s’inscrire pour les événements de changement de ressource.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6bb15fc4879bb735264ab45c4a84f6581cbf094a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488239"
---
# <a name="partner-center-webhooks"></a>Webhooks de l’espace partenaires


**S’applique à**

- Espace partenaires   
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government   


Les API de webhook de l’espace partenaires permettent aux partenaires de s’inscrire aux événements de changement de ressource. Ces événements sont fournis sous la forme de publications HTTP à l’URL inscrite du partenaire. Pour recevoir un événement de l’espace partenaires, les partenaires hébergent un rappel où l’espace partenaires peut poster l’événement de changement de ressource. L’événement est signé numériquement afin que le partenaire puisse vérifier qu’il a été envoyé à partir de l’espace partenaires. 

Les partenaires peuvent sélectionner des événements de webhook, comme ci-dessous, qui sont pris en charge par l’espace partenaires.  

- **Événement de test (« test créé »)**

    Cet événement vous permet d’auto-intégrer et de tester votre inscription en demandant un événement de test, puis en effectuant le suivi de sa progression. Vous serez en mesure de voir les messages d’erreur reçus de Microsoft lors de la tentative de remise de l’événement. Cela s’applique uniquement aux événements « test créés » et les données datant de plus de 7 jours sont purgées.

- **Événement de mise à jour d’abonnement (« abonnement-mis à jour »)**

    Cet événement se déclenche lors d’une modification de l’abonnement. Ces événements seront générés lorsqu’il se produit un changement interne en plus des modifications apportées par le biais de l’API de l’Espace partenaires. 
    
    >[!NOTE]
    >Il y a un délai de 48 heures entre le moment où un abonnement est modifié et le moment où l’événement mis à jour de l’abonnement est déclenché. 

- **Événement de seuil dépassé (« usagerecords-thresholdExceeded »)**

    Cet événement se déclenche lorsque la quantité d’utilisation de Microsoft Azure d’un client dépasse son budget de dépenses d’utilisation (son seuil). Pour plus d’informations, consultez [définir un budget de dépenses Azure pour vos clients](https://docs.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers).

- **Événement créé par la référence (« référence créée »)**

    Cet événement est déclenché lorsque la référence est créée. 

- **Événement mis à jour de référence (« référence-mis à jour »)**

    Cet événement est déclenché lorsque la référence est mise à jour. 

- **Événement de facturation prête (« prêt pour la facturation »)**

    Cet événement est déclenché lorsque la nouvelle facture est prête.


Les événements de webhook ultérieurs seront ajoutés pour les ressources qui changent dans le système dont le partenaire n’est pas en mesure de contrôler, et d’autres mises à jour seront effectuées pour que ces événements soient aussi proches que possible en temps réel. Les commentaires des partenaires sur lesquels des événements ajoutent de la valeur à leur entreprise seront extrêmement utiles pour déterminer les nouveaux événements à ajouter. 

Pour obtenir la liste complète des événements webhook pris en charge par l’espace partenaires, consultez [événements de webhook de l’espace partenaires](partner-center-webhook-events.md).

## <a name="prerequisites"></a>Conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.   



## <a name="receiving-events-from-partner-center"></a>Réception d’événements de l’espace partenaires

Pour recevoir des événements de l’espace partenaires, vous devez exposer un point de terminaison accessible publiquement ; et étant donné que ce point de terminaison est exposé, vous devez vérifier que la communication provient de l’espace partenaires. Tous les événements de webhook que vous recevez sont signés numériquement avec un certificat qui est lié à la racine Microsoft. Un lien vers le certificat utilisé pour signer l’événement est également fourni. Cela permet de renouveler le certificat sans avoir à redéployer ou reconfigurer votre service. L’espace partenaires fera 10 tentatives pour remettre l’événement. Si l’événement n’est toujours pas remis après 10 tentatives, il est déplacé dans une file d’attente hors connexion et aucune autre tentative n’est effectuée au moment de la remise. 

L’exemple suivant montre un événement publié par l’espace partenaires.

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
} 
```

>[!NOTE] 
>L’en-tête d’autorisation a un schéma de « signature ». Il s’agit d’une signature encodée en base64 du contenu.

## <a name="how-to-authenticate-the-callback"></a>Comment authentifier le rappel


Pour authentifier l’événement de rappel reçu à partir de l’espace partenaires, procédez comme suit :

1.  Vérifiez que les en-têtes requis sont présents (autorisation, x-ms-Certificate-URL, x-ms-signature-algorithme).
2.  Téléchargez le certificat utilisé pour signer le contenu (x-ms-Certificate-URL).
3.  Vérifiez la chaîne de certificats.
4.  Vérifiez l' « organisation » du certificat.
5.  Lit le contenu avec encodage UTF8 dans une mémoire tampon.
6.  Créez un fournisseur de chiffrement RSA.
7.  Vérifiez que les données correspondent à ce qui a été signé avec l’algorithme de hachage spécifié (par exemple, SHA256).
8.  Si la vérification est réussie, traitez le message.

> [!NOTE]
> Par défaut, le jeton de signature est envoyé dans un en-tête d’autorisation. Si vous affectez à **SignatureTokenToMsSignatureHeader** la valeur true dans votre inscription, le jeton de signature est envoyé dans l’en-tête x-ms-signature à la place.

## <a name="event-model"></a>Modèle d’événement


Le tableau suivant décrit les propriétés d’un événement de l’espace partenaires.

**Propriétés**

| Nom                      | Description                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **Protégée**             | Nom de l’événement. Sous la forme {Resource}-{action}. Par exemple, « test créé ».  |
| **URI**           | URI de la ressource qui a été modifiée.                                                 |
| **ResourceName**          | Nom de la ressource qui a été modifiée.                                                |
| **AuditUrl**              | Facultatif. URI de l’enregistrement d’audit.                                                |
| **ResourceChangeUtcDate** | Date et heure, au format UTC, auxquelles la modification de ressource s’est produite.                  |


**Exemple**

L’exemple suivant illustre la structure d’un événement de l’espace partenaires.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


## <a name="webhook-apis"></a>API webhook   


**Authentification**   

Tous les appels aux API webhook sont authentifiés à l’aide du jeton de porteur dans l’en-tête Authorization. Vous devez obtenir un jeton d’accès pour accéder à https://api.partnercenter.microsoft.com. Il s’agit du même jeton que celui utilisé pour accéder au reste des API de l’espace partenaires.


 
### <a name="get-a-list-of-events"></a>Obtenir une liste d’événements

Retourne une liste des événements actuellement pris en charge par les API webhook.

**URL de ressource**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/events

**Exemple de requête**   

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

**Exemple de réponse**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US
 
[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```



### <a name="register-to-receive-events"></a>S’inscrire pour recevoir des événements      

Inscrit un locataire pour recevoir les événements spécifiés.

**URL de ressource**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**Exemple de requête**   

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219
 
{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

**Exemple de réponse**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2 

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```



### <a name="view-a-registration"></a>Afficher une inscription        

Retourne l’inscription de l’événement webhooks pour un locataire.

**URL de ressource**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**Exemple de requête**   

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

**Exemple de réponse**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```



### <a name="update-an-event-registration"></a>Mettre à jour une inscription d’événement      

Met à jour une inscription d’événement existante. 

**URL de ressource**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**Exemple de requête**   

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258
 
{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

**Exemple de réponse**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2 

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```


### <a name="send-a-test-event-to-validate-your-registration"></a>Envoyer un événement de test pour valider votre inscription   

Génère un événement de test pour valider l’inscription d’un webhook. Ce test est destiné à confirmer que vous pouvez recevoir des événements de l’espace partenaires. Les données de ces événements seront supprimées sept jours après la création de l’événement initial. Vous devez être inscrit pour l’événement « test créé », à l’aide de l’API d’inscription, avant d’envoyer un événement de validation. 

>[!NOTE]
>Il existe une limite de 2 requêtes par minute lors de la publication d’un événement de validation. 

**URL de ressource**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents

**Exemple de requête**   

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

**Exemple de réponse**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```



### <a name="verify-that-the-event-was-delivered"></a>Vérifier que l’événement a été remis   

Retourne l’état actuel de l’événement de validation. Cela peut être utile pour le dépannage des problèmes de remise des événements. La réponse contient un résultat pour chaque tentative effectuée pour remettre l’événement.

**URL de ressource**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}

**Exemple de requête**   

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

**Exemple de réponse**     

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```


## <a name="example-for-signature-validation"></a>Exemple de validation de signature


**Exemple de signature de contrôleur de rappel (ASP.NET)**     

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

     de **validation de signature**  
L’exemple suivant montre comment ajouter un attribut d’autorisation au contrôleur qui reçoit des rappels d’événements de webhook.

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.Diagnostics;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (authHeader == null || string.IsNullOrEmpty(authHeader.Parameter))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization Header missing"));
            }

            if (authHeader.Scheme != "Signature")
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization Scheme needs to be 'Signature'"));
            }

            if (string.IsNullOrEmpty(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing"));
            }

            if (string.IsNullOrEmpty(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing"));
            }
        }

        private static string GetHeaderValue(HttpRequestHeaders headers, string key)
        {
            headers.TryGetValues(key, out IEnumerable<string> headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            var base64Signture = request.Headers.Authorization?.Parameter;
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-');    // e.g. RSA-SHA1
            var isValid = false;

            // Validate the certificate
            if (VerifyCertificate(certificate))
            {
                if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
                {
                    byte[] signature = Convert.FromBase64String(base64Signture);

                    RSACryptoServiceProvider csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                    var encoding = new UTF8Encoding();
                    byte[] data = encoding.GetBytes(content);

                    string hashAlgorithm = alg[1].ToUpper();

                    isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
                }

                if (!isValid)
                {
                    // log that we were not able to validate the signature
                    Trace.WriteLine($"Failed to validate signature for webhook callback. base64Signature: {base64Signture}, certificateUrl: {certificateUrl}, signatureAlgorithm: {signatureAlgorithm}");

                    var logger = GetLoggerIfAvailable(request);
                    logger?.TrackTrace("Failed to validate Signature for webhook callback", new Dictionary<string, string> { { "base64Signature", base64Signture }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                    throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
                }
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static bool VerifyCertificate(X509Certificate2 certificate)
        {
            return certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
        }
    }
}
```
