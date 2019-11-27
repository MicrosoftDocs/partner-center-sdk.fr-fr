---
title: Obtenir un lien de téléchargement pour le modèle de contrat client Microsoft
description: Obtenir un lien de téléchargement pour le modèle de contrat de client Microsoft.
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
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Obtenir un lien de téléchargement pour le modèle de contrat client Microsoft

S’applique à :

- Espace partenaires

La ressource **AgreementDocument** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas à :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment obtenir un lien pour télécharger le modèle de contrat client Microsoft, en fonction du pays et de la langue du client.

## <a name="prerequisites"></a>Conditions préalables

- Si vous utilisez le kit de développement logiciel (SDK) .NET de l’espace partenaires, la version 1,14 ou une version ultérieure est requise.
- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](./partner-center-authentication.md). Ce scénario ne prend en charge que l’authentification d’application + utilisateur.
- Pays du client auquel le modèle de contrat de client Microsoft s’applique.
- Langue dans laquelle le modèle de contrat de licence utilisateur Microsoft doit être localisé.

> [!IMPORTANT]
> - Le contrat client Microsoft est spécifique au pays. Lorsque vous demandez un lien pour télécharger le modèle de contrat client Microsoft, veillez à spécifier le pays approprié en fonction de l’emplacement du client. ou la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).
> - Dans certains pays, le contrat client Microsoft est disponible dans plusieurs langues. Pour une expérience utilisateur optimale, choisissez la langue qui correspond le mieux aux besoins du client. Pour obtenir la liste des langues prises en charge, consultez la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).
> - Cette méthode est uniquement prise en charge par le contrat client Microsoft. Vous ne pouvez pas l’utiliser pour obtenir un lien de téléchargement pour Microsoft Cloud modèle d’accord.

## <a name="net"></a>.NET

Pour récupérer un lien permettant de télécharger le modèle de contrat client Microsoft :

1. Récupérez les métadonnées de l’accord pour le contrat client Microsoft. Vous devez obtenir l' **TemplateID** du contrat du client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Utilisez la collection collection iaggregatepartner. AgreementTemplates.
3. Appelez la méthode **méthode BYID** et spécifiez l' **TemplateID** du contrat du client Microsoft.
4. Extraire la propriété de **document** .
5. Appelez la méthode **ByCountry** et spécifiez le pays du client auquel le modèle de contrat s’applique. La requête est définie par défaut sur *US* si la méthode n’est pas spécifiée. Pour obtenir la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages). Cette méthode est **sensible à la casse**.
6. Appelez la méthode **ByLanguage** et spécifiez la langue dans laquelle le modèle d’accord doit être localisé. La requête par défaut est en *-US* si la méthode n’est pas spécifiée ou si l’indicatif du pays spécifié n’est pas pris en charge pour le pays spécifié. Pour obtenir la liste des codes de langue pris en charge, consultez la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages) .
7. Appelez la **méthode** **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string customerCountry = "US";

string languageForLocalization = "en-US";

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry(customerCountry).ByLanguage(languageForLocalization).Get();
```

Un exemple complet est disponible dans la classe [GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .


## <a name="rest-request"></a>Demande REST

Pour récupérer un lien permettant de télécharger le modèle de contrat client Microsoft :

1. Récupérez les métadonnées de l’accord pour le contrat client Microsoft. Vous devez obtenir l' **TemplateID** du contrat du client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](get-customer-agreement-metadata.md).
2. Créez une demande REST pour extraire une [ressource **AgreementDocument** ](./agreement-document-resources.md). Pour obtenir un exemple, consultez l’exemple de [syntaxe de requête](#request-syntax) . Vous devez spécifier les informations suivantes :
    - L' **TemplateID** du contrat du client Microsoft.
    - Pays auquel le modèle de contrat de client Microsoft s’applique.
    - Langue dans laquelle le modèle de contrat de licence utilisateur Microsoft doit être localisé.

### <a name="request-syntax"></a>Syntaxe de la requête

Utilisez la syntaxe de requête suivante pour cette ressource :

| Méthode | URI de requête |
|--------|---------------------------------------------------------------------|
| GET | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreementtemplates/{Agreement-template-ID}/document ? Language = {language} & pays = {Country} http/1.1 |

### <a name="uri-parameters"></a>Paramètres d’URI

Vous pouvez utiliser les paramètres URI suivants avec votre demande :

| Nom                   | Type   | Obligatoire | Description                                 |
|------------------------|--------|----------|---------------------------------------------|
| ID de modèle d’accord  | chaîne | Oui      | Identificateur unique du type de contrat. Vous pouvez obtenir l’templateId pour le contrat de client Microsoft en extrayant les métadonnées de l’accord pour le contrat de client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](./get-customer-agreement-metadata.md). Ce paramètre respecte la **casse**.|
| country                | chaîne | Non       | Indique le pays auquel le modèle de contrat s’applique. La requête est définie par défaut sur *US* si le paramètre n’est pas spécifié. Pour obtenir la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).|
| language               | chaîne | Non       | Indique la langue dans laquelle le modèle d’accord doit être localisé. La requête prend par défaut la valeur en *-US* si le paramètre n’est pas spécifié ou si l’indicatif du pays spécifié in’t est pris en charge pour le pays spécifié. Pour obtenir la liste des pays pris en charge, reportez-vous à la [liste des pays et des langues pris en charge](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md).

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

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une [ressource **AgreementDocument** ](./agreement-document-resources.md) dans le corps de la réponse.

La ressource a une propriété **downloadUri** , qui contient une chaîne d’URL qui peut être utilisée pour télécharger le modèle de contrat. Un lien différent est retourné chaque fois que vous effectuez une requête. Ce lien expire au bout de cinq minutes.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires.

Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

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

| Country                   | Code du pays   | Code (s) de langue pris en charge |
|------------------------|--------|----------|
| Åland (îles d’) | PASSANT | fr-FR |
| Afghanistan | AF | fr-FR |
| Albanie | AL | fr-FR |
| Algérie | DZ | en-US, fr-FR, en-US |
| Samoa américaines | AS | fr-FR |
| Andorre | AD | fr-FR |
| Angola | AO | en-US, PT-PT |
| Anguilla | IA | fr-FR |
| Antarctique | INACTIF | fr-FR |
| Antigua-et-Barbuda | GA | fr-FR |
| Argentine | AR | en-US, es-ES |
| Arménie | AM | fr-FR |
| Aruba | AW | fr-FR |
| Australie | AU | fr-FR |
| Autriche | AT | fr-fr, de-DE |
| Azerbaïdjan | AZ | fr-FR |
| Bahamas | BS | fr-FR |
| Bahreïn | BH | fr-fr, ar-SA |
| Bangladesh | BD | fr-FR |
| Barbade (La) | BB | fr-FR |
| Bélarus | BY | en-US, ru-RU |
| Belgique | BE | fr-fr, NL-NL |
| Belize | Via | en-US, es-ES |
| Bénin | BJ | fr-FR |
| Bermudes | NOMENCLATURE | fr-FR |
| Bhoutan | CC | fr-FR |
| Bolivie | BO | en-US, es-ES |
| Bonaire | BQ | fr-FR |
| Bosnie-Herzégovine | BA | fr-FR |
| Botswana | BW | fr-FR |
| Bouvet (Île) | BV | fr-FR |
| Brésil | BR | fr-fr, PT-BR |
| Territoires britanniques de l’océan Indien | E/S | fr-FR |
| Îles Vierges britanniques | VG | fr-FR |
| Brunéi Darussalam | BN | fr-FR |
| Bulgarie | BG | fr-fr, BG-BG |
| Burkina-Faso | BF | fr-FR |
| Burundi | DÉCISIONNEL | fr-FR |
| Côte d’Ivoire | CI | en-US, fr-FR |
| Cap Vert | CV | en-US, PT-PT |
| Cambodge | KH | fr-FR |
| Cameroun | CM | en-US, fr-FR |
| Canada | AC | en-US, fr-FR |
| Caïmans (îles) | KY | fr-fr, en-US |
| République centrafricaine | CF | fr-FR |
| Tchad | ÉQUIPEMENTS | fr-FR |
| Chili | CL | en-US, es-ES |
| Christmas (île) | CX | fr-FR |
| Cocos-Keeling (îles) | CC | fr-FR |
| Colombie | CO | en-US, es-ES |
| Comores (Les) | KILOMÈTRES | fr-FR |
| Congo (RDC) | CD-ROM | fr-FR |
| Congo | CG | fr-FR |
| Cook (îles) | HT | fr-FR |
| Costa Rica | CR | en-US, es-ES |
| Croatie | HR | fr-fr, RH-RH |
| Curaçao | APPROXIMATIF | fr-FR |
| Chypre | CY | fr-FR |
| Czechia | CZ | en-US, CS-CZ |
| Danemark | DK | fr-fr, da-DK |
| Djibouti | EFFECTUÉ | fr-FR |
| Dominique | EXPLORATION | fr-FR |
| République dominicaine | DO | en-US, es-ES |
| Équateur (République de) | EC | fr-FR |
| Égypte | EG | fr-fr, ar-SA |
| Salvador | SV | en-US, es-ES |
| Guinée équatoriale | GQ | fr-FR |
| Érythrée | ERRE | fr-FR |
| Estonie | EE | fr-fr, et-EE |
| eSwatini | SZ | fr-FR |
| Éthiopie | Mendes | fr-FR |
| Malouines (îles) | FK | fr-FR |
| Féroé (îles) | FO | fr-FR |
| Fidji | FJ | fr-FR |
| Finlande | FI | en-US, FI-FI |
| France | FR | en-US, fr-FR |
| Guyane française | GF | en-US, fr-FR  |
| Polynésie française | UTIL | fr-FR |
| Terres australes françaises | TF | fr-FR |
| Gabon | GA | fr-FR |
| Gambie | GÉNÉTIQUE | fr-FR |
| Géorgie | GE | fr-FR |
| Allemagne | DE | fr-fr, de-DE |
| Ghana | GH | fr-FR |
| Gibraltar | GI | fr-FR |
| Grèce | GR | fr-fr, El-GR |
| Groenland | GÉNÉRALE | fr-FR |
| Grenade | GD | fr-FR |
| Guadeloupe | MARGE | fr-FR |
| Guam | GU | fr-FR |
| Guatemala | GT | en-US, es-ES |
| Guernesey | GG | fr-FR |
| Guinée | GN | fr-FR |
| Guinée-Bissau | ENTREPÔT | fr-FR |
| Guyana | GY | fr-FR |
| Haïti | HT | fr-FR |
| Heard et McDonald (Îles) | Britannique | fr-FR |
| Honduras | HN | en-US, es-ES |
| Hong Kong R.A.S. | HK | fr-fr, zh-HK |
| Hongrie | HU | en-US, HU-HU |
| Islande | IS | fr-FR |
| Inde | IN | en-US, hi-IN |
| Indonésie | ID | en-US, ID-ID |
| Irak | IQ | fr-fr, ar-SA |
| Irlande | Internet Explorer | fr-FR |
| Île de Man | Messagerie instantanée | fr-FR |
| Israël | IL | en-US, HE-il |
| Italie | Informatique | en-US, informatique |
| Jamaïque | JM | fr-FR |
| Jan Mayen | XJ | fr-FR |
| Japon | JP | en-US, ja-JP |
| Jersey | JE | fr-FR |
| Jordanie | JO | fr-fr, ar-SA |
| Kazakhstan | KZ | en-US, KK-KZ |
| Kenya | KE | fr-FR |
| Kiribati | KI | fr-FR |
| Corée | KR | en-US, ko-KR |
| Kosovo | XK | fr-FR |
| Koweït | KW | fr-fr, ar-SA |
| Kirghizistan | KG | en-US, ru-RU |
| Laos | LA | fr-FR |
| Lettonie | LV | en-US, LV-LV |
| Liban | LB | fr-fr, ar-SA |
| Lesotho | LS | fr-FR |
| Liberia | GD | fr-FR |
| Libye | EMPLOYÉS | fr-fr, ar-SA |
| Liechtenstein | LI | fr-fr, de-DE |
| Lituanie | LT | fr-fr, LT-LT |
| Luxembourg | LU | en-US, fr-FR |
| Macao R.A.S. | MOLYBDÈN | fr-fr, zh-HK |
| Macédoine, Ex.-Rép. yougoslave de | MK | fr-FR |
| Madagascar | ML | fr-FR |
| Malawi | MW | fr-FR |
| Malaisie | MY | en-US, MS-MY |
| Maldives | MV | fr-FR |
| Mali | ENVIRON | fr-FR |
| Malte | MT | fr-FR |
| Marshall (îles) | MH | fr-FR |
| Martinique | MQ | fr-FR |
| Mauritanie | MR | fr-FR |
| Maurice | MU | fr-fr, ar-SA |
| Mayotte | YT | fr-FR |
| Mexique | MX | en-US, es-ES |
| Micronésie | Radio | fr-FR |
| République de Moldavie | MD | en-US, RO-RO |
| Monaco | MC | en-US, fr-FR |
| Mongolie | PORTABLE | fr-FR |
| Monténégro | ME | fr-FR |
| Montserrat | MS | fr-FR |
| Maroc | MA | en-US, fr-FR, en-US |
| Mozambique | MZ | fr-FR |
| Myanmar | MM | fr-FR |
| Namibie | N/A | fr-FR |
| Nauru | NR | fr-FR |
| Népal | NP | fr-FR |
| Pays-Bas | NL | fr-fr, NL-NL |
| Nouvelle-Calédonie | OBTEN | fr-FR |
| Nouvelle-Zélande | NZ | fr-FR |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | fr-FR |
| Nigeria | NG | fr-FR |
| Niue | NU | fr-FR |
| Norfolk (île) | NF | fr-FR |
| Mariannes du Nord (îles) | MP | fr-FR |
| Norvège | NON | fr-fr, NB-non |
| Oman | OM | fr-fr, ar-SA |
| Pakistan | PK | fr-FR |
| Palau | CONFIGURER passe | fr-FR |
| Autorité palestinienne | PS | fr-FR |
| Panama | AF | en-US, es-ES |
| Papouasie-Nouvelle-Guinée | SOUHAITABLE | fr-FR |
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
| Rwanda | GRAVE | en-US, fr-FR |
| São Tomé et Príncipe | ST | en-US, fr-FR |
| Saba | XS | fr-FR |
| Saint--Barthélemy | BL | fr-FR |
| Saint Kitts et Nevis | KN | fr-FR |
| Sainte-Lucie | EUROS | fr-fr, en-US |
| Saint-Martin | INSTANTANÉ | fr-fr, en-US |
| Saint-Pierre-et-Miquelon | Manuel | fr-FR |
| Saint-Vincent-et-les-Grenadines | VIRTUEL | fr-FR |
| Samoa | Web | fr-FR |
| Saint-Marin | MS | fr-FR |
| Arabie saoudite | SA | fr-FR |
| Sénégal | SN | en-US, fr-FR |
| Serbie | RS | en-US, SR-LATN-RS, en-US |
| Seychelles | SC | fr-FR |
| Sierra Leone | SL | fr-FR |
| Singapour | SG | fr-fr, zh-SG |
| Saint-Eustache | XE | fr-FR |
| Saint-Martin (Royaume des Pays-Bas) | SX | fr-fr, en-US |
| Slovaquie | SK | fr-fr, SK-SK |
| Slovénie | SI | fr-fr, SL-SI |
| Salomon (îles) | ASPIRATEUR | fr-FR |
| Somalie | AFIN | fr-FR |
| Afrique du Sud | ZA | fr-FR |
| Géorgie du Sud et Sandwich du Sud (îles) | GS | fr-FR |
| Soudan du Sud | SÉCURITÉ | fr-FR |
| Espagne | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | fr-FR |
| Sainte-Hélène, ascension, Tristan da Cunha | & | fr-FR |
| Surinam | SR | fr-FR |
| Svalbard | SJ | fr-FR |
| Suède | SE | en-US, SV-SE |
| Suisse | CH | en-US, fr-FR, en-US, en-US |
| Taïwan | TW | fr-fr, zh-HK |
| Tadjikistan | TJ | fr-FR |
| Tanzanie | TZ | fr-FR |
| Thaïlande | TH | en-US, th-TH |
| Timor-Leste | TL | fr-FR |
| Togo | OCDE | fr-FR |
| Tokelau | J | fr-FR |
| Tonga | À | fr-FR |
| Trinité-et-Tobago | TT | fr-FR |
| Tunisie | TN | en-US, fr-FR, en-US |
| Turquie | TR | fr-fr, TR-TR |
| Turkménistan | TM | fr-FR |
| Turks et Caïcos (îles) | CT | fr-FR |
| Tuvalu | TV | fr-FR |
| Îles mineures éloignées des États-Unis | UNIFIÉ | fr-FR |
| Îles Vierges (É.-U.) | VL | fr-FR |
| Ouganda | UG | fr-FR |
| Ukraine | UA | en-US, Royaume-Uni-UA |
| Émirats arabes unis | AE | fr-fr, ar-SA |
| Royaume-Uni | Go | fr-FR |
| États-Unis | US | fr-FR |
| Uruguay | UY | en-US, es-ES |
| Ouzbékistan | UZ | en-US, ru-RU |
| Vanuatu | VOU | fr-FR |
| État de la Cité du Vatican | VA | fr-FR |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis-et-Futuna | WF | fr-FR |
| Yémen | POUSSE | fr-fr, ar-SA |
| Zambie | ZM | fr-FR |
| Zimbabwe | ZW | fr-FR |


