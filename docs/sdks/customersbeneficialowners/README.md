# Customers.BeneficialOwners

## Overview

### Available Operations

* [list](#list) - List customer beneficial owners
* [create](#create) - Create customer beneficial owner

## list

Returns all beneficial owners associated with a business verified customer. Beneficial owners are individuals who directly or indirectly own 25% or more of the company's equity. Includes personal information, verification status, and address details for each owner.

### Example Usage

<!-- UsageSnippet language="php" operationID="listBeneficialOwnersForCustomer" method="get" path="/customers/{id}/beneficial-owners" -->
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



$response = $sdk->customers->beneficialOwners->list(
    id: '<id>'
);

if ($response->beneficialOwners !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | Customer unique identifier |

### Response

**[?Operations\ListBeneficialOwnersForCustomerResponse](../../Models/Operations/ListBeneficialOwnersForCustomerResponse.md)**

### Errors

| Error Type                                                     | Status Code                                                    | Content Type                                                   |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| Errors\ListBeneficialOwnersForCustomerDwollaV1HalJSONException | 404                                                            | application/vnd.dwolla.v1.hal+json                             |
| Errors\APIException                                            | 4XX, 5XX                                                       | \*/\*                                                          |

## create

Creates a new beneficial owner for a business verified customer. Beneficial owners are individuals who own 25% or more of the company's equity. Requires personal information, address, and SSN or passport for identity verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="createBeneficialOwnerForCustomer" method="post" path="/customers/{id}/beneficial-owners" -->
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



$response = $sdk->customers->beneficialOwners->create(
    id: '<id>',
    body: new Components\CreateUSBeneficialOwner(
        firstName: 'John',
        lastName: 'Doe',
        dateOfBirth: '1980-01-31',
        address: new Components\InternationalAddress(
            address1: '462 Main Street',
            address2: 'Suite 123',
            address3: 'Unit 123',
            city: 'Des Moines',
            postalCode: '50309',
            country: 'USA',
            stateProvinceRegion: 'IA',
        ),
        ssn: '123456789',
    )

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                  | Type                                                                                                                                                       | Required                                                                                                                                                   | Description                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                       | *string*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                         | Customer ID for which to create a Beneficial Owner                                                                                                         |
| `body`                                                                                                                                                     | [Components\CreateUSBeneficialOwner\|Components\CreateInternationalBeneficialOwner](../../Models/Operations/CreateBeneficialOwnerForCustomerRequestBody.md) | :heavy_check_mark:                                                                                                                                         | Parameters for creating a beneficial owner                                                                                                                 |

### Response

**[?Operations\CreateBeneficialOwnerForCustomerResponse](../../Models/Operations/CreateBeneficialOwnerForCustomerResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\BadRequestError             | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |