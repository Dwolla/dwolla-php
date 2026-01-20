# ExchangeSessions

## Overview

### Available Operations

* [get](#get) - Retrieve exchange session

## get

Returns details of a previously created exchange session, including URLs and tokens needed to continue the instant account verification flow. Response varies by partner - MX provides redirect URLs while Plaid provides session tokens for Link initialization.

### Example Usage

<!-- UsageSnippet language="php" operationID="retrieveCustomerExchangeSession" method="get" path="/exchange-sessions/{id}" -->
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



$response = $sdk->exchangeSessions->get(
    id: '<id>'
);

if ($response->exchangeSession !== null) {
    // handle response
}
```

### Parameters

| Parameter                            | Type                                 | Required                             | Description                          |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `id`                                 | *string*                             | :heavy_check_mark:                   | Exchange session's unique identifier |

### Response

**[?Operations\RetrieveCustomerExchangeSessionResponse](../../Models/Operations/RetrieveCustomerExchangeSessionResponse.md)**

### Errors

| Error Type                                                              | Status Code                                                             | Content Type                                                            |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Errors\RetrieveCustomerExchangeSessionForbiddenDwollaV1HalJSONException | 403                                                                     | application/vnd.dwolla.v1.hal+json                                      |
| Errors\RetrieveCustomerExchangeSessionNotFoundDwollaV1HalJSONException  | 404                                                                     | application/vnd.dwolla.v1.hal+json                                      |
| Errors\APIException                                                     | 4XX, 5XX                                                                | \*/\*                                                                   |