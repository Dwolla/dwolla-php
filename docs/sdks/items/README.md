# MassPayments.Items

## Overview

### Available Operations

* [list](#list) - List items for a mass payment
* [get](#get) - Retrieve mass payment item

## list

Retrieve individual payment items within a mass payment with optional status filtering and pagination support. Each item represents a distinct payment with status indicators (failed, pending, success) showing whether a transfer was successfully created. Returns paginated item details including amount, destination, metadata, and error information for failed items. Supports filtering by status and standard pagination.

### Example Usage

<!-- UsageSnippet language="php" operationID="listMassPaymentItems" method="get" path="/mass-payments/{id}/items" -->
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



$response = $sdk->massPayments->items->list(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                      | Type                           | Required                       | Description                    |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| `id`                           | *string*                       | :heavy_check_mark:             | Mass payment unique identifier |
| `limit`                        | *?string*                      | :heavy_minus_sign:             | How many results to return     |
| `offset`                       | *?string*                      | :heavy_minus_sign:             | How many results to skip       |
| `status`                       | *?string*                      | :heavy_minus_sign:             | Filter by item status          |

### Response

**[?Operations\ListMassPaymentItemsResponse](../../Models/Operations/ListMassPaymentItemsResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Errors\ListMassPaymentItemsForbiddenDwollaV1HalJSONException | 403                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\ListMassPaymentItemsNotFoundDwollaV1HalJSONException  | 404                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\APIException                                          | 4XX, 5XX                                                     | \*/\*                                                        |

## get

Retrieve detailed information for a specific mass payment item by its unique identifier. Returns item status, amount, metadata, and links to the parent mass payment, associated transfer, and destination funding source. Use this endpoint to check the processing status and details of an individual item within a mass payment batch.

### Example Usage

<!-- UsageSnippet language="php" operationID="getMassPaymentItem" method="get" path="/mass-payment-items/{itemId}" -->
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



$response = $sdk->massPayments->items->get(
    itemId: '<id>'
);

if ($response->massPaymentItem !== null) {
    // handle response
}
```

### Parameters

| Parameter                                  | Type                                       | Required                                   | Description                                |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| `itemId`                                   | *string*                                   | :heavy_check_mark:                         | ID of item to be retrieved in mass payment |

### Response

**[?Operations\GetMassPaymentItemResponse](../../Models/Operations/GetMassPaymentItemResponse.md)**

### Errors

| Error Type                                                 | Status Code                                                | Content Type                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| Errors\GetMassPaymentItemForbiddenDwollaV1HalJSONException | 403                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\GetMassPaymentItemNotFoundDwollaV1HalJSONException  | 404                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\APIException                                        | 4XX, 5XX                                                   | \*/\*                                                      |