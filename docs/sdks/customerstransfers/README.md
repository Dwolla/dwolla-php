# Customers.Transfers

## Overview

### Available Operations

* [list](#list) - List and search transfers for a customer

## list

Retrieve and search transfers for a specific Customer with comprehensive filtering and pagination support. Supports searching by customer details (name, email, business name), amount ranges, date ranges, transfer status, and correlation IDs for enhanced transaction discovery. Returns paginated transfer results including status, amounts, metadata, and links to source and destination funding sources. Use this endpoint for transaction history analysis and reconciliation purposes.

### Example Usage

<!-- UsageSnippet language="php" operationID="listCustomerTransfers" method="get" path="/customers/{id}/transfers" -->
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

$request = new Operations\ListCustomerTransfersRequest(
    id: '<id>',
);

$response = $sdk->customers->transfers->list(
    request: $request
);

if ($response->transfers !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                          | Type                                                                                               | Required                                                                                           | Description                                                                                        |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `$request`                                                                                         | [Operations\ListCustomerTransfersRequest](../../Models/Operations/ListCustomerTransfersRequest.md) | :heavy_check_mark:                                                                                 | The request object to use for the request.                                                         |

### Response

**[?Operations\ListCustomerTransfersResponse](../../Models/Operations/ListCustomerTransfersResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |