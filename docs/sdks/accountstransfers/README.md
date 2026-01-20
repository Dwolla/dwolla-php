# Accounts.Transfers

## Overview

### Available Operations

* [list](#list) - List and search account transfers

## list

Returns a paginated, searchable list of transfers associated with the specified Main Dwolla account. Supports advanced filtering by amount range, date range, transfer status, and correlation ID. Results are limited to 10,000 transfers per query; use date range filters for historical data beyond this limit.

### Example Usage

<!-- UsageSnippet language="php" operationID="listAndSearchTransfers" method="get" path="/accounts/{id}/transfers" -->
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

$request = new Operations\ListAndSearchTransfersRequest(
    id: '<id>',
);

$response = $sdk->accounts->transfers->list(
    request: $request
);

if ($response->transfers !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `$request`                                                                                           | [Operations\ListAndSearchTransfersRequest](../../Models/Operations/ListAndSearchTransfersRequest.md) | :heavy_check_mark:                                                                                   | The request object to use for the request.                                                           |

### Response

**[?Operations\ListAndSearchTransfersResponse](../../Models/Operations/ListAndSearchTransfersResponse.md)**

### Errors

| Error Type                                            | Status Code                                           | Content Type                                          |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| Errors\ListAndSearchTransfersDwollaV1HalJSONException | 404                                                   | application/vnd.dwolla.v1.hal+json                    |
| Errors\APIException                                   | 4XX, 5XX                                              | \*/\*                                                 |