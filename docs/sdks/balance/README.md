# FundingSources.Balance

## Overview

### Available Operations

* [get](#get) - Retrieve funding source balance

## get

Returns the current balance for a specific funding source. For bank accounts, includes available and closing balances; for Dwolla balance, includes balance and total amounts; for settlement accounts (bankUsageType = card-network), includes available balance only. Supports bank accounts (via Open Banking), Dwolla balance (verified customers only), and settlement accounts for card network processing.

### Example Usage

<!-- UsageSnippet language="php" operationID="getFundingSourceBalance" method="get" path="/funding-sources/{id}/balance" -->
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



$response = $sdk->fundingSources->balance->get(
    id: '<id>'
);

if ($response->oneOf !== null) {
    // handle response
}
```

### Parameters

| Parameter                                        | Type                                             | Required                                         | Description                                      |
| ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ |
| `id`                                             | *string*                                         | :heavy_check_mark:                               | ID of funding source to retrieve the balance for |

### Response

**[?Operations\GetFundingSourceBalanceResponse](../../Models/Operations/GetFundingSourceBalanceResponse.md)**

### Errors

| Error Type                                             | Status Code                                            | Content Type                                           |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Errors\GetFundingSourceBalanceDwollaV1HalJSONException | 404                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\APIException                                    | 4XX, 5XX                                               | \*/\*                                                  |