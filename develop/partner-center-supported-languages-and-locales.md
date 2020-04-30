---
title: Langues et paramètres régionaux pris en charge dans l’Espace partenaires
description: Liste des paramètres régionaux pris en charge par ISO2 et ISO3 pour l’espace partenaires.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 70b9b6a4954b133c619cb72ff40bc5e99fb307cd
ms.sourcegitcommit: 42b4d44796df44c18460145acb5a63566d9153c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82089359"
---
# <a name="partner-center-supported-languages-and-locales"></a>Langues et paramètres régionaux pris en charge dans l’Espace partenaires

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Certaines API de l’espace partenaires requièrent une valeur indiquant les paramètres régionaux, le pays ou la région. Par exemple, l' [en-tête X de l’en-tête REST de l’espace partenaires](headers.md) requiert une valeur souvent au format « langue-pays » (« en-US » indique « anglais-États-Unis »).

Dans les API gérées par l’espace partenaires, la classe [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) et les propriétés [OfferCategory. locale](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest. CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode)ou [CustomerBillingProfile. culture](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) requièrent des valeurs de chaîne qui indiquent une langue ou un pays/région (sous la forme d’un code de langue ISO2 ou d’un code de pays/région ISO3), des paramètres régionaux ou une culture (un ID de langue associé à un pays

Le tableau suivant répertorie les cultures et les codes de pays ISO (International Standards Organization) qui sont pris en charge dans les API de l’espace partenaires.

| Pays/région                           | Code du pays ISO alpha 2 | Code du pays ISO alpha 3 | Culture (s) prise en charge                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afghanistan                              | AF                       | AFG                      | PS-AF/fr-fr                         |
| Åland (îles d’)                            | AX                       | Unis                      | SV-SE/en-US                         |
| Albanie                                  | AL                       | ALB                      | Sq-AL/fr-fr                         |
| Algérie                                  | DZ                       | DZA                      | ar-DZ/fr-fr                         |
| Samoa américaines                           | AS                       | ASM                      | fr-FR                                 |
| Andorre                                  | AD                       | AND                      | ca-ES/en-US                         |
| Angola                                   | AO                       | EU                      | PT-PT/en-US                         |
| Anguilla                                 | AI                       | AIA                      | fr-FR                                 |
| Antarctique                               | AQ                       | ATA                      | fr-FR                                 |
| Antigua-et-Barbuda                      | Groupe de disponibilité                       | ATG                      | fr-FR                                 |
| Argentine                                | AR                       | DONNÉE                      | es-AR/fr-fr                         |
| Arménie                                  | AM                       | ARM                      | HY-AM/en-US                         |
| Aruba                                    | AW                       | ABW                      | NL-NL/en-US                         |
| Australie                                | AU                       | AUS                      | en-dessous/en-US                         |
| Autriche                                  | AT                       | CONFORMITÉ                      | de-AT/fr-fr                         |
| Azerbaïdjan                               | AZ                       | AZE                      | az-Latn-AZ/fr-US                    |
| Les Bahamas                                  | BS                       | BHS                      | en-GB/fr-fr                         |
| Bahreïn                                  | BH                       | BHR                      | AR-BH/fr-fr                         |
| Bangladesh                               | BD                       | BGD                      | -BD/fr-fr                         |
| Barbade                                 | BB                       | BRB                      | en-GB/fr-fr                         |
| Bélarus                                  | BY                       | BLR                      | être par/en-US                         |
| Belgique                                  | BE                       | BEL                      | fr-a/NL-is/fr-US                 |
| Belize                                   | BZ                       | BLZ                      | en-via/fr-fr                         |
| Bénin                                    | BJ                       | BEN                      | fr-FR/fr-fr                         |
| Bermudes                                  | BM                       | BMU                      | en-GB/fr-fr                         |
| Bhoutan                                   | BT                       | BTN                      | fr-FR                                 |
| Bolivie                                  | BO                       | BOL                      | es-BO/fr-fr                         |
| Bonaire                                  | BQ                       | BES                      | NL-NL/en-US                         |
| Bosnie-Herzégovine                   | BA                       | RELATIF                      | bs-Latn-BA/fr-US                    |
| Botswana                                 | BW                       | BWA                      | en-GB/fr-fr                         |
| Bouvet (Île)                            | BV                       | BVT                      | NB-non/en-US                         |
| Brésil                                   | BR                       | BRA                      | PT-BR/fr-fr                         |
| Territoires britanniques de l’océan Indien           | IO                       | IOT                      | fr-FR                                 |
| Îles Vierges britanniques                   | VG                       | VGB                      | fr-FR                                 |
| Brunéi Darussalam                                   | BN                       | BRN                      | MS-m/en-US                         |
| Bulgarie                                 | BG                       | BVR                      | BG-BG/fr-fr                         |
| Burkina Faso                             | BF                       | BFA                      | fr-FR/fr-fr                         |
| Burundi                                  | BI                       | BDI                      | fr-FR/fr-fr                         |
| Cabo Verde                               | CV                       | CPV                      | PT-CV/fr-fr                         |
| Cambodge                                 | KH                       | KHM                      | km-KH/en-US                         |
| Cameroun                                 | CM                       | ENVOYÉS                      | fr-FR/fr-fr                         |
| Canada                                   | CA                       | CAN                      | fr-CA/fr-fr                         |
| Caïmans (îles)                           | KY                       | CYM                      | en-GB/fr-fr                         |
| République centrafricaine                 | CF                       | CAF                      | fr-FR/fr-fr                         |
| Tchad                                     | TD                       | TCD                      | fr-FR/fr-fr                         |
| Chili                                    | CL                       | CHL                      | es-CL/fr-fr                         |
| Chine                                    | CN                       | CHN                      | zh-CN/fr-fr                         |
| Christmas (île)                         | CX                       | CXR                      | fr-FR                                 |
| Cocos-Keeling (îles)                  | CC                       | CCK                      | fr-FR                                 |
| Colombie                                 | CO                       | COL                      | es-CO/en-US                         |
| Comores (Les)                                  | KM                       | COM                      | fr-FR/fr-fr                         |
| Congo                                    | CG                       | ROUE dentée                      | fr-FR/fr-fr                         |
| Congo (RDC)                              | CD                       | COD                      | fr-FR/fr-fr                         |
| Cook (îles)                             | CK                       | COK                      | fr-FR                                 |
| Costa Rica                               | CR                       | CRI, éléments                      | es-CR/fr-fr                         |
| Côte d’Ivoire                            | CI                       | CIV                      | fr-FR/fr-fr                         |
| Croatie                                  | HR                       | HRV                      | HR-HR/fr-fr                         |
| Curaçao                                  | CW                       | CUW                      | NL-NL/en-US                         |
| Chypre                                   | CY                       | CYP                      | El-GR/fr-fr                         |
| Tchéquie                                  | CZ                       | CZE                      | CS-CZ/fr-fr                         |
| Danemark                                  | DK                       | DNK                      | da-DK/fr-fr                         |
| Djibouti                                 | DJ                       | DJI                      | fr-FR/fr-fr                         |
| Dominique                                 | DM                       | DMA                      | fr-FR                                 |
| République dominicaine                       | DO                       | DOM                      | es-DO/en-US                         |
| Équateur                                  | EC                       | ÉCU                      | es-EC/fr-fr                         |
| Égypte                                    | EG                       | EGY                      | AR-EG/fr-fr                         |
| El Salvador                              | SV                       | SLV                      | es-VP/en-US                         |
| Guinée équatoriale                        | GQ                       | GNQ                      | es-ES/en-US                         |
| Érythrée                                  | ER                       | ERI                      | ar-SA/en-US                         |
| Estonie                                  | EE                       | ESTIMÉ                      | et-EE/fr-fr                         |
| eSwatini                                 | SZ                       | SWZ                      | fr-FR                                 |
| Éthiopie                                 | ET                       | Ed                      | AM-ET/en-US                         |
| Malouines (îles)                         | FK                       | FLK                      | fr-FR                                 |
| Féroé (îles)                            | FO                       | PROVENANT                      | FO-FO/fr-fr                         |
| Fidji                                     | FJ                       | FJI                      | en-GB/fr-fr                         |
| Finlande                                  | FI                       | FIN                      | fi-fi/sv-FI/FR-US                 |
| France                                   | FR                       | FRA                      | fr-FR/fr-fr                         |
| Guyane française                            | GF                       | GUF                      | fr-FR/fr-fr                         |
| Polynésie française                         | PF                       | PYF                      | fr-FR/fr-fr                         |
| Terres australes françaises              | TF                       | ATF                      | fr-FR/fr-fr                         |
| Gabon                                    | GA                       | GAB                      | fr-FR/fr-fr                         |
| Gambie                                   | GM                       | GMB                      | fr-FR                                 |
| Géorgie                                  | GE                       | LOCAL                      | Ka-GE/en-US                         |
| Allemagne                                  | DE                       | DEU                      | de-fr/fr-fr                         |
| Ghana                                    | GH                       | GHA                      | en-GB/fr-fr                         |
| Gibraltar                                | GI                       | Gio                      | fr-FR                                 |
| Grèce                                   | GR                       | GRC                      | El-GR/fr-fr                         |
| Groenland                                | GL                       | GRL                      | da-DK/fr-fr                         |
| Grenade                                  | GD                       | GRD                      | fr-FR                                 |
| Guadeloupe                               | GP                       | AUX                      | fr-FR/fr-fr                         |
| Guam                                     | GU                       | GENCIVE                      | fr-FR                                 |
| Guatemala                                | GT                       | GTM                      | es-GT/en-US                         |
| Guernesey                                 | GG                       | GGY                      | fr-FR                                 |
| Guinée                                   | GN                       | GIN                      | fr-FR/fr-fr                         |
| Guinée-Bissau                            | GW                       | GNB                      | PT-PT/en-US                         |
| Guyane                                   | GY                       | EXPERT                      | fr-FR                                 |
| Haïti                                    | HT                       | HTI                      | fr-FR/fr-fr                         |
| Heard et McDonald (Îles)        | HM                       | HMD                      | fr-FR                                 |
| Honduras                                 | HN                       | HND                      | es-HN/en-US                         |
| Hong Kong (R.A.S.)                            | HK                       | HKG                      | zh-HK/fr-fr                         |
| Hongrie                                  | HU                       | HUN                      | HU-HU/fr-fr                         |
| Islande                                  | IS                       | SANDWICH                      | IS-IS/fr-fr                         |
| Inde                                    | IN                       | IND                      | en-IN/HI-IN/fr-fr                 |
| Indonésie                                | id                       | IDN                      | ID-ID/fr-fr                         |
| Irak                                     | IQ                       | IRQ                      | AR-IQ/fr-fr                         |
| Irlande                                  | IE                       | IRL                      | en-IE/en-US                         |
| Île de Man                              | IM                       | IMN                      | fr-FR                                 |
| Israël                                   | IL                       | ISR                      | He-IL/en-US                         |
| Italie                                    | IT                       | ITA                      | informatique-informatique/fr-fr                         |
| Jamaïque                                  | JM                       | BOURRAGE                      | en-JM/fr-fr                         |
| Jan Mayen                                | XJ                       | XJA                      | NB-non/en-US                         |
| Japon                                    | JP                       | JPN                      | ja-JP/fr-fr                         |
| Jersey                                   | JE                       | JEY                      | fr-FR                                 |
| Jordanie                                   | JO                       | JOR                      | AR-JO/en-US                         |
| Kazakhstan                               | KZ                       | KAZ                      | KK-KZ/en-US                         |
| Kenya                                    | KE                       | KEN                      | SW-KE/fr-US                         |
| Kiribati                                 | KI                       | KIR                      | fr-FR                                 |
| Corée du Sud                                    | KR                       | KOR                      | ko-KR/en-US                         |
| Kosovo                                   | XK                       | XKS                      | fr-FR                                 |
| Koweït                                   | KW                       | KWT                      | AR-KW/fr-fr                         |
| Kirghizistan                               | KG                       | KGZ                      | KY-KG/en-US                         |
| Laos                                     | LA                       | SYMBOLE                      | Lo-LA/en-US                         |
| Lettonie                                   | LV                       | LVA                      | LV-LV/en-US                         |
| Liban                                  | LB                       | LBN                      | ar-LB/en-US                         |
| Lesotho                                  | LS                       | LSO                      | fr-FR                                 |
| Liberia                                  | LR                       | LBR                      | fr-FR                                 |
| Libye                                    | LY                       | LBY                      | AR-EP/fr-fr                         |
| Liechtenstein                            | LI                       | INCOMB                      | de-LI/fr-fr                         |
| Lituanie                                | LT                       | LTU                      | lt-LT/fr-fr                         |
| Luxembourg                               | LU                       | LUX                      | de-LU/FR-LU/fr-fr                 |
| Macao R.A.S.                                | MO                       | MAC                      | zh-MO/fr-fr                         |
| Macédoine, macédonien                          | MK                       | MKD                      | MK-MK/fr-fr                         |
| Madagascar                               | MG                       | MDG                      | fr-FR/fr-fr                         |
| Malawi                                   | MW                       | MWI                      | fr-FR                                 |
| Malaisie                                 | MY                       | MYS                      | en-MY/fr-US                         |
| Maldives                                 | MV                       | MDV                      | DV-MV/en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR/fr-fr                         |
| Malte                                    | MT                       | MLT                      | MT-MT/fr-US                         |
| Marshall (îles)                         | MH                       | MHL                      | fr-FR                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR/fr-fr                         |
| Mauritanie                               | MR                       | MRT                      | ar-SA/en-US                         |
| Maurice (île)                                | MU                       | MUS                      | en-GB/fr-fr                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR/fr-fr                         |
| Mexique                                   | MX                       | MEX                      | es-MX/fr-fr                         |
| Micronésie                               | FM                       | FSM                      | fr-FR                                 |
| Moldova                                  | MD                       | MDA                      | RO-RO/fr-fr                         |
| Monaco                                   | MC                       | MCO                      | fr-MC/fr-fr                         |
| Mongolie                                 | MN                       | MNG                      | mn-MN/fr-fr                         |
| Monténégro                               | ME                       | MNE                      | SR-LATN-ME/fr-fr                    |
| Montserrat                               | MS                       | MSR                      | fr-FR                                 |
| Maroc                                  | MA                       | MAR                      | AR-MA/en-US                         |
| Mozambique                               | MZ                       | MOZ                      | PT-PT/en-US                         |
| Myanmar                                  | MM                       | MMR                      | fr-FR                                 |
| Namibie                                  | N/D                       | NAM                      | en-GB/fr-fr                         |
| Nauru                                    | NR                       | NRU                      | fr-FR                                 |
| Népal                                    | NP                       | NPL                      | Nou-NP/fr-fr                         |
| Antilles néerlandaises                     | AN                       | IN                      | fr-FR                                 |
| Pays-Bas                         | NL                       | NLD                      | NL-NL/en-US                         |
| Nouvelle-Calédonie                            | NC                       | NCL                      | fr-FR/fr-fr                         |
| Nouvelle-Zélande                              | NZ                       | NZL                      | en-NZ/en-US                         |
| Nicaragua                                | NI                       | Carte d’interface réseau                      | es-NI/en-US                         |
| Niger                                    | NE                       | NER                      | fr-FR/fr-fr                         |
| Nigeria                                  | NG                       | NGA                      | ha-LATN-NG/fr-fr                    |
| Niue                                     | NU                       | NIU                      | fr-FR                                 |
| Norfolk (île)                           | NF                       | NFK                      | fr-FR                                 |
| Îles Marianne du Nord                 | MP                       | MNP                      | fr-FR                                 |
| Norvège                                   | Non                       | NOR                      | NB-non/en-US                         |
| Oman                                     | OM                       | OMN                      | AR-OM/en-US                         |
| Pakistan                                 | PK                       | RESOURCEPAK                      | Your-PK/fr-fr                         |
| Palau                                    | PW                       | PLW                      | fr-FR                                 |
| Autorité palestinienne                    | PS                       | PSE                      | ar-SA/en-US                         |
| Panama                                   | PA                       | PAN                      | es-PA/en-US                         |
| Papouasie-Nouvelle-Guinée                         | PG                       | PNG                      | fr-FR                                 |
| Paraguay                                 | PY                       | ARRACH                      | es-PY/fr-fr                         |
| Pérou                                     | PE                       | POUR                      | es-PE/en-US                         |
| Philippines                              | PH                       | PHL                      | en-PH/fr-fr                         |
| Pitcairn (îles)                         | PN                       | PCN                      | fr-FR                                 |
| Pologne                                   | PL                       | POL                      | PL-PL/fr-fr                         |
| Portugal                                 | PT                       | PRT                      | PT-PT/en-US                         |
| Porto Rico                              | PR                       | PRI                      | es-PR/fr-fr                         |
| Qatar                                    | QA                       | QAT                      | AR-QA/fr-fr                         |
| La Réunion                                  | RE                       | REU                      | fr-FR/fr-fr                         |
| Roumanie                                  | RO                       | ROU                      | RO-RO/fr-fr                         |
| Russie                                   | RU                       | RUS                      | ru-RU/en-US                         |
| Rwanda                                   | L/E                       | Accès web à distance                      | RW-RW/en-US                         |
| Saba                                     | XS                       | XSA                      | NL-NL/en-US                         |
| Saint-Christophe-et-Niévès                    | KN                       | KNA                      | en-GB/fr-fr                         |
| Sainte-Lucie                              | LC                       | LCA                      | fr-FR                                 |
| Saint-Martin (partie française)                             | MF                       | MAF                      | fr-FR/fr-fr                         |
| Saint-Pierre-et-Miquelon                | PM                       | SPM                      | fr-FR/fr-fr                         |
| Saint-Vincent-et-les-Grenadines         | VC                       | VCT                      | fr-FR                                 |
| Saint--Barthélemy                         | BL                       | BLM                      | fr-FR/fr-fr                         |
| Samoa                                    | WS                       | WSM                      | fr-FR                                 |
| Saint-Marin                               | SM                       | SMR                      | informatique-informatique/fr-fr                         |
| São Tomé et Príncipe                    | ST                       | Protocole                      | PT-PT/en-US                         |
| Arabie Saoudite                             | SA                       | SAU                      | ar-SA/en-US                         |
| Sénégal                                  | SN                       | Send                      | WO-SN/en-US                         |
| Serbie                                   | RS                       | SRB                      | SR-LATN-RS/SR-Cyrl-RS/fr-US       |
| Seychelles                               | SC                       | SYC                      | fr-FR                                 |
| Sierra Leone                             | SL                       | UNIQUE                      | fr-FR                                 |
| Singapour                                | SG                       | SGP                      | fr-SG/zh-SG/fr-fr                 |
| Saint-Eustache                           | XE                       | XSE                      | NL-NL/en-US                         |
| Saint-Martin (partie néerlandaise)                             | SX                       | SXM                      | fr-FR                                 |
| Slovaquie                                 | SK                       | SVK                      | SK-SK/fr-fr                         |
| Slovénie                                 | SI                       | SVN                      | SL-SI/en-US                         |
| Salomon (îles)                          | SB                       | SLB                      | fr-FR                                 |
| Somalie                                  | SO                       | SOM                      | ar-SA/en-US                         |
| Afrique du Sud                             | ZA                       | ZAF                      | en-ZA/fr-fr                         |
| Géorgie du Sud et les îles Sandwich du Sud | GS                       | SGS                      | fr-FR                                 |
| Soudan du Sud                              | SS                       | SSD                      | fr-FR                                 |
| Espagne                                    | ES                       | ESP                      | es-ES/ca-ES/UE-ES/GL-ES/fr-fr |
| Sri Lanka                                | LK                       | LKA                      | Si-LK/fr-fr                         |
| Sainte-Hélène, Ascension et Tristan da Cunha   | SH                       | SHN                      | fr-FR                                 |
| Surinam                                 | SR                       | Couch                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | NB-non/en-US                         |
| Suède                                   | SE                       | $ $                      | SV-SE/en-US                         |
| Suisse                              | CH                       | CHE                      | de-CH/fr-CH/IT-CH/fr-fr         |
| Taïwan                                   | TW                       | TWN                      | zh-TW/fr-fr                         |
| Tadjikistan                               | TJ                       | TJK                      | TG-Cyrl-TJ/fr-US                    |
| Tanzanie                                 | TZ                       | TZA                      | en-GB/fr-fr                         |
| Thaïlande                                 | MJ                       | THA                      | th-TH/en-US                         |
| Timor-Leste                              | TL                       | TLS                      | PT-PT/en-US                         |
| Togo                                     | TG                       | TGO                      | fr-FR/fr-fr                         |
| Tokelau                                  | TK                       | TKL                      | fr-FR                                 |
| Tonga                                    | TO                       | MILLIERS                      | fr-FR                                 |
| Trinité-et-Tobago                      | TT                       | TTO                      | en-TT/en-US                         |
| Tunisie                                  | TN                       | Exécutez                      | AR-TN/fr-fr                         |
| Turquie                                   | TR                       | Ready                      | TR-TR/en-US                         |
| Turkménistan                             | TM                       | TKM                      | TK-TM/fr-fr                         |
| Turques-et-Caïques (îles)                 | TC                       | ÉLÉMENTAIRE                      | fr-FR                                 |
| Tuvalu                                   | TV                       | TUV                      | fr-FR                                 |
| Ouganda                                   | UG                       | UGA                      | en-GB/fr-fr                         |
| Ukraine                                  | UA                       | UKR                      | Royaume-Uni-UA/fr-US                         |
| Émirats Arabes Unis                     | AE                       | ARE                      | AR-AE/fr-fr                         |
| Royaume-Uni                           | Go                       | GBR                      | en-GB/fr-fr                         |
| États-Unis Îles mineures éloignées                    | UM                       | UMI                      | fr-FR                                 |
| Îles Vierges (É.-U.)                      | VI                       | VIR                      | fr-FR                                 |
| États-Unis                            | US                       | États-Unis                      | fr-fr/es-US                         |
| Uruguay                                  | UY                       | URY                      | es-UY/fr-fr                         |
| Ouzbékistan                               | UZ                       | UZB                      | uz-LATN-UZ/fr-US                    |
| Vanuatu                                  | VU                       | VUT                      | fr-FR                                 |
| État de la Cité du Vatican                             | VA                       | T.V.A.                      | informatique-informatique/fr-fr                         |
| Venezuela                                | VE                       | ENSEMBLE                      | es-VE/fr-fr                         |
| Vietnam                                  | VN                       | VNM                      | vi-VN/en-US                         |
| Wallis-et-Futuna                        | WF                       | WLF                      | fr-FR/fr-fr                         |
| Yémen                                    | YE                       | YEM                      | AR-Yé/en-US                         |
| Zambie                                   | ZM                       | ZMB                      | en-GB/fr-fr                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW/fr-fr                         |

