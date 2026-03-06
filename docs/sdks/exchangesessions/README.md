# ExchangeSessions

## Overview

### Available Operations

* [get](#get) - Retrieve exchange session

## get

Returns details of a previously created exchange session. Response varies by partner:
- **MX**: `_links.external-provider-session.href` (redirect URL for verification).
- **Plaid**: `externalProviderSessionToken` (token to initialize Plaid Link).
- **Checkout.com**: `externalProviderSessionData` with `id`, `payment_session_secret`, and `payment_session_token` to initialize the Checkout.com Flow component for debit card capture (Push to Card).


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