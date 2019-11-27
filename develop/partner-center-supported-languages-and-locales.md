---
title: Langues et paramètres régionaux pris en charge par l’espace partenaires
description: Liste des paramètres régionaux pris en charge par ISO2 et ISO3 pour l’espace partenaires.
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
# <a name="partner-center-supported-languages-and-locales"></a>Langues et paramètres régionaux pris en charge par l’espace partenaires


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
| Åland (îles d’)                            | PASSANT                       | Unis                      | SV-SE/en-US                         |
| Albanie                                  | AL                       | ALB                      | Sq-AL/fr-fr                         |
| Algérie                                  | DZ                       | DZA                      | ar-DZ/fr-fr                         |
| Samoa américaines                           | AS                       | ASM                      | fr-FR                                 |
| Andorre                                  | AD                       | ET                      | ca-ES/en-US                         |
| Angola                                   | AO                       | EU                      | PT-PT/en-US                         |
| Anguilla                                 | IA                       | AIA                      | fr-FR                                 |
| Antarctique                               | INACTIF                       | ATA                      | fr-FR                                 |
| Antigua-et-Barbuda                      | GA                       | ATG                      | fr-FR                                 |
| Argentine                                | AR                       | DONNÉE                      | es-AR/fr-fr                         |
| Arménie                                  | AM                       | ARM                      | HY-AM/en-US                         |
| Aruba                                    | AW                       | ABW                      | NL-NL/en-US                         |
| Australie                                | AU                       | UNITÉS Analytics                      | en-dessous/en-US                         |
| Autriche                                  | AT                       | CONFORMITÉ                      | de-AT/fr-fr                         |
| Azerbaïdjan                               | AZ                       | AZE                      | az-Latn-AZ/fr-US                    |
| Bahamas                                  | BS                       | BHS                      | en-GB/fr-fr                         |
| Bahreïn                                  | BH                       | BHR                      | AR-BH/fr-fr                         |
| Bangladesh                               | BD                       | BGD                      | -BD/fr-fr                         |
| Barbade (La)                                 | BB                       | BRB                      | en-GB/fr-fr                         |
| Bélarus                                  | BY                       | BLR                      | être par/en-US                         |
| Belgique                                  | BE                       | BEL                      | fr-a/NL-is/fr-US                 |
| Belize                                   | Via                       | BLZ                      | en-via/fr-fr                         |
| Bénin                                    | BJ                       | BEN                      | fr-FR/fr-fr                         |
| Bermudes                                  | NOMENCLATURE                       | BMU                      | en-GB/fr-fr                         |
| Bhoutan                                   | CC                       | BTN                      | fr-FR                                 |
| Bolivie                                  | BO                       | BOL                      | es-BO/fr-fr                         |
| Bonaire                                  | BQ                       | BES                      | NL-NL/en-US                         |
| Bosnie-Herzégovine                   | BA                       | RELATIF                      | bs-Latn-BA/fr-US                    |
| Botswana                                 | BW                       | BWA                      | en-GB/fr-fr                         |
| Bouvet (Île)                            | BV                       | BVT                      | NB-non/en-US                         |
| Brésil                                   | BR                       | BRA                      | PT-BR/fr-fr                         |
| Territoires britanniques de l’océan Indien           | E/S                       | IOT                      | fr-FR                                 |
| Îles Vierges britanniques                   | VG                       | VGB                      | fr-FR                                 |
| Brunéi Darussalam                                   | BN                       | BRN                      | MS-m/en-US                         |
| Bulgarie                                 | BG                       | BGR                      | BG-BG/fr-fr                         |
| Burkina-Faso                             | BF                       | BFA                      | fr-FR/fr-fr                         |
| Burundi                                  | DÉCISIONNEL                       | BDI                      | fr-FR/fr-fr                         |
| Cap Vert                               | CV                       | CPV                      | PT-CV/fr-fr                         |
| Cambodge                                 | KH                       | KHM                      | km-KH/en-US                         |
| Cameroun                                 | CM                       | ENVOYÉS                      | fr-FR/fr-fr                         |
| Canada                                   | AC                       | PUISSIEZ                      | fr-CA/fr-fr                         |
| Caïmans (îles)                           | KY                       | CYM                      | en-GB/fr-fr                         |
| République centrafricaine                 | CF                       | CAF                      | fr-FR/fr-fr                         |
| Tchad                                     | ÉQUIPEMENTS                       | TCD                      | fr-FR/fr-fr                         |
| Chili                                    | CL                       | CHL                      | es-CL/fr-fr                         |
| Chine                                    | CN                       | CHN                      | zh-CN/fr-fr                         |
| Christmas (île)                         | CX                       | CXR                      | fr-FR                                 |
| Cocos-Keeling (îles)                  | CC                       | CCK                      | fr-FR                                 |
| Colombie                                 | CO                       | COL                      | es-CO/en-US                         |
| Comores (Les)                                  | KILOMÈTRES                       | COM                      | fr-FR/fr-fr                         |
| Congo                                    | CG                       | ROUE dentée                      | fr-FR/fr-fr                         |
| Congo (RDC)                              | CD-ROM                       | VENDUS                      | fr-FR/fr-fr                         |
| Cook (îles)                             | HT                       | COK                      | fr-FR                                 |
| Costa Rica                               | CR                       | RAPPORT personnalisé                      | es-CR/fr-fr                         |
| Côte d’Ivoire                            | CI                       | CIV                      | fr-FR/fr-fr                         |
| Croatie                                  | HR                       | HRV                      | HR-HR/fr-fr                         |
| Curaçao                                  | APPROXIMATIF                       | CUW                      | NL-NL/en-US                         |
| Chypre                                   | CY                       | CYP                      | El-GR/fr-fr                         |
| Czechia                                  | CZ                       | CZE                      | CS-CZ/fr-fr                         |
| Danemark                                  | DK                       | DNK                      | da-DK/fr-fr                         |
| Djibouti                                 | EFFECTUÉ                       | DJI                      | fr-FR/fr-fr                         |
| Dominique                                 | EXPLORATION                       | CANAL                      | fr-FR                                 |
| République dominicaine                       | DO                       | Loc                      | es-DO/en-US                         |
| Équateur (République de)                                  | EC                       | ÉCU                      | es-EC/fr-fr                         |
| Égypte                                    | EG                       | EGY                      | AR-EG/fr-fr                         |
| Salvador                              | SV                       | SLV                      | es-VP/en-US                         |
| Guinée équatoriale                        | GQ                       | GNQ                      | es-ES/en-US                         |
| Érythrée                                  | ERRE                       | ERI                      | ar-SA/en-US                         |
| Estonie                                  | EE                       | ESTIMÉ                      | et-EE/fr-fr                         |
| eSwatini                                 | SZ                       | SWZ                      | fr-FR                                 |
| Éthiopie                                 | Mendes                       | Ed                      | AM-ET/en-US                         |
| Malouines (îles)                         | FK                       | FLK                      | fr-FR                                 |
| Féroé (îles)                            | FO                       | PROVENANT                      | FO-FO/fr-fr                         |
| Fidji                                     | FJ                       | FJI                      | en-GB/fr-fr                         |
| Finlande                                  | FI                       | FIN                      | fi-fi/sv-FI/FR-US                 |
| France                                   | FR                       | FRA                      | fr-FR/fr-fr                         |
| Guyane française                            | GF                       | GUF                      | fr-FR/fr-fr                         |
| Polynésie française                         | UTIL                       | PYF                      | fr-FR/fr-fr                         |
| Terres australes françaises              | TF                       | ATF                      | fr-FR/fr-fr                         |
| Gabon                                    | GA                       | CARNET                      | fr-FR/fr-fr                         |
| Gambie                                   | GÉNÉTIQUE                       | GMB                      | fr-FR                                 |
| Géorgie                                  | GE                       | LOCAL                      | Ka-GE/en-US                         |
| Allemagne                                  | DE                       | DEU                      | de-fr/fr-fr                         |
| Ghana                                    | GH                       | GHA                      | en-GB/fr-fr                         |
| Gibraltar                                | GI                       | Gio                      | fr-FR                                 |
| Grèce                                   | GR                       | GRC                      | El-GR/fr-fr                         |
| Groenland                                | GÉNÉRALE                       | GRL                      | da-DK/fr-fr                         |
| Grenade                                  | GD                       | GRD                      | fr-FR                                 |
| Guadeloupe                               | MARGE                       | AUX                      | fr-FR/fr-fr                         |
| Guam                                     | GU                       | GENCIVE                      | fr-FR                                 |
| Guatemala                                | GT                       | GTM                      | es-GT/en-US                         |
| Guernesey                                 | GG                       | GGY                      | fr-FR                                 |
| Guinée                                   | GN                       | GIN                      | fr-FR/fr-fr                         |
| Guinée-Bissau                            | ENTREPÔT                       | GNB                      | PT-PT/en-US                         |
| Guyana                                   | GY                       | EXPERT                      | fr-FR                                 |
| Haïti                                    | HT                       | HTI                      | fr-FR/fr-fr                         |
| Heard et McDonald (Îles)        | Britannique                       | HMD                      | fr-FR                                 |
| Honduras                                 | HN                       | HND                      | es-HN/en-US                         |
| Hong Kong R.A.S.                            | HK                       | HKG                      | zh-HK/fr-fr                         |
| Hongrie                                  | HU                       | HUN                      | HU-HU/fr-fr                         |
| Islande                                  | IS                       | SANDWICH                      | IS-IS/fr-fr                         |
| Inde                                    | IN                       | HERCHER                      | en-IN/HI-IN/fr-fr                 |
| Indonésie                                | ID                       | IDN                      | ID-ID/fr-fr                         |
| Irak                                     | IQ                       | IRQ                      | AR-IQ/fr-fr                         |
| Irlande                                  | Internet Explorer                       | IRL                      | en-IE/en-US                         |
| Île de Man                              | Messagerie instantanée                       | IMN                      | fr-FR                                 |
| Israël                                   | IL                       | ISR                      | He-IL/en-US                         |
| Italie                                    | Informatique                       | ITA                      | informatique-informatique/fr-fr                         |
| Jamaïque                                  | JM                       | BOURRAGE                      | en-JM/fr-fr                         |
| Jan Mayen                                | XJ                       | XJA                      | NB-non/en-US                         |
| Japon                                    | JP                       | JPN                      | ja-JP/fr-fr                         |
| Jersey                                   | JE                       | JEY                      | fr-FR                                 |
| Jordanie                                   | JO                       | JOR                      | AR-JO/en-US                         |
| Kazakhstan                               | KZ                       | KAZ                      | KK-KZ/en-US                         |
| Kenya                                    | KE                       | KEN                      | SW-KE/fr-US                         |
| Kiribati                                 | KI                       | KIR                      | fr-FR                                 |
| Corée                                    | KR                       | KOR                      | ko-KR/en-US                         |
| Kosovo                                   | XK                       | XKS                      | fr-FR                                 |
| Koweït                                   | KW                       | KWT                      | AR-KW/fr-fr                         |
| Kirghizistan                               | KG                       | KGZ                      | KY-KG/en-US                         |
| Laos                                     | LA                       | SYMBOLE                      | Lo-LA/en-US                         |
| Lettonie                                   | LV                       | LVA                      | LV-LV/en-US                         |
| Liban                                  | LB                       | LBN                      | ar-LB/en-US                         |
| Lesotho                                  | LS                       | LSO                      | fr-FR                                 |
| Liberia                                  | GD                       | LBR                      | fr-FR                                 |
| Libye                                    | EMPLOYÉS                       | LBY                      | AR-EP/fr-fr                         |
| Liechtenstein                            | LI                       | INCOMB                      | de-LI/fr-fr                         |
| Lituanie                                | LT                       | LTU                      | lt-LT/fr-fr                         |
| Luxembourg                               | LU                       | LUX                      | de-LU/FR-LU/fr-fr                 |
| Macao R.A.S.                                | MOLYBDÈN                       | MAC                      | zh-MO/fr-fr                         |
| Macédoine, Ex.-Rép. yougoslave de                          | MK                       | MKD                      | MK-MK/fr-fr                         |
| Madagascar                               | ML                       | MDG                      | fr-FR/fr-fr                         |
| Malawi                                   | MW                       | MWI                      | fr-FR                                 |
| Malaisie                                 | MY                       | MYS                      | en-MY/fr-US                         |
| Maldives                                 | MV                       | MDV                      | DV-MV/en-US                         |
| Mali                                     | ENVIRON                       | MLI                      | fr-FR/fr-fr                         |
| Malte                                    | MT                       | MLT                      | MT-MT/fr-US                         |
| Marshall (îles)                         | MH                       | MHL                      | fr-FR                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR/fr-fr                         |
| Mauritanie                               | MR                       | MRT                      | ar-SA/en-US                         |
| Maurice                                | MU                       | MUS                      | en-GB/fr-fr                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR/fr-fr                         |
| Mexique                                   | MX                       | MEX                      | es-MX/fr-fr                         |
| Micronésie                               | Radio                       | FSM                      | fr-FR                                 |
| République de Moldavie                                  | MD                       | MDA                      | RO-RO/fr-fr                         |
| Monaco                                   | MC                       | MCO                      | fr-MC/fr-fr                         |
| Mongolie                                 | PORTABLE                       | MNG                      | mn-MN/fr-fr                         |
| Monténégro                               | ME                       | MNE                      | SR-LATN-ME/fr-fr                    |
| Montserrat                               | MS                       | Caisse                      | fr-FR                                 |
| Maroc                                  | MA                       | MARS                      | AR-MA/en-US                         |
| Mozambique                               | MZ                       | MOZ                      | PT-PT/en-US                         |
| Myanmar                                  | MM                       | MMR                      | fr-FR                                 |
| Namibie                                  | N/A                       | NAM                      | en-GB/fr-fr                         |
| Nauru                                    | NR                       | NRU                      | fr-FR                                 |
| Népal                                    | NP                       | NPL                      | Nou-NP/fr-fr                         |
| Antilles néerlandaises                     | PIÈCE                       | IN                      | fr-FR                                 |
| Pays-Bas, le                         | NL                       | NLD                      | NL-NL/en-US                         |
| Nouvelle-Calédonie                            | OBTEN                       | NCL                      | fr-FR/fr-fr                         |
| Nouvelle-Zélande                              | NZ                       | NZL                      | en-NZ/en-US                         |
| Nicaragua                                | NI                       | INTERFACE                      | es-NI/en-US                         |
| Niger                                    | NE                       | NER                      | fr-FR/fr-fr                         |
| Nigeria                                  | NG                       | NGA                      | ha-LATN-NG/fr-fr                    |
| Niue                                     | NU                       | NIU                      | fr-FR                                 |
| Norfolk (île)                           | NF                       | NFK                      | fr-FR                                 |
| Mariannes du Nord (îles)                 | MP                       | MNP                      | fr-FR                                 |
| Norvège                                   | NON                       | NOR                      | NB-non/en-US                         |
| Oman                                     | OM                       | OMN                      | AR-OM/en-US                         |
| Pakistan                                 | PK                       | RESOURCEPAK                      | Your-PK/fr-fr                         |
| Palau                                    | CONFIGURER passe                       | PLW                      | fr-FR                                 |
| Autorité palestinienne                    | PS                       | PRODUIT                      | ar-SA/en-US                         |
| Panama                                   | AF                       | PAN                      | es-PA/en-US                         |
| Papouasie-Nouvelle-Guinée                         | SOUHAITABLE                       | PNG                      | fr-FR                                 |
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
| Rwanda                                   | GRAVE                       | Accès web à distance                      | RW-RW/en-US                         |
| Saba                                     | XS                       | XSA                      | NL-NL/en-US                         |
| Saint Kitts et Nevis                    | KN                       | KNA                      | en-GB/fr-fr                         |
| Sainte-Lucie                              | EUROS                       | LCA                      | fr-FR                                 |
| Saint-Martin                             | INSTANTANÉ                       | MAF                      | fr-FR/fr-fr                         |
| Saint-Pierre-et-Miquelon                | Manuel                       | SPM                      | fr-FR/fr-fr                         |
| Saint-Vincent-et-les-Grenadines         | VIRTUEL                       | VCT                      | fr-FR                                 |
| Saint--Barthélemy                         | BL                       | BLM                      | fr-FR/fr-fr                         |
| Samoa                                    | Web                       | WSM                      | fr-FR                                 |
| Saint-Marin                               | MS                       | SMR                      | informatique-informatique/fr-fr                         |
| São Tomé et Príncipe                    | ST                       | Protocole                      | PT-PT/en-US                         |
| Arabie saoudite                             | SA                       | SAU                      | ar-SA/en-US                         |
| Sénégal                                  | SN                       | Send                      | WO-SN/en-US                         |
| Serbie                                   | RS                       | SRB                      | SR-LATN-RS/SR-Cyrl-RS/fr-US       |
| Seychelles                               | SC                       | SYC                      | fr-FR                                 |
| Sierra Leone                             | SL                       | UNIQUE                      | fr-FR                                 |
| Singapour                                | SG                       | SGP                      | fr-SG/zh-SG/fr-fr                 |
| Saint-Eustache                           | XE                       | XSE                      | NL-NL/en-US                         |
| Saint-Martin (Royaume des Pays-Bas)                             | SX                       | SXM                      | fr-FR                                 |
| Slovaquie                                 | SK                       | SVK                      | SK-SK/fr-fr                         |
| Slovénie                                 | SI                       | SVN                      | SL-SI/en-US                         |
| Salomon (îles)                          | ASPIRATEUR                       | SLB                      | fr-FR                                 |
| Somalie                                  | AFIN                       | MODÈLE                      | ar-SA/en-US                         |
| Afrique du Sud                             | ZA                       | ZAF                      | en-ZA/fr-fr                         |
| Géorgie du Sud et Sandwich du Sud (îles) | GS                       | SGS                      | fr-FR                                 |
| Soudan du Sud                              | SÉCURITÉ                       | SSD                      | fr-FR                                 |
| Espagne                                    | ES                       | ESP                      | es-ES/ca-ES/UE-ES/GL-ES/fr-fr |
| Sri Lanka                                | LK                       | LKA                      | Si-LK/fr-fr                         |
| Sainte-Hélène, ascension, Tristan da Cunha   | &                       | SHN                      | fr-FR                                 |
| Surinam                                 | SR                       | SUR                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | NB-non/en-US                         |
| Suède                                   | SE                       | $ $                      | SV-SE/en-US                         |
| Suisse                              | CH                       | TCHE                      | de-CH/fr-CH/IT-CH/fr-fr         |
| Taïwan                                   | TW                       | TWN                      | zh-TW/fr-fr                         |
| Tadjikistan                               | TJ                       | TJK                      | TG-Cyrl-TJ/fr-US                    |
| Tanzanie                                 | TZ                       | TZA                      | en-GB/fr-fr                         |
| Thaïlande                                 | TH                       | THA                      | th-TH/en-US                         |
| Timor-Leste                              | TL                       | TLS                      | PT-PT/en-US                         |
| Togo                                     | OCDE                       | TGO                      | fr-FR/fr-fr                         |
| Tokelau                                  | J                       | TKL                      | fr-FR                                 |
| Tonga                                    | À                       | MILLIERS                      | fr-FR                                 |
| Trinité-et-Tobago                      | TT                       | POUR                      | en-TT/en-US                         |
| Tunisie                                  | TN                       | Exécutez                      | AR-TN/fr-fr                         |
| Turquie                                   | TR                       | Ready                      | TR-TR/en-US                         |
| Turkménistan                             | TM                       | TKM                      | TK-TM/fr-fr                         |
| Turks et Caïcos (îles)                 | CT                       | ÉLÉMENTAIRE                      | fr-FR                                 |
| Tuvalu                                   | TV                       | CERTIFIÉ                      | fr-FR                                 |
| Ouganda                                   | UG                       | UGA                      | en-GB/fr-fr                         |
| Ukraine                                  | UA                       | UKR                      | Royaume-Uni-UA/fr-US                         |
| Émirats arabes unis                     | AE                       | SERONT                      | AR-AE/fr-fr                         |
| Royaume-Uni                           | Go                       | GBR                      | en-GB/fr-fr                         |
| Îles mineures éloignées des États-Unis                    | UNIFIÉ                       | UMI                      | fr-FR                                 |
| Îles Vierges (É.-U.)                      | VL                       | VIR                      | fr-FR                                 |
| États-Unis                            | US                       | USA                      | fr-fr/es-US                         |
| Uruguay                                  | UY                       | URY                      | es-UY/fr-fr                         |
| Ouzbékistan                               | UZ                       | UZB                      | uz-LATN-UZ/fr-US                    |
| Vanuatu                                  | VOU                       | VUT                      | fr-FR                                 |
| État de la Cité du Vatican                             | VA                       | T.V.A.                      | informatique-informatique/fr-fr                         |
| Venezuela                                | VE                       | ENSEMBLE                      | es-VE/fr-fr                         |
| Vietnam                                  | VN                       | VNM                      | vi-VN/en-US                         |
| Wallis-et-Futuna                        | WF                       | WLF                      | fr-FR/fr-fr                         |
| Yémen                                    | POUSSE                       | YEM                      | AR-Yé/en-US                         |
| Zambie                                   | ZM                       | ZMB                      | en-GB/fr-fr                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW/fr-fr                         |

