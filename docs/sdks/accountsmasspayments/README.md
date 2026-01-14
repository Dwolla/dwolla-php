# Accounts.MassPayments

## Overview

### Available Operations

* [list](#list) - List account mass payments

## list

Returns a paginated list of mass payments created by your Main Dwolla account. Results are sorted by creation date in descending order (newest first) and can be filtered by correlation ID.

### Example Usage

<!-- UsageSnippet language="php" operationID="listMassPayments" method="get" path="/accounts/{id}/mass-payments" -->
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



$response = $sdk->accounts->massPayments->list(
    id: '<id>',
    limit: 25,
    offset: 0

);

if ($response->massPayments !== null) {
    // handle response
}
```

### Parameters

| Parameter                           | Type                                | Required                            | Description                         | Example                             |
| ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- |
| `id`                                | *string*                            | :heavy_check_mark:                  | Account's unique identifier         |                                     |
| `limit`                             | *?int*                              | :heavy_minus_sign:                  | Maximum number of results to return | 25                                  |
| `offset`                            | *?int*                              | :heavy_minus_sign:                  | How many results to skip.           | 0                                   |
| `correlationId`                     | *?string*                           | :heavy_minus_sign:                  | Correlation ID to search by.        |                                     |

### Response

**[?Operations\ListMassPaymentsResponse](../../Models/Operations/ListMassPaymentsResponse.md)**

### Errors

| Error Type                                               | Status Code                                              | Content Type                                             |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| Errors\ListMassPaymentsForbiddenDwollaV1HalJSONException | 403                                                      | application/vnd.dwolla.v1.hal+json                       |
| Errors\ListMassPaymentsNotFoundDwollaV1HalJSONException  | 404                                                      | application/vnd.dwolla.v1.hal+json                       |
| Errors\APIException                                      | 4XX, 5XX                                                 | \*/\*                                                    |