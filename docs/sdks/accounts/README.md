# Accounts

## Overview

Operations related to Accounts

### Available Operations

* [get](#get) - Retrieve account details

## get

Returns basic account information for your authorized Main Dwolla Account, including account ID, name, and links to related resources such as funding sources, transfers, and customers.

### Example Usage

<!-- UsageSnippet language="php" operationID="getAccount" method="get" path="/accounts/{id}" -->
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



$response = $sdk->accounts->get(
    id: '<id>'
);

if ($response->account !== null) {
    // handle response
}
```

### Parameters

| Parameter                   | Type                        | Required                    | Description                 |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- |
| `id`                        | *string*                    | :heavy_check_mark:          | Account's unique identifier |

### Response

**[?Operations\GetAccountResponse](../../Models/Operations/GetAccountResponse.md)**

### Errors

| Error Type                                | Status Code                               | Content Type                              |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| Errors\GetAccountDwollaV1HalJSONException | 403                                       | application/vnd.dwolla.v1.hal+json        |
| Errors\NotFoundError                      | 404                                       | application/vnd.dwolla.v1.hal+json        |
| Errors\APIException                       | 4XX, 5XX                                  | \*/\*                                     |