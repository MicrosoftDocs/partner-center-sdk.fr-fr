---
title: Partner Center supported languages and locales
description: List of ISO2 and ISO3 supported locales for Partner Center.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6b066c4afb87656717327e57cef94ab84eb93309
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488289"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partner Center supported languages and locales


**Applies To**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Some Partner Center APIs require a value indicating a locale, country or region. For example, the [Partner Center REST header](headers.md) X-Locale requires a value often in the format "language-country" ("en-US" indicates "English - United States").

In the Partner Center managed APIs, the [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) class and the [OfferCategory.Locale](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode), or [CustomerBillingProfile.Culture](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) properties require string values that indicate a language or country/region (in the form of an ISO2 language code or ISO3 country/region code), a locale, or a culture (a language ID combined with a country/region code).

The following table lists the cultures and International Standards Organization (ISO) country codes that are supported in the Partner Center APIs. 


| Pays/région                           | ISO Alpha 2 Country Code | ISO Alpha 3 Country Code | Supported Culture(s)                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afghanistan                              | AF                       | AFG                      | ps-AF / en-US                         |
| Åland (îles d’)                            | AX                       | ALA                      | sv-SE / en-US                         |
| Albanie                                  | AL                       | ALB                      | sq-AL / en-US                         |
| Algérie                                  | DZ                       | DZA                      | ar-DZ / en-US                         |
| Samoa américaines                           | AS                       | ASM                      | en-US                                 |
| Andorre                                  | AD                       | ET                      | ca-ES / en-US                         |
| Angola                                   | AO                       | AGO                      | pt-PT / en-US                         |
| Anguilla                                 | IA                       | AIA                      | en-US                                 |
| Antarctique                               | AQ                       | ATA                      | en-US                                 |
| Antigua-et-Barbuda                      | AG                       | ATG                      | en-US                                 |
| Argentine                                | AR                       | ARG                      | es-AR / en-US                         |
| Arménie                                  | AM                       | ARM                      | hy-AM / en-US                         |
| Aruba                                    | AW                       | ABW                      | nl-NL / en-US                         |
| Australie                                | AU                       | AUS                      | en-AU / en-US                         |
| Autriche                                  | AT                       | AUT                      | de-AT / en-US                         |
| Azerbaïdjan                               | AZ                       | AZE                      | az-Latn-AZ / en-US                    |
| Bahamas                                  | BS                       | BHS                      | en-GB / en-US                         |
| Bahreïn                                  | BH                       | BHR                      | ar-BH / en-US                         |
| Bangladesh                               | BD                       | BGD                      | bn-BD / en-US                         |
| Barbade (La)                                 | BB                       | BRB                      | en-GB / en-US                         |
| Bélarus                                  | BY                       | BLR                      | be-BY / en-US                         |
| Belgique                                  | BE                       | BEL                      | fr-BE / nl-BE / en-US                 |
| Belize                                   | BZ                       | BLZ                      | en-BZ / en-US                         |
| Bénin                                    | BJ                       | BEN                      | fr-FR / en-US                         |
| Bermudes                                  | BM                       | BMU                      | en-GB / en-US                         |
| Bhoutan                                   | BT                       | BTN                      | en-US                                 |
| Bolivie                                  | BO                       | BOL                      | es-BO / en-US                         |
| Bonaire                                  | BQ                       | BES                      | nl-NL / en-US                         |
| Bosnie-Herzégovine                   | BA                       | BIH                      | bs-Latn-BA / en-US                    |
| Botswana                                 | BW                       | BWA                      | en-GB / en-US                         |
| Bouvet (Île)                            | BV                       | BVT                      | nb-NO / en-US                         |
| Brésil                                   | BR                       | BRA                      | pt-BR / en-US                         |
| Territoires britanniques de l’océan Indien           | E/S                       | IOT                      | en-US                                 |
| Îles Vierges britanniques                   | VG                       | VGB                      | en-US                                 |
| Brunei                                   | BN                       | BRN                      | ms-BN / en-US                         |
| Bulgarie                                 | BG                       | BGR                      | bg-BG / en-US                         |
| Burkina-Faso                             | BF                       | BFA                      | fr-FR / en-US                         |
| Burundi                                  | BI                       | BDI                      | fr-FR / en-US                         |
| Cap Vert                               | CV                       | CPV                      | pt-CV / en-US                         |
| Cambodge                                 | KH                       | KHM                      | km-KH / en-US                         |
| Cameroun                                 | CM                       | CMR                      | fr-FR / en-US                         |
| Canada                                   | AC                       | CAN                      | fr-CA / en-US                         |
| Caïmans (îles)                           | KY                       | CYM                      | en-GB / en-US                         |
| République centrafricaine                 | CF                       | CAF                      | fr-FR / en-US                         |
| Tchad                                     | TD                       | TCD                      | fr-FR / en-US                         |
| Chili                                    | CL                       | CHL                      | es-CL / en-US                         |
| Chine                                    | CN                       | CHN                      | zh-CN / en-US                         |
| Christmas (île)                         | CX                       | CXR                      | en-US                                 |
| Cocos-Keeling (îles)                  | CC                       | CCK                      | en-US                                 |
| Colombie                                 | CO                       | COL                      | es-CO / en-US                         |
| Comores (Les)                                  | KM                       | COM                      | fr-FR / en-US                         |
| République démocratique du Congo                                    | CG                       | COG                      | fr-FR / en-US                         |
| Congo (RDC)                              | CD-ROM                       | COD                      | fr-FR / en-US                         |
| Cook (îles)                             | CK                       | COK                      | en-US                                 |
| Costa Rica                               | CR                       | CRI                      | es-CR / en-US                         |
| Côte d’Ivoire                            | CI                       | CIV                      | fr-FR / en-US                         |
| Croatie                                  | HR                       | HRV                      | hr-HR / en-US                         |
| Curaçao                                  | CW                       | CUW                      | nl-NL / en-US                         |
| Chypre                                   | CY                       | CYP                      | el-GR / en-US                         |
| Czechia                                  | CZ                       | CZE                      | cs-CZ / en-US                         |
| Danemark                                  | DK                       | DNK                      | da-DK / en-US                         |
| Djibouti                                 | DJ                       | DJI                      | fr-FR / en-US                         |
| Dominique                                 | DM                       | DMA                      | en-US                                 |
| République dominicaine                       | DO                       | DOM                      | es-DO / en-US                         |
| Équateur (République de l’)                                  | EC                       | ECU                      | es-EC / en-US                         |
| Égypte                                    | EG                       | EGY                      | ar-EG / en-US                         |
| Salvador                              | SV                       | SLV                      | es-SV / en-US                         |
| Guinée équatoriale                        | GQ                       | GNQ                      | es-ES / en-US                         |
| Érythrée                                  | ER                       | ERI                      | ar-SA / en-US                         |
| Estonie                                  | EE                       | EST                      | et-EE / en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| Éthiopie                                 | ET                       | ETH                      | am-ET / en-US                         |
| Malouines (îles)                         | FK                       | FLK                      | en-US                                 |
| Îles Féroé                            | FO                       | FRO                      | fo-FO / en-US                         |
| Fidji                                     | FJ                       | FJI                      | en-GB / en-US                         |
| Finlande                                  | FI                       | FIN                      | fi-FI / sv-FI / en-US                 |
| France                                   | FR                       | FRA                      | fr-FR / en-US                         |
| Guyane française                            | GF                       | GUF                      | fr-FR / en-US                         |
| Polynésie française                         | PF                       | PYF                      | fr-FR / en-US                         |
| Terres australes françaises              | TF                       | ATF                      | fr-FR / en-US                         |
| Gabon                                    | GA                       | GAB                      | fr-FR / en-US                         |
| Gambie                                   | GM                       | GMB                      | en-US                                 |
| Géorgie                                  | GE                       | GEO                      | ka-GE / en-US                         |
| Allemagne                                  | DE                       | DEU                      | de-DE / en-US                         |
| Ghana                                    | GH                       | GHA                      | en-GB / en-US                         |
| Gibraltar                                | GI                       | GIB                      | en-US                                 |
| Grèce                                   | GR                       | GRC                      | el-GR / en-US                         |
| Groenland                                | GL                       | GRL                      | da-DK / en-US                         |
| Grenade                                  | GD                       | GRD                      | en-US                                 |
| Guadeloupe                               | GP                       | GLP                      | fr-FR / en-US                         |
| Guam                                     | GU                       | GUM                      | en-US                                 |
| Guatemala                                | GT                       | GTM                      | es-GT / en-US                         |
| Guernesey                                 | GG                       | GGY                      | en-US                                 |
| Guinée                                   | GN                       | GIN                      | fr-FR / en-US                         |
| Guinée-Bissau                            | GW                       | GNB                      | pt-PT / en-US                         |
| Guyana                                   | GY                       | GUY                      | en-US                                 |
| Haïti                                    | HT                       | HTI                      | fr-FR / en-US                         |
| Heard et McDonald (Îles)        | HM                       | HMD                      | en-US                                 |
| Honduras                                 | HN                       | HND                      | es-HN / en-US                         |
| Hong Kong R.A.S.                            | HK                       | HKG                      | zh-HK / en-US                         |
| Hongrie                                  | HU                       | HUN                      | hu-HU / en-US                         |
| Islande                                  | IS                       | ISL                      | is-IS / en-US                         |
| Inde                                    | IN                       | IND                      | en-IN / hi-IN / en-US                 |
| Indonésie                                | ID                       | IDN                      | id-ID / en-US                         |
| Irak                                     | IQ                       | IRQ                      | ar-IQ / en-US                         |
| Irlande                                  | Internet Explorer                       | IRL                      | en-IE / en-US                         |
| Île de Man                              | Messagerie instantanée                       | IMN                      | en-US                                 |
| Israël                                   | IL                       | ISR                      | he-IL / en-US                         |
| Italie                                    | Informatique                       | ITA                      | it-IT / en-US                         |
| Jamaïque                                  | JM                       | JAM                      | en-JM / en-US                         |
| Jan Mayen                                | XJ                       | XJA                      | nb-NO / en-US                         |
| Japon                                    | JP                       | JPN                      | ja-JP / en-US                         |
| Jersey                                   | JE                       | JEY                      | en-US                                 |
| Jordanie                                   | JO                       | JOR                      | ar-JO / en-US                         |
| Kazakhstan                               | KZ                       | KAZ                      | kk-KZ / en-US                         |
| Kenya                                    | KE                       | KEN                      | sw-KE / en-US                         |
| Kiribati                                 | KI                       | KIR                      | en-US                                 |
| Corée                                    | KR                       | KOR                      | ko-KR / en-US                         |
| Kosovo                                   | XK                       | XKS                      | en-US                                 |
| Koweït                                   | KW                       | KWT                      | ar-KW / en-US                         |
| Kirghizistan                               | KG                       | KGZ                      | ky-KG / en-US                         |
| Laos                                     | LA                       | LAO                      | lo-LA / en-US                         |
| Lettonie                                   | LV                       | LVA                      | lv-LV / en-US                         |
| Liban                                  | LB                       | LBN                      | ar-LB / en-US                         |
| Lesotho                                  | LS                       | LSO                      | en-US                                 |
| Liberia                                  | LR                       | LBR                      | en-US                                 |
| Libye                                    | LY                       | LBY                      | ar-LY / en-US                         |
| Liechtenstein                            | LI                       | LIE                      | de-LI / en-US                         |
| Lituanie                                | LT                       | LTU                      | lt-LT / en-US                         |
| Luxembourg                               | LU                       | LUX                      | de-LU / fr-LU / en-US                 |
| Macao R.A.S.                                | MO                       | MAC                      | zh-MO / en-US                         |
| Macédoine, Ex.-Rép. yougoslave de                          | MK                       | MKD                      | mk-MK / en-US                         |
| Madagascar                               | MG                       | MDG                      | fr-FR / en-US                         |
| Malawi                                   | MW                       | MWI                      | en-US                                 |
| Malaisie                                 | MY                       | MYS                      | en-MY / en-US                         |
| Maldives                                 | MV                       | MDV                      | dv-MV / en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR / en-US                         |
| Malte (République de)                                    | MT                       | MLT                      | mt-MT / en-US                         |
| Marshall (îles)                         | MH                       | MHL                      | en-US                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR / en-US                         |
| Mauritanie                               | MR                       | MRT                      | ar-SA / en-US                         |
| Maurice                                | MU                       | MUS                      | en-GB / en-US                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR / en-US                         |
| Mexique                                   | MX                       | MEX                      | es-MX / en-US                         |
| Micronésie                               | FM                       | FSM                      | en-US                                 |
| République de Moldavie                                  | MD                       | MDA                      | ro-RO / en-US                         |
| Monaco                                   | MC                       | MCO                      | fr-MC / en-US                         |
| Mongolie                                 | MN                       | MNG                      | mn-MN / en-US                         |
| Monténégro                               | ME                       | MNE                      | sr-Latn-ME / en-US                    |
| Montserrat                               | MS                       | MSR                      | en-US                                 |
| Maroc                                  | MA                       | MAR                      | ar-MA / en-US                         |
| Mozambique                               | MZ                       | MOZ                      | pt-PT / en-US                         |
| Myanmar                                  | MM                       | MMR                      | en-US                                 |
| Namibie                                  | N/A                       | NAM                      | en-GB / en-US                         |
| Nauru                                    | NR                       | NRU                      | en-US                                 |
| Népal                                    | NP                       | NPL                      | ne-NP / en-US                         |
| Antilles néerlandaises                     | AN                       | ANT                      | en-US                                 |
| Netherlands, The                         | NL                       | NLD                      | nl-NL / en-US                         |
| Nouvelle-Calédonie                            | NC                       | NCL                      | fr-FR / en-US                         |
| Nouvelle-Zélande                              | NZ                       | NZL                      | en-NZ / en-US                         |
| Nicaragua                                | NI                       | NIC                      | es-NI / en-US                         |
| Niger                                    | NE                       | NER                      | fr-FR / en-US                         |
| Nigéria                                  | NG                       | NGA                      | ha-Latn-NG / en-US                    |
| Niue                                     | NU                       | NIU                      | en-US                                 |
| Norfolk (île)                           | NF                       | NFK                      | en-US                                 |
| Mariannes du Nord (îles)                 | MP                       | MNP                      | en-US                                 |
| Norvège                                   | NON                       | NOR                      | nb-NO / en-US                         |
| Oman                                     | OM                       | OMN                      | ar-OM / en-US                         |
| Pakistan                                 | PK                       | PAK                      | ur-PK / en-US                         |
| Palau                                    | PW                       | PLW                      | en-US                                 |
| Autorité palestinienne                    | PS                       | PSE                      | ar-SA / en-US                         |
| Panama                                   | AF                       | PAN                      | es-PA / en-US                         |
| Papouasie-Nouvelle-Guinée                         | PG                       | PNG                      | en-US                                 |
| Paraguay                                 | PY                       | PRY                      | es-PY / en-US                         |
| Pérou                                     | PE                       | PER                      | es-PE / en-US                         |
| Philippines                              | PH                       | PHL                      | en-PH / en-US                         |
| Pitcairn (îles)                         | PN                       | PCN                      | en-US                                 |
| Pologne                                   | PL                       | POL                      | pl-PL / en-US                         |
| Portugal                                 | PT                       | PRT                      | pt-PT / en-US                         |
| Porto Rico                              | PR                       | PRI                      | es-PR / en-US                         |
| Qatar                                    | QA                       | QAT                      | ar-QA / en-US                         |
| La Réunion                                  | RE                       | REU                      | fr-FR / en-US                         |
| Roumanie                                  | RO                       | ROU                      | ro-RO / en-US                         |
| Russie                                   | RU                       | RUS                      | ru-RU / en-US                         |
| Rwanda                                   | RW                       | Accès web à distance                      | rw-RW / en-US                         |
| Saba                                     | XS                       | XSA                      | nl-NL / en-US                         |
| Saint Kitts et Nevis                    | KN                       | KNA                      | en-GB / en-US                         |
| Sainte-Lucie                              | LC                       | LCA                      | en-US                                 |
| Saint-Martin                             | MF                       | MAF                      | fr-FR / en-US                         |
| Saint-Pierre-et-Miquelon                | PM                       | SPM                      | fr-FR / en-US                         |
| Saint-Vincent-et-les-Grenadines         | VC                       | VCT                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | BLM                      | fr-FR / en-US                         |
| Samoa                                    | WS                       | WSM                      | en-US                                 |
| Saint-Marin                               | SM                       | SMR                      | it-IT / en-US                         |
| São Tomé et Príncipe                    | ST                       | STP                      | pt-PT / en-US                         |
| Arabie saoudite                             | SA                       | SAU                      | ar-SA / en-US                         |
| Sénégal                                  | SN                       | SEN                      | wo-SN / en-US                         |
| Serbie                                   | RS                       | SRB                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| Seychelles                               | SC                       | SYC                      | en-US                                 |
| Sierra Leone                             | SL                       | SLE                      | en-US                                 |
| Singapour                                | SG                       | SGP                      | en-SG / zh-SG / en-US                 |
| Sint Eustatius                           | XE                       | XSE                      | nl-NL / en-US                         |
| Saint-Martin (Royaume des Pays-Bas)                             | SX                       | SXM                      | en-US                                 |
| Slovaquie                                 | SK                       | SVK                      | sk-SK / en-US                         |
| Slovénie                                 | SI                       | SVN                      | sl-SI / en-US                         |
| Salomon (îles)                          | SB                       | SLB                      | en-US                                 |
| Somalie                                  | SO                       | SOM                      | ar-SA / en-US                         |
| Afrique du Sud                             | ZA                       | ZAF                      | en-ZA / en-US                         |
| South Georgia and South Sandwich Islands | GS                       | SGS                      | en-US                                 |
| Soudan du Sud                              | SS                       | SSD                      | en-US                                 |
| Espagne                                    | ES                       | ESP                      | es-ES / ca-ES / eu-ES / gl-ES / en-US |
| Sri Lanka                                | LK                       | LKA                      | si-LK / en-US                         |
| St Helena, Ascension, Tristan da Cunha   | SH                       | SHN                      | en-US                                 |
| Surinam                                 | SR                       | SUR                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | nb-NO / en-US                         |
| Suède                                   | SE                       | SWE                      | sv-SE / en-US                         |
| Suisse                              | CH                       | CHE                      | de-CH / fr-CH / it-CH / en-US         |
| Taïwan                                   | TW                       | TWN                      | zh-TW / en-US                         |
| Tadjikistan                               | TJ                       | TJK                      | tg-Cyrl-TJ / en-US                    |
| Tanzanie                                 | TZ                       | TZA                      | en-GB / en-US                         |
| Thaïlande                                 | TH                       | THA                      | th-TH / en-US                         |
| Timor-Leste                              | TL                       | TLS                      | pt-PT / en-US                         |
| Togo                                     | TG                       | TGO                      | fr-FR / en-US                         |
| Tokelau                                  | TK                       | TKL                      | en-US                                 |
| Tonga                                    | TO                       | TON                      | en-US                                 |
| Trinité-et-Tobago                      | TT                       | TTO                      | en-TT / en-US                         |
| Tunisie                                  | TN                       | TUN                      | ar-TN / en-US                         |
| Turquie                                   | TR                       | TUR                      | tr-TR / en-US                         |
| Turkménistan                             | TM                       | TKM                      | tk-TM / en-US                         |
| Turks et Caïcos (îles)                 | TC                       | TCA                      | en-US                                 |
| Tuvalu                                   | TV                       | TUV                      | en-US                                 |
| Ouganda                                   | UG                       | UGA                      | en-GB / en-US                         |
| Ukraine                                  | UA                       | UKR                      | uk-UA / en-US                         |
| Émirats arabes unis                     | AE                       | ARE                      | ar-AE / en-US                         |
| Royaume-Uni                           | Go                       | GBR                      | en-GB / en-US                         |
| Îles mineures éloignées des États-Unis                    | UM                       | UMI                      | en-US                                 |
| Îles Vierges (É.-U.)                      | VI                       | VIR                      | en-US                                 |
| États-Unis                            | États-Unis                       | États-Unis                      | en-US / es-US                         |
| Uruguay                                  | UY                       | URY                      | es-UY / en-US                         |
| Ouzbékistan                               | UZ                       | UZB                      | uz-Latn-UZ / en-US                    |
| Vanuatu                                  | VU                       | VUT                      | en-US                                 |
| Cité du Vatican                             | VA                       | VAT                      | it-IT / en-US                         |
| Venezuela                                | VE                       | VEN                      | es-VE / en-US                         |
| Vietnam                                  | VN                       | VNM                      | vi-VN / en-US                         |
| Wallis-et-Futuna                        | WF                       | WLF                      | fr-FR / en-US                         |
| Yémen                                    | YE                       | YEM                      | ar-YE / en-US                         |
| Zambie                                   | ZM                       | ZMB                      | en-GB / en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW / en-US                         |

