---
title: Utility resources
description: The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b19eb80c5be2cc07bd325681f9870a1af7fed481
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486249"
---
# <a name="utility-resources"></a>Utility resources


**Applies To**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.


## <a name="span-idaddressspan-idaddressaddress"></a><span id="address"/><span id="ADDRESS"/>Address

An address to use for the customer or for partner profiles. For more information about the supported formats and properties in different countries/regions, see [Get address formatting rules by market](get-market-specific-validation-data.md).

| Propriété     | Tapez   | Length (min, max) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | chaîne | (1, 200)          | The first line of the address.                                                                   |
| AddressLine2 | chaîne | (0, 200)          | The second line of the address. Cette propriété est facultative.                                       |
| Ville         | chaîne | Non applicable               | The city.                                                                                        |
| Région        | chaîne | (0, 2)            | The state.                                                                                       |
| PostalCode   | chaîne | Non applicable               | The ZIP code or postal code.                                                                     |
| Country      | chaîne | (2, 2)            | The country/region in ISO country code format.                                                   |
| Région       | chaîne | Non applicable               | The region.                                                                                      |
| Prénom    | chaîne | (1, 50)           | The first name of a contact at the customer's company/organization.                              |
| LastName     | chaîne | (1, 50)           | The last name of a contact at the customer's company/organization.                               |
| PhoneNumber  | chaîne | Non applicable               | The phone number of a contact at the customer's company/organization. Cette propriété est facultative. |
 

## <a name="span-idcontactspan-idcontactspan-idcontactcontact"></a><span id="Contact"/><span id="contact"/><span id="CONTACT"/>Contact

Describes contact information for a specific individual.

| Propriété    | Tapez   | Description                  |
|-------------|--------|------------------------------|
| Prénom   | chaîne | The contact's first name.    |
| LastName    | chaîne | The contact's last name.     |
| E-mail       | chaîne | The contact's email address. |
| PhoneNumber | chaîne | The contact's phone number.  |
 

## <a name="span-idfieldfilterspan-idfieldfilterspan-idfieldfilterfieldfilter"></a><span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

Describes a filter that can be applied to search results.

| Propriété | Tapez   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Opérateur | chaîne | The filter operator: "equals", "not\_equals", "greater\_than", "greater\_than\_or\_equals", "less\_than", "less\_than\_or\_equals", "substring", "and", "or", "starts\_with", "not\_starts\_with". |
 

## <a name="span-idfileinfospan-idfileinfospan-idfileinfofileinfo"></a><span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

Represents an external file uploaded to Partner Center.

| Propriété                 | Tapez   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Comment                  | chaîne | A comment associated with the file upload.    |
| FileExtension            | chaîne | The file extension.                           |
| FileNameWithoutExtension | chaîne | The name of the file, extension not included. |
| FileSize                 | longue   | The size of the file.                         |
| Id                       | chaîne | The unique ID for the file upload.            |
 

## <a name="span-idlinkspan-idlinkspan-idlinklink"></a><span id="Link"/><span id="link"/><span id="LINK"/>Link

Contains a URI link and associated information.

| Propriété | Tapez                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | chaîne                 | The URI.                           |
| Méthode   | chaîne                 | The method represented by the URI. |
| En-têtes  | Array of KeyValuePairs | The headers for the link.          |
 

## <a name="span-idpasswordprofilespan-idpasswordprofilespan-idpasswordprofilepasswordprofile"></a><span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

Describes a specific password and if that password needs to be changed.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

| Propriété            | Tapez                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Mot de passe            | [SecureString](#securestring) | The password.                                                          |
| ForceChangePassword | booléen                       | Determines if the password needs to be forcibly changed on next login. |
 

## <a name="span-idresourcelinksspan-idresourcelinksspan-idresourcelinksresourcelinks"></a><span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

Contains a list of links for a resource.

| Propriété   | Tapez                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self (Auto)       | [Link](#link)                             | The self URI.                                      |
| Suivant       | [Link](#link)                             | The next page of items.                            |
| Previous   | [Link](#link)                             | The previous page of items.                        |
| Attributs | [ResourceAttributes](#resourceattributes) | The metadata attributes corresponding to the user. |
 

## <a name="span-idresourceattributesspan-idresourceattributesspan-idresourceattributesresourceattributes"></a><span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

Contains attribute metadata for a resource.

| Propriété   | Tapez   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | chaîne | The etag, also known as the object version. |
| ObjectType | chaîne | The type of object of the base resource.    |
 

## <a name="span-idsecurestringspan-idsecurestringspan-idsecurestringsecurestring"></a><span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

Stores secured information, such as a password.

| Propriété | Tapez | Description                       |
|----------|------|-----------------------------------|
| Durée   | entier  | The length of the secured string. |


## <a name="span-idvalidationcodespan-idvalidationcodespan-idvalidationcodevalidationcode"></a><span id="ValidationCode"/><span id="validationcode"/><span id="VALIDATIONCODE"/>ValidationCode

Represents a partner's Government Community Cloud validation code.

| Propriété         | Tapez         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Partner identifier                                                       |
| OrganizationName | chaîne       | The organization name provided during the validation process             |
| ValidationId     | entier          | A unique identifier for validation                                       |
| MaxCreates       | nullable int | The maximum customers allowed to be created with this validation code    |
| RemainingCreates | nullable int | Remaining customer creates under this validation ID                      |
| ETag             | chaîne       | The specific version of this resource. Changes when resource is changed. |
