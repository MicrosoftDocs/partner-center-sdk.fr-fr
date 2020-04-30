---
title: Obtenir un lien de téléchargement pour le modèle de Contrat client Microsoft
description: Obtenir un lien de téléchargement pour le modèle de contrat de client Microsoft.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcc81acbab84e7f6ac9a495c00b2798c87075d89
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155579"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Obtenir un lien de téléchargement pour le modèle de Contrat client Microsoft

**S’applique à :**

- Espace partenaires

La ressource **AgreementDocument** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas à :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment obtenir un lien pour télécharger le modèle de contrat client Microsoft, en fonction du pays et de la langue du client.

## <a name="prerequisites"></a>Prérequis

- Si vous utilisez le SDK .NET de l’Espace partenaires, la version 1.14 ou une version ultérieure est nécessaire.

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](./partner-center-authentication.md). Ce scénario ne prend en charge que l’authentification de l’application et de l’utilisateur.

- Pays du client auquel le modèle de contrat de client Microsoft s’applique.

- Langue dans laquelle le modèle de contrat de licence utilisateur Microsoft doit être localisé.

> [!IMPORTANT]
>
> - Le contrat client Microsoft est spécifique au pays. Lorsque vous demandez un lien pour télécharger le modèle de contrat client Microsoft, veillez à spécifier le pays approprié en fonction de l’emplacement du client. ou la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).
>
> - Dans certains pays, le contrat client Microsoft est disponible dans plusieurs langues. Pour une expérience utilisateur optimale, choisissez la langue qui correspond le mieux aux besoins du client. Pour obtenir la liste des langues prises en charge, consultez la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).
> - Cette méthode est uniquement prise en charge par le contrat client Microsoft.

## <a name="net"></a>.NET

Pour récupérer un lien permettant de télécharger le modèle de contrat client Microsoft :

1. Récupérez les métadonnées du Contrat client Microsoft. Vous devez obtenir la valeur **templateId** du Contrat client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Utilisez la collection collection iaggregatepartner. AgreementTemplates.

3. Appelez la méthode **méthode BYID** et spécifiez l' **TemplateID** du contrat du client Microsoft.

4. Extraire la propriété de **document** .

5. Appelez la méthode **ByCountry** et spécifiez le pays du client auquel le modèle de contrat s’applique. La requête est définie par défaut sur *US* si la méthode n’est pas spécifiée. Pour obtenir la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages). Cette méthode est **sensible à la casse**.

6. Appelez la méthode **ByLanguage** et spécifiez la langue dans laquelle le modèle d’accord doit être localisé. La requête par défaut est en *-US* si la méthode n’est pas spécifiée ou si l’indicatif du pays spécifié n’est pas pris en charge pour le pays spécifié. Pour obtenir la liste des codes de langue pris en charge, consultez la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).

7. Appelez la **méthode** **GetAsync** .

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Un exemple complet est disponible dans la classe [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Demande REST

Pour récupérer un lien permettant de télécharger le modèle de contrat client Microsoft :

1. Récupérez les métadonnées du Contrat client Microsoft. Vous devez obtenir la valeur **templateId** du Contrat client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](get-customer-agreement-metadata.md).

2. Créez une demande REST pour extraire une [ressource **AgreementDocument** ](./agreement-document-resources.md). Pour obtenir un exemple, consultez l’exemple de [syntaxe de requête](#request-syntax) . Vous devez spécifier les informations suivantes :

    - L' **TemplateID** du contrat du client Microsoft.
    - Pays auquel le modèle de contrat de client Microsoft s’applique.
    - Langue dans laquelle le modèle de contrat de licence utilisateur Microsoft doit être localisé.

### <a name="request-syntax"></a>Syntaxe de la requête

Utilisez la syntaxe de requête suivante pour cette ressource :

| Méthode | URI de demande |
|--------|---------------------------------------------------------------------|
| GET | baseURL/v1/agreementtemplates/{Agreement-template-ID}/document ? Language = {Language} &pays = {Country} http/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>Paramètres URI

Vous pouvez utiliser les paramètres URI suivants avec votre demande :

| Nom                   | Type   | Obligatoire | Description                                 |
|------------------------|--------|----------|---------------------------------------------|
| ID de modèle d’accord  | string | Oui      | Identificateur unique du type de contrat. Vous pouvez obtenir la valeur de templateId du Contrat client Microsoft en récupérant les métadonnées du Contrat client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](./get-customer-agreement-metadata.md). Ce paramètre respecte la **casse**.|
| country                | string | Non       | Indique le pays auquel le modèle de contrat s’applique. La requête est définie par défaut sur *US* si le paramètre n’est pas spécifié. Pour obtenir la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).|
| langage               | string | Non       | Indique la langue dans laquelle le modèle d’accord doit être localisé. La requête prend par défaut la valeur en *-US* si le paramètre n’est pas spécifié ou si l’indicatif du pays spécifié in’t est pris en charge pour le pays spécifié. Pour obtenir la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne une [ressource **AgreementDocument** ](./agreement-document-resources.md) dans le corps de la réponse.

La ressource a une propriété **downloadUri** , qui contient une chaîne d’URL qui peut être utilisée pour télécharger le modèle de contrat. Un lien différent est retourné chaque fois que vous effectuez une requête. Ce lien expire au bout de cinq minutes.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires.

Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>Liste des pays et langues pris en charge

> [!IMPORTANT]
> La propriété de code Country respecte la casse. Veillez à utiliser la casse correcte spécifiée dans le tableau ci-dessous.

| Country                   | Code pays   | Code (s) de langue pris en charge |
|------------------------|--------|----------|
| Åland (îles d’) | AX | fr-FR |
| Afghanistan | AF | fr-FR |
| Albanie | AL | fr-FR |
| Algérie | DZ | en-US, fr-FR, en-US |
| Samoa américaines | AS | fr-FR |
| Andorre | AD | fr-FR |
| Angola | AO | en-US, PT-PT |
| Anguilla | AI | fr-FR |
| Antarctique | AQ | fr-FR |
| Antigua-et-Barbuda | Groupe de disponibilité | fr-FR |
| Argentine | AR | en-US, es-ES |
| Arménie | AM | fr-FR |
| Aruba | AW | fr-FR |
| Australie | AU | fr-FR |
| Autriche | AT | fr-fr, de-DE |
| Azerbaïdjan | AZ | fr-FR |
| Les Bahamas | BS | fr-FR |
| Bahreïn | BH | fr-fr, ar-SA |
| Bangladesh | BD | fr-FR |
| Barbade | BB | fr-FR |
| Bélarus | BY | en-US, ru-RU |
| Belgique | BE | fr-fr, NL-NL |
| Belize | BZ | en-US, es-ES |
| Bénin | BJ | fr-FR |
| Bermudes | BM | fr-FR |
| Bhoutan | BT | fr-FR |
| Bolivie | BO | en-US, es-ES |
| Bonaire | BQ | fr-FR |
| Bosnie-Herzégovine | BA | fr-FR |
| Botswana | BW | fr-FR |
| Bouvet (Île) | BV | fr-FR |
| Brésil | BR | fr-fr, PT-BR |
| Territoires britanniques de l’océan Indien | IO | fr-FR |
| Îles Vierges britanniques | VG | fr-FR |
| Brunéi Darussalam | BN | fr-FR |
| Bulgarie | BG | fr-fr, BG-BG |
| Burkina Faso | BF | fr-FR |
| Burundi | BI | fr-FR |
| Côte d’Ivoire | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, PT-PT |
| Cambodge | KH | fr-FR |
| Cameroun | CM | en-US, fr-FR |
| Canada | CA | en-US, fr-FR |
| Caïmans (îles) | KY | fr-fr, en-US |
| République centrafricaine | CF | fr-FR |
| Tchad | TD | fr-FR |
| Chili | CL | en-US, es-ES |
| Christmas (île) | CX | fr-FR |
| Cocos-Keeling (îles) | CC | fr-FR |
| Colombie | CO | en-US, es-ES |
| Comores (Les) | KM | fr-FR |
| Congo (RDC) | CD | fr-FR |
| Congo | CG | fr-FR |
| Cook (îles) | CK | fr-FR |
| Costa Rica | CR | en-US, es-ES |
| Croatie | HR | fr-fr, RH-RH |
| Curaçao | CW | fr-FR |
| Chypre | CY | fr-FR |
| Tchéquie | CZ | en-US, CS-CZ |
| Danemark | DK | fr-fr, da-DK |
| Djibouti | DJ | fr-FR |
| Dominique | DM | fr-FR |
| République dominicaine | DO | en-US, es-ES |
| Équateur | EC | fr-FR |
| Égypte | EG | fr-fr, ar-SA |
| El Salvador | SV | en-US, es-ES |
| Guinée équatoriale | GQ | fr-FR |
| Érythrée | ER | fr-FR |
| Estonie | EE | fr-fr, et-EE |
| eSwatini | SZ | fr-FR |
| Éthiopie | ET | fr-FR |
| Malouines (îles) | FK | fr-FR |
| Féroé (îles) | FO | fr-FR |
| Fidji | FJ | fr-FR |
| Finlande | FI | en-US, FI-FI |
| France | FR | en-US, fr-FR |
| Guyane française | GF | en-US, fr-FR  |
| Polynésie française | PF | fr-FR |
| Terres australes françaises | TF | fr-FR |
| Gabon | GA | fr-FR |
| Gambie | GM | fr-FR |
| Géorgie | GE | fr-FR |
| Allemagne | DE | fr-fr, de-DE |
| Ghana | GH | fr-FR |
| Gibraltar | GI | fr-FR |
| Grèce | GR | fr-fr, El-GR |
| Groenland | GL | fr-FR |
| Grenade | GD | fr-FR |
| Guadeloupe | GP | fr-FR |
| Guam | GU | fr-FR |
| Guatemala | GT | en-US, es-ES |
| Guernesey | GG | fr-FR |
| Guinée | GN | fr-FR |
| Guinée-Bissau | GW | fr-FR |
| Guyane | GY | fr-FR |
| Haïti | HT | fr-FR |
| Heard et McDonald (Îles) | HM | fr-FR |
| Honduras | HN | en-US, es-ES |
| Hong Kong (R.A.S.) | HK | fr-fr, zh-HK |
| Hongrie | HU | en-US, HU-HU |
| Islande | IS | fr-FR |
| Inde | IN | en-US, hi-IN |
| Indonésie | id | en-US, ID-ID |
| Irak | IQ | fr-fr, ar-SA |
| Irlande | IE | fr-FR |
| Île de Man | IM | fr-FR |
| Israël | IL | en-US, HE-il |
| Italie | IT | en-US, informatique |
| Jamaïque | JM | fr-FR |
| Jan Mayen | XJ | fr-FR |
| Japon | JP | en-US, ja-JP |
| Jersey | JE | fr-FR |
| Jordanie | JO | fr-fr, ar-SA |
| Kazakhstan | KZ | en-US, KK-KZ |
| Kenya | KE | fr-FR |
| Kiribati | KI | fr-FR |
| Corée du Sud | KR | en-US, ko-KR |
| Kosovo | XK | fr-FR |
| Koweït | KW | fr-fr, ar-SA |
| Kirghizistan | KG | en-US, ru-RU |
| Laos | LA | fr-FR |
| Lettonie | LV | en-US, LV-LV |
| Liban | LB | fr-fr, ar-SA |
| Lesotho | LS | fr-FR |
| Liberia | LR | fr-FR |
| Libye | LY | fr-fr, ar-SA |
| Liechtenstein | LI | fr-fr, de-DE |
| Lituanie | LT | fr-fr, LT-LT |
| Luxembourg | LU | en-US, fr-FR |
| Macao R.A.S. | MO | fr-fr, zh-HK |
| Macédoine, macédonien | MK | fr-FR |
| Madagascar | MG | fr-FR |
| Malawi | MW | fr-FR |
| Malaisie | MY | en-US, MS-MY |
| Maldives | MV | fr-FR |
| Mali | ML | fr-FR |
| Malte | MT | fr-FR |
| Marshall (îles) | MH | fr-FR |
| Martinique | MQ | fr-FR |
| Mauritanie | MR | fr-FR |
| Maurice (île) | MU | fr-fr, ar-SA |
| Mayotte | YT | fr-FR |
| Mexique | MX | en-US, es-ES |
| Micronésie | FM | fr-FR |
| Moldova | MD | en-US, RO-RO |
| Monaco | MC | en-US, fr-FR |
| Mongolie | MN | fr-FR |
| Monténégro | ME | fr-FR |
| Montserrat | MS | fr-FR |
| Maroc | MA | en-US, fr-FR, en-US |
| Mozambique | MZ | fr-FR |
| Myanmar | MM | fr-FR |
| Namibie | N/D | fr-FR |
| Nauru | NR | fr-FR |
| Népal | NP | fr-FR |
| Pays-Bas | NL | fr-fr, NL-NL |
| Nouvelle-Calédonie | NC | fr-FR |
| Nouvelle-Zélande | NZ | fr-FR |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | fr-FR |
| Nigeria | NG | fr-FR |
| Niue | NU | fr-FR |
| Norfolk (île) | NF | fr-FR |
| Îles Marianne du Nord | MP | fr-FR |
| Norvège | Non | fr-fr, NB-non |
| Oman | OM | fr-fr, ar-SA |
| Pakistan | PK | fr-FR |
| Palau | PW | fr-FR |
| Autorité palestinienne | PS | fr-FR |
| Panama | PA | en-US, es-ES |
| Papouasie-Nouvelle-Guinée | PG | fr-FR |
| Paraguay | PY | en-US, es-ES |
| Pérou | PE | en-US, es-ES |
| Philippines | PH | fr-FR |
| Pitcairn (îles) | PN | fr-FR |
| Pologne | PL | fr-fr, PL-PL |
| Portugal | PT | en-US, PT-PT |
| Porto Rico | PR | fr-fr, en-US |
| Qatar | QA | fr-fr, ar-SA |
| La Réunion | RE | fr-FR |
| Roumanie | RO | en-US, RO-RO |
| Russie | RU | en-US, ru-RU |
| Rwanda | L/E | en-US, fr-FR |
| São Tomé et Príncipe | ST | en-US, fr-FR |
| Saba | XS | fr-FR |
| Saint--Barthélemy | BL | fr-FR |
| Saint-Christophe-et-Niévès | KN | fr-FR |
| Sainte-Lucie | LC | fr-fr, en-US |
| Saint-Martin (partie française) | MF | fr-fr, en-US |
| Saint-Pierre-et-Miquelon | PM | fr-FR |
| Saint-Vincent-et-les-Grenadines | VC | fr-FR |
| Samoa | WS | fr-FR |
| Saint-Marin | SM | fr-FR |
| Arabie Saoudite | SA | fr-FR |
| Sénégal | SN | en-US, fr-FR |
| Serbie | RS | en-US, SR-LATN-RS, en-US |
| Seychelles | SC | fr-FR |
| Sierra Leone | SL | fr-FR |
| Singapour | SG | fr-fr, zh-SG |
| Saint-Eustache | XE | fr-FR |
| Saint-Martin (partie néerlandaise) | SX | fr-fr, en-US |
| Slovaquie | SK | fr-fr, SK-SK |
| Slovénie | SI | fr-fr, SL-SI |
| Salomon (îles) | SB | fr-FR |
| Somalie | SO | fr-FR |
| Afrique du Sud | ZA | fr-FR |
| Géorgie du Sud et les îles Sandwich du Sud | GS | fr-FR |
| Soudan du Sud | SS | fr-FR |
| Espagne | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | fr-FR |
| Sainte-Hélène, Ascension et Tristan da Cunha | SH | fr-FR |
| Surinam | SR | fr-FR |
| Svalbard | SJ | fr-FR |
| Suède | SE | en-US, SV-SE |
| Suisse | CH | en-US, fr-FR, en-US, en-US |
| Taïwan | TW | fr-fr, zh-HK |
| Tadjikistan | TJ | fr-FR |
| Tanzanie | TZ | fr-FR |
| Thaïlande | MJ | en-US, th-TH |
| Timor-Leste | TL | fr-FR |
| Togo | TG | fr-FR |
| Tokelau | TK | fr-FR |
| Tonga | TO | fr-FR |
| Trinité-et-Tobago | TT | fr-FR |
| Tunisie | TN | en-US, fr-FR, en-US |
| Turquie | TR | fr-fr, TR-TR |
| Turkménistan | TM | fr-FR |
| Turques-et-Caïques (îles) | TC | fr-FR |
| Tuvalu | TV | fr-FR |
| États-Unis Îles mineures éloignées | UM | fr-FR |
| Îles Vierges (É.-U.) | VI | fr-FR |
| Ouganda | UG | fr-FR |
| Ukraine | UA | en-US, Royaume-Uni-UA |
| Émirats Arabes Unis | AE | fr-fr, ar-SA |
| Royaume-Uni | Go | fr-FR |
| États-Unis | US | fr-FR |
| Uruguay | UY | en-US, es-ES |
| Ouzbékistan | UZ | en-US, ru-RU |
| Vanuatu | VU | fr-FR |
| État de la Cité du Vatican | VA | fr-FR |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis-et-Futuna | WF | fr-FR |
| Yémen | YE | fr-fr, ar-SA |
| Zambie | ZM | fr-FR |
| Zimbabwe | ZW | fr-FR |
