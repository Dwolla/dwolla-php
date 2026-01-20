# Customers.BeneficialOwnership

## Overview

### Available Operations

* [get](#get) - Retrieve beneficial ownership status
* [certify](#certify) - Certify beneficial ownership

## get

Returns the certification status of beneficial ownership for a business verified customer. Status indicates whether beneficial owner information has been certified and affects the customer's ability to send funds. Possible values include uncertified, certified, and recertify.

### Example Usage

<!-- UsageSnippet language="php" operationID="getBeneficialOwnershipStatusForCustomer" method="get" path="/customers/{id}/beneficial-ownership" -->
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



$response = $sdk->customers->beneficialOwnership->get(
    id: '<id>'
);

if ($response->beneficialOwnership !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | Customer unique identifier |

### Response

**[?Operations\GetBeneficialOwnershipStatusForCustomerResponse](../../Models/Operations/GetBeneficialOwnershipStatusForCustomerResponse.md)**

### Errors

| Error Type                                                                      | Status Code                                                                     | Content Type                                                                    |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Errors\GetBeneficialOwnershipStatusForCustomerForbiddenDwollaV1HalJSONException | 403                                                                             | application/vnd.dwolla.v1.hal+json                                              |
| Errors\GetBeneficialOwnershipStatusForCustomerNotFoundDwollaV1HalJSONException  | 404                                                                             | application/vnd.dwolla.v1.hal+json                                              |
| Errors\APIException                                                             | 4XX, 5XX                                                                        | \*/\*                                                                           |

## certify

Updates the beneficial ownership certification status to "certified", confirming that all beneficial owner information is accurate and complete. This action enables the business customer to send funds and is required to complete the verification process.

### Example Usage

<!-- UsageSnippet language="php" operationID="certifyBeneficialOwnershipForCustomer" method="post" path="/customers/{id}/beneficial-ownership" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();

$body = new Operations\CertifyBeneficialOwnershipForCustomerRequestBody(
    status: '<value>',
);

$response = $sdk->customers->beneficialOwnership->certify(
    id: '<id>',
    body: $body

);

if ($response->beneficialOwnership !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                  | Type                                                                                                                                       | Required                                                                                                                                   | Description                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                                                       | *string*                                                                                                                                   | :heavy_check_mark:                                                                                                                         | Customer unique identifier                                                                                                                 |
| `body`                                                                                                                                     | [Operations\CertifyBeneficialOwnershipForCustomerRequestBody](../../Models/Operations/CertifyBeneficialOwnershipForCustomerRequestBody.md) | :heavy_check_mark:                                                                                                                         | Parameters for certifying beneficial ownership for a Customer                                                                              |

### Response

**[?Operations\CertifyBeneficialOwnershipForCustomerResponse](../../Models/Operations/CertifyBeneficialOwnershipForCustomerResponse.md)**

### Errors

| Error Type                                                           | Status Code                                                          | Content Type                                                         |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Errors\ValidationErrorSchema                                         | 400                                                                  | application/vnd.dwolla.v1.hal+json                                   |
| Errors\CertifyBeneficialOwnershipForCustomerDwollaV1HalJSONException | 403                                                                  | application/vnd.dwolla.v1.hal+json                                   |
| Errors\APIException                                                  | 4XX, 5XX                                                             | \*/\*                                                                |