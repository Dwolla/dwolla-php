# Customers.ExchangeSessions

## Overview

### Available Operations

* [create](#create) - Create customer exchange session

## create

Creates an exchange session for a customer. Use cases include:
- **Plaid / MX**: Instant bank account verification (open banking). For faster verification as compared to traditional micro-deposits.
- **Checkout.com**: Debit card capture for Push to Card. Create a session, then retrieve it to get `externalProviderSessionData` (payment session) for the Checkout.com Flow component.


### Example Usage

<!-- UsageSnippet language="php" operationID="createCustomerExchangeSession" method="post" path="/customers/{id}/exchange-sessions" -->
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



$response = $sdk->customers->exchangeSessions->create(
    id: '<id>',
    body: new Components\CreateCustomerExchangeSessionWithRedirect(
        links: new Components\CreateCustomerExchangeSessionWithRedirectLinks(
            exchangePartner: new Components\CreateCustomerExchangeSessionWithRedirectExchangePartner(
                href: 'https://api.dwolla.com/exchange-partners/292317ec-e252-47d8-93c3-2d128e037aa4',
            ),
            redirectUrl: new Components\CreateCustomerExchangeSessionWithRedirectRedirectUrl(
                href: 'https://example.com/app123',
            ),
        ),
    )

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                  | Type                                                                                                                                                                       | Required                                                                                                                                                                   | Description                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                       | *string*                                                                                                                                                                   | :heavy_check_mark:                                                                                                                                                         | Customer's unique identifier                                                                                                                                               |
| `body`                                                                                                                                                                     | [Components\CreateCustomerExchangeSessionWithRedirect\|Components\CreateCustomerExchangeSessionForWeb](../../Models/Operations/CreateCustomerExchangeSessionRequestBody.md) | :heavy_check_mark:                                                                                                                                                         | Parameters for creating an exchange session                                                                                                                                |

### Response

**[?Operations\CreateCustomerExchangeSessionResponse](../../Models/Operations/CreateCustomerExchangeSessionResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Errors\ResponseBodyBadRequestException1                      | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\ResponseBodyBadRequestException2                      | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\ResponseBodyBadRequestException3                      | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\CreateCustomerExchangeSessionDwollaV1HalJSONException | 401                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\ResponseBodyForbiddenException1                       | 403                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\ResponseBodyForbiddenException2                       | 403                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\NotFoundError                                         | 404                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\APIException                                          | 4XX, 5XX                                                     | \*/\*                                                        |