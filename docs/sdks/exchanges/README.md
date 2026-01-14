# Exchanges

## Overview

Operations related to Exchanges

### Available Operations

* [get](#get) - Retrieve exchange resource

## get

Returns details for a specific exchange connection between Dwolla and an open banking partner for a customer's bank account. Includes exchange status, creation date, and links to the associated customer and exchange partner.

### Example Usage

<!-- UsageSnippet language="php" operationID="getExchange" method="get" path="/exchanges/{id}" -->
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



$response = $sdk->exchanges->get(
    id: 'e5e9f2d3-a96c-4abd-a097-8ec7ae28aa8a'
);

if ($response->exchange !== null) {
    // handle response
}
```

### Parameters

| Parameter                            | Type                                 | Required                             | Description                          | Example                              |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `id`                                 | *string*                             | :heavy_check_mark:                   | Exchange resource unique identifier. | e5e9f2d3-a96c-4abd-a097-8ec7ae28aa8a |

### Response

**[?Operations\GetExchangeResponse](../../Models/Operations/GetExchangeResponse.md)**

### Errors

| Error Type                                             | Status Code                                            | Content Type                                           |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Errors\GetExchangeUnauthorizedDwollaV1HalJSONException | 401                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\GetExchangeNotFoundDwollaV1HalJSONException     | 404                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\APIException                                    | 4XX, 5XX                                               | \*/\*                                                  |