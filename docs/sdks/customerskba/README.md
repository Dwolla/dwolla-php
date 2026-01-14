# Customers.Kba

## Overview

### Available Operations

* [initiate](#initiate) - Initiate a KBA session

## initiate

Creates a new KBA (Knowledge-Based Authentication) session for a personal Verified Customer. Returns a KBA identifier that represents the session and is used to retrieve authentication questions for customer verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="initiateKbaForCustomer" method="post" path="/customers/{id}/kba" -->
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



$response = $sdk->customers->kba->initiate(
    id: '<id>'
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                           | Type                                                | Required                                            | Description                                         |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| `id`                                                | *string*                                            | :heavy_check_mark:                                  | The ID of the Customer for initiating a KBA session |

### Response

**[?Operations\InitiateKbaForCustomerResponse](../../Models/Operations/InitiateKbaForCustomerResponse.md)**

### Errors

| Error Type                                 | Status Code                                | Content Type                               |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| Errors\InvalidResourceStateSchemaException | 403                                        | application/vnd.dwolla.v1.hal+json         |
| Errors\ForbiddenError                      | 403                                        | application/vnd.dwolla.v1.hal+json         |
| Errors\NotFoundError                       | 404                                        | application/vnd.dwolla.v1.hal+json         |
| Errors\APIException                        | 4XX, 5XX                                   | \*/\*                                      |