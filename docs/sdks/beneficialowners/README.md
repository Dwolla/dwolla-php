# BeneficialOwners

## Overview

### Available Operations

* [get](#get) - Retrieve beneficial owner
* [update](#update) - Update beneficial owner
* [delete](#delete) - Remove beneficial owner

## get

Returns detailed information for a specific beneficial owner, including personal information, address, and verification status. The verification status indicates the owner's identity verification progress and affects the business customer's transaction capabilities.

### Example Usage

<!-- UsageSnippet language="php" operationID="retrieveBeneficialOwner" method="get" path="/beneficial-owners/{id}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();



$response = $sdk->beneficialOwners->get(
    id: '<id>'
);

if ($response->beneficialOwner !== null) {
    // handle response
}
```

### Parameters

| Parameter                          | Type                               | Required                           | Description                        |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `id`                               | *string*                           | :heavy_check_mark:                 | Beneficial owner unique identifier |

### Response

**[?Operations\RetrieveBeneficialOwnerResponse](../../Models/Operations/RetrieveBeneficialOwnerResponse.md)**

### Errors

| Error Type                                             | Status Code                                            | Content Type                                           |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Errors\RetrieveBeneficialOwnerDwollaV1HalJSONException | 404                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\APIException                                    | 4XX, 5XX                                               | \*/\*                                                  |

## update

Updates a beneficial owner's information to retry verification when their status is "incomplete". Only beneficial owners with incomplete verification status can be updated. Used to correct information that caused initial verification to fail.

### Example Usage

<!-- UsageSnippet language="php" operationID="updateBeneficialOwner" method="post" path="/beneficial-owners/{id}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();



$response = $sdk->beneficialOwners->update(
    id: '<id>',
    body: new Components\CreateInternationalBeneficialOwner(
        firstName: 'Jane',
        lastName: 'Smith',
        dateOfBirth: '1985-03-15',
        address: new Components\InternationalAddress(
            address1: '462 Main Street',
            address2: 'Suite 123',
            address3: 'Unit 123',
            city: 'Des Moines',
            postalCode: '50309',
            country: 'USA',
            stateProvinceRegion: 'IA',
        ),
        passport: new Components\Passport(
            number: '<value>',
            country: 'Montenegro',
        ),
    )

);

if ($response->beneficialOwner !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                       | Type                                                                                                                                            | Required                                                                                                                                        | Description                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                            | *string*                                                                                                                                        | :heavy_check_mark:                                                                                                                              | Beneficial owner unique identifier                                                                                                              |
| `body`                                                                                                                                          | [Components\CreateUSBeneficialOwner\|Components\CreateInternationalBeneficialOwner](../../Models/Operations/UpdateBeneficialOwnerRequestBody.md) | :heavy_check_mark:                                                                                                                              | Parameters for updating a beneficial owner                                                                                                      |

### Response

**[?Operations\UpdateBeneficialOwnerResponse](../../Models/Operations/UpdateBeneficialOwnerResponse.md)**

### Errors

| Error Type                                                    | Status Code                                                   | Content Type                                                  |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| Errors\ValidationErrorSchema                                  | 400                                                           | application/vnd.dwolla.v1.hal+json                            |
| Errors\UpdateBeneficialOwnerForbiddenDwollaV1HalJSONException | 403                                                           | application/vnd.dwolla.v1.hal+json                            |
| Errors\UpdateBeneficialOwnerNotFoundDwollaV1HalJSONException  | 404                                                           | application/vnd.dwolla.v1.hal+json                            |
| Errors\APIException                                           | 4XX, 5XX                                                      | \*/\*                                                         |

## delete

Permanently removes a beneficial owner from a business customer. This action is irreversible and the beneficial owner cannot be retrieved after removal. Removing a beneficial owner will change the customer's certification status to "recertify".

### Example Usage

<!-- UsageSnippet language="php" operationID="deleteBeneficialOwner" method="delete" path="/beneficial-owners/{id}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();



$response = $sdk->beneficialOwners->delete(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                          | Type                               | Required                           | Description                        |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `id`                               | *string*                           | :heavy_check_mark:                 | Beneficial owner unique identifier |

### Response

**[?Operations\DeleteBeneficialOwnerResponse](../../Models/Operations/DeleteBeneficialOwnerResponse.md)**

### Errors

| Error Type                                           | Status Code                                          | Content Type                                         |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| Errors\DeleteBeneficialOwnerDwollaV1HalJSONException | 404                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\APIException                                  | 4XX, 5XX                                             | \*/\*                                                |