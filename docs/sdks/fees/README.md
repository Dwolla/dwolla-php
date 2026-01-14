# Transfers.Fees

## Overview

### Available Operations

* [list](#list) - List fees for a transfer

## list

Retrieve detailed fee information for a specific transfer by its unique identifier. Returns the total number of fees and individual fee transaction details including amounts, status, and links to source and destination accounts.

### Example Usage

<!-- UsageSnippet language="php" operationID="listTransferFees" method="get" path="/transfers/{id}/fees" -->
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



$response = $sdk->transfers->fees->list(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                           | Type                                | Required                            | Description                         |
| ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- |
| `id`                                | *string*                            | :heavy_check_mark:                  | ID of transfer to retrieve fees for |

### Response

**[?Operations\ListTransferFeesResponse](../../Models/Operations/ListTransferFeesResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |