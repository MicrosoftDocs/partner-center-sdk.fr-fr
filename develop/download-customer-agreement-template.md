---
title: Get a download link for the Microsoft Customer Agreement template
description: Get a download link for Microsoft Customer Agreement template.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 76b0b6ceb20504ad0f9903027ac61feca78c3970
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489959"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Get a download link for the Microsoft Customer Agreement template

S'applique à :

- Espace partenaires

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

This article describes how to get a link to download the Microsoft Customer Agreement template, based on the customer's country and language.

## <a name="prerequisites"></a>Conditions préalables

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario only supports App+User authentication.
- The customer's country to which the Microsoft Customer Agreement template applies.
- The language in which the Microsoft Customer Agreement template should be localized.

> [!IMPORTANT]
> - The Microsoft Customer Agreement is country-specific. When requesting for a link to download the Microsoft Customer Agreement template, Be sure to specify the correct country based on customer's location. or list of supported countries, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - For some countries, the Microsoft Customer Agreement is available in multiple languages. For best customer experience, pick the language that best match the customer's needs. For list of supported languages, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - This method is only supported with the Microsoft Customer Agreement. You cannot use it to get a download link for Microsoft Cloud Agreement template.

## <a name="net"></a>.NET

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Use the IAggregatePartner.AgreementTemplates collection.
3. Call the **ById** method and specify the **templateId** of the Microsoft Customer Agreement.
4. Fetch the **Document** property.
5. Call the **ByCountry** method and specify the customer's country to which the agreement template applies. The query defaults to *US* if the method isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages). This method is **case-sensitive**.
6. Call the **ByLanguage** method and specify the language which the agreement template should be localized in. The query defaults to *en-US* if the method isn't specified or the country code specified isn't supported for the country specified. For list of supported language codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages)
7. Call the **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

string customerCountry = "US";

string languageForLocalization = "en-US";

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry(customerCountry).ByLanguage(languageForLocalization).Get();
```

A complete sample can be found in the [GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## <a name="rest-request"></a>REST request

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).
2. Create a REST request to fetch an [**AgreementDocument** resource](./agreement-document-resources.md). For an example, see the [request syntax](#request-syntax) example. You must specify the following information:
    - The **templateId** of the Microsoft Customer Agreement.
    - The country to which the Microsoft Customer Agreement template applies.
    - The language in which the Microsoft Customer Agreement template should be localized.

### <a name="request-syntax"></a>Syntaxe de la requête

Use the following request syntax for this resource:

| Méthode | URI de requête |
|--------|---------------------------------------------------------------------|
| GET | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>Paramètres d’URI

You can use the following URI parameters with your request:

| Nom                   | Tapez   | Obligatoire | Description                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | chaîne | Oui      | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md). This parameter is **case-sensitive**.|
| country                | chaîne | non       | Indicates the country to which the agreement template applies. The query defaults to *US* if the parameter isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|
| language               | chaîne | non       | Indicates the language in which the agreement template should be localized. The query defaults to *en-US* if the parameter isn't specified or the country code specified in't supported for the country specified. For list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>En-têtes de requête

For more information, see [Partner Center REST headers](headers.md).

### <a name="request-body"></a>Corps de la requête

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST response

If successful, this method returns an [**AgreementDocument** resource](./agreement-document-resources.md) in the response body.

The resource has a **downloadUri** property, which contains a URL string that can be used to download the agreement template. A different link is returned each time you make a query. This link expires after five minutes.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information.

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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

## <a name="list-of-supported-countries-and-languages"></a>List of supported countries and languages

> [!IMPORTANT]
> The country code property is case-sensitive. Please sure to use the correct casing specified in the table below.

| Country                   | Code du pays   | Supported language code(s) |
|------------------------|--------|----------|
| Åland (îles d’) | AX | en-US |
| Afghanistan | AF | en-US |
| Albanie | AL | en-US |
| Algérie | DZ | en-US, fr-FR, en-US |
| Samoa américaines | AS | en-US |
| Andorre | AD | en-US |
| Angola | AO | en-US, pt-PT |
| Anguilla | IA | en-US |
| Antarctique | AQ | en-US |
| Antigua-et-Barbuda | AG | en-US |
| Argentine | AR | en-US, es-ES |
| Arménie | AM | en-US |
| Aruba | AW | en-US |
| Australie | AU | en-US |
| Autriche | AT | en-US, de-DE |
| Azerbaïdjan | AZ | en-US |
| Bahamas | BS | en-US |
| Bahreïn | BH | en-US, ar-SA |
| Bangladesh | BD | en-US |
| Barbade (La) | BB | en-US |
| Bélarus | BY | en-US, ru-RU |
| Belgique | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Bénin | BJ | en-US |
| Bermudes | BM | en-US |
| Bhoutan | BT | en-US |
| Bolivie | BO | en-US, es-ES |
| Bonaire | BQ | en-US |
| Bosnie-Herzégovine | BA | en-US |
| Botswana | BW | en-US |
| Bouvet (Île) | BV | en-US |
| Brésil | BR | en-US, pt-BR |
| Territoires britanniques de l’océan Indien | E/S | en-US |
| Îles Vierges britanniques | VG | en-US |
| Brunei | BN | en-US |
| Bulgarie | BG | en-US, bg-BG |
| Burkina-Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d’Ivoire | CI | en-US, fr-FR |
| Cap Vert | CV | en-US, pt-PT |
| Cambodge | KH | en-US |
| Cameroun | CM | en-US, fr-FR |
| Canada | AC | en-US, fr-FR |
| Caïmans (îles) | KY | en-US, en-US |
| République centrafricaine | CF | en-US |
| Tchad | TD | en-US |
| Chili | CL | en-US, es-ES |
| Christmas (île) | CX | en-US |
| Cocos-Keeling (îles) | CC | en-US |
| Colombie | CO | en-US, es-ES |
| Comores (Les) | KM | en-US |
| Congo (RDC) | CD-ROM | en-US |
| République démocratique du Congo | CG | en-US |
| Cook (îles) | CK | en-US |
| Costa Rica | CR | en-US, es-ES |
| Croatie | HR | en-US, hr-HR |
| Curaçao | CW | en-US |
| Chypre | CY | en-US |
| Czechia | CZ | en-US, cs-CZ |
| Danemark | DK | en-US, da-DK |
| Djibouti | DJ | en-US |
| Dominique | DM | en-US |
| République dominicaine | DO | en-US, es-ES |
| Équateur (République de l’) | EC | en-US |
| Égypte | EG | en-US, ar-SA |
| Salvador | SV | en-US, es-ES |
| Guinée équatoriale | GQ | en-US |
| Érythrée | ER | en-US |
| Estonie | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| Éthiopie | ET | en-US |
| Malouines (îles) | FK | en-US |
| Îles Féroé | FO | en-US |
| Fidji | FJ | en-US |
| Finlande | FI | en-US, fi-FI |
| France | FR | en-US, fr-FR |
| Guyane française | GF | en-US, fr-FR  |
| Polynésie française | PF | en-US |
| Terres australes françaises | TF | en-US |
| Gabon | GA | en-US |
| Gambie | GM | en-US |
| Géorgie | GE | en-US |
| Allemagne | DE | en-US, de-DE |
| Ghana | GH | en-US |
| Gibraltar | GI | en-US |
| Grèce | GR | en-US, el-GR |
| Groenland | GL | en-US |
| Grenade | GD | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | en-US, es-ES |
| Guernesey | GG | en-US |
| Guinée | GN | en-US |
| Guinée-Bissau | GW | en-US |
| Guyana | GY | en-US |
| Haïti | HT | en-US |
| Heard et McDonald (Îles) | HM | en-US |
| Honduras | HN | en-US, es-ES |
| Hong Kong R.A.S. | HK | en-US, zh-HK |
| Hongrie | HU | en-US, hu-HU |
| Islande | IS | en-US |
| Inde | IN | en-US, hi-IN |
| Indonésie | ID | en-US, id-ID |
| Irak | IQ | en-US, ar-SA |
| Irlande | Internet Explorer | en-US |
| Île de Man | Messagerie instantanée | en-US |
| Israël | IL | en-US, he-IL |
| Italie | Informatique | en-US, it-IT |
| Jamaïque | JM | en-US |
| Jan Mayen | XJ | en-US |
| Japon | JP | en-US, ja-JP |
| Jersey | JE | en-US |
| Jordanie | JO | en-US, ar-SA |
| Kazakhstan | KZ | en-US, kk-KZ |
| Kenya | KE | en-US |
| Kiribati | KI | en-US |
| Corée | KR | en-US, ko-KR |
| Kosovo | XK | en-US |
| Koweït | KW | en-US, ar-SA |
| Kirghizistan | KG | en-US, ru-RU |
| Laos | LA | en-US |
| Lettonie | LV | en-US, lv-LV |
| Liban | LB | en-US, ar-SA |
| Lesotho | LS | en-US |
| Liberia | LR | en-US |
| Libye | LY | en-US, ar-SA |
| Liechtenstein | LI | en-US, de-DE |
| Lituanie | LT | en-US, lt-LT |
| Luxembourg | LU | en-US, fr-FR |
| Macao R.A.S. | MO | en-US, zh-HK |
| Macédoine, Ex.-Rép. yougoslave de | MK | en-US |
| Madagascar | MG | en-US |
| Malawi | MW | en-US |
| Malaisie | MY | en-US, ms-MY |
| Maldives | MV | en-US |
| Mali | ML | en-US |
| Malte (République de) | MT | en-US |
| Marshall (îles) | MH | en-US |
| Martinique | MQ | en-US |
| Mauritanie | MR | en-US |
| Maurice | MU | en-US, ar-SA |
| Mayotte | YT | en-US |
| Mexique | MX | en-US, es-ES |
| Micronésie | FM | en-US |
| République de Moldavie | MD | en-US, ro-RO |
| Monaco | MC | en-US, fr-FR |
| Mongolie | MN | en-US |
| Monténégro | ME | en-US |
| Montserrat | MS | en-US |
| Maroc | MA | en-US, fr-FR, en-US |
| Mozambique | MZ | en-US |
| Myanmar | MM | en-US |
| Namibie | N/A | en-US |
| Nauru | NR | en-US |
| Népal | NP | en-US |
| Pays-Bas | NL | en-US, nl-NL |
| Nouvelle-Calédonie | NC | en-US |
| Nouvelle-Zélande | NZ | en-US |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | en-US |
| Nigéria | NG | en-US |
| Niue | NU | en-US |
| Norfolk (île) | NF | en-US |
| Mariannes du Nord (îles) | MP | en-US |
| Norvège | NON | en-US, nb-NO |
| Oman | OM | en-US, ar-SA |
| Pakistan | PK | en-US |
| Palau | PW | en-US |
| Autorité palestinienne | PS | en-US |
| Panama | AF | en-US, es-ES |
| Papouasie-Nouvelle-Guinée | PG | en-US |
| Paraguay | PY | en-US, es-ES |
| Pérou | PE | en-US, es-ES |
| Philippines | PH | en-US |
| Pitcairn (îles) | PN | en-US |
| Pologne | PL | en-US, pl-PL |
| Portugal | PT | en-US, pt-PT |
| Porto Rico | PR | en-US, en-US |
| Qatar | QA | en-US, ar-SA |
| La Réunion | RE | en-US |
| Roumanie | RO | en-US, ro-RO |
| Russie | RU | en-US, ru-RU |
| Rwanda | RW | en-US, fr-FR |
| São Tomé et Príncipe | ST | en-US, fr-FR |
| Saba | XS | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts et Nevis | KN | en-US |
| Sainte-Lucie | LC | en-US, en-US |
| Saint-Martin | MF | en-US, en-US |
| Saint-Pierre-et-Miquelon | PM | en-US |
| Saint-Vincent-et-les-Grenadines | VC | en-US |
| Samoa | WS | en-US |
| Saint-Marin | SM | en-US |
| Arabie saoudite | SA | en-US |
| Sénégal | SN | en-US, fr-FR |
| Serbie | RS | en-US, sr-Latn-RS, en-US |
| Seychelles | SC | en-US |
| Sierra Leone | SL | en-US |
| Singapour | SG | en-US, zh-SG |
| Sint Eustatius | XE | en-US |
| Saint-Martin (Royaume des Pays-Bas) | SX | en-US, en-US |
| Slovaquie | SK | en-US, sk-SK |
| Slovénie | SI | en-US, sl-SI |
| Salomon (îles) | SB | en-US |
| Somalie | SO | en-US |
| Afrique du Sud | ZA | en-US |
| South Georgia and South Sandwich Islands | GS | en-US |
| Soudan du Sud | SS | en-US |
| Espagne | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | en-US |
| St Helena, Ascension, Tristan da Cunha | SH | en-US |
| Surinam | SR | en-US |
| Svalbard | SJ | en-US |
| Suède | SE | en-US, sv-SE |
| Suisse | CH | en-US, fr-FR, en-US, en-US |
| Taïwan | TW | en-US, zh-HK |
| Tadjikistan | TJ | en-US |
| Tanzanie | TZ | en-US |
| Thaïlande | TH | en-US, th-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | TK | en-US |
| Tonga | TO | en-US |
| Trinité-et-Tobago | TT | en-US |
| Tunisie | TN | en-US, fr-FR, en-US |
| Turquie | TR | en-US, tr-TR |
| Turkménistan | TM | en-US |
| Turks et Caïcos (îles) | TC | en-US |
| Tuvalu | TV | en-US |
| Îles mineures éloignées des États-Unis | UM | en-US |
| Îles Vierges (É.-U.) | VI | en-US |
| Ouganda | UG | en-US |
| Ukraine | UA | en-US, uk-UA |
| Émirats arabes unis | AE | en-US, ar-SA |
| Royaume-Uni | Go | en-US |
| États-Unis | États-Unis | en-US |
| Uruguay | UY | en-US, es-ES |
| Ouzbékistan | UZ | en-US, ru-RU |
| Vanuatu | VU | en-US |
| Cité du Vatican | VA | en-US |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis-et-Futuna | WF | en-US |
| Yémen | YE | en-US, ar-SA |
| Zambie | ZM | en-US |
| Zimbabwe | ZW | en-US |


