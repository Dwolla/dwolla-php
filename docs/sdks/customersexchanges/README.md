# Customers.Exchanges

## Overview

### Available Operations

* [list](#list) - List exchanges for a customer
* [create](#create) - Create an exchange for a customer

## list

Returns all exchanges for a specific customer. Exchanges represent connections between the customer's external bank accounts and open banking partners. Includes exchange status, creation date, and links to associated funding sources and partners.

### Example Usage

<!-- UsageSnippet language="php" operationID="listCustomerExchanges" method="get" path="/customers/{id}/exchanges" -->
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



$response = $sdk->customers->exchanges->list(
    id: '<id>'
);

if ($response->exchanges !== null) {
    // handle response
}
```

### Parameters

| Parameter                                    | Type                                         | Required                                     | Description                                  |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| `id`                                         | *string*                                     | :heavy_check_mark:                           | The ID of the Customer to list exchanges for |

### Response

**[?Operations\ListCustomerExchangesResponse](../../Models/Operations/ListCustomerExchangesResponse.md)**

### Errors

| Error Type                                           | Status Code                                          | Content Type                                         |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| Errors\ListCustomerExchangesDwollaV1HalJSONException | 404                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\APIException                                  | 4XX, 5XX                                             | \*/\*                                                |

## create

Creates an exchange connection between a customer's external bank account and Dwolla through open banking partners. Acts as the handshake that establishes secure access to the customer's bank account data. Request body varies by partner (Plaid, MX, Flinks, Finicity).

### Example Usage

<!-- UsageSnippet language="php" operationID="createCustomerExchange" method="post" path="/customers/{id}/exchanges" -->
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



$response = $sdk->customers->exchanges->create(
    id: '<id>',
    body: new Components\CreatePlaidOpenBankingExchange(
        links: new Components\CreatePlaidOpenBankingExchangeLinks(
            exchangePartner: new Components\CreatePlaidOpenBankingExchangeExchangePartner(
                href: 'https://api.dwolla.com/exchange-partners/f53ffb32-c84f-496a-9d9d-acd100d396ef',
            ),
        ),
        plaid: new Components\Plaid(
            publicToken: 'public-production-d5456acb-01d5-4932-9783-e4c883cf1c0c',
        ),
    )

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                         | *string*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The ID of the customer to create an exchange for                                                                                                                                                                             |
| `body`                                                                                                                                                                                                                       | [Components\CreateFinicitySecureExchange\|Components\CreateTokenBasedExchange\|Components\CreateMXOpenBankingExchange\|Components\CreatePlaidOpenBankingExchange](../../Models/Operations/CreateCustomerExchangeRequestBody.md) | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[?Operations\CreateCustomerExchangeResponse](../../Models/Operations/CreateCustomerExchangeResponse.md)**

### Errors

| Error Type                                          | Status Code                                         | Content Type                                        |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| Errors\InvalidExchangeTokenException                | 400                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\InvalidExchangeException                     | 400                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\CreateCustomerExchangeResponseBodyException1 | 401                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\CreateCustomerExchangeResponseBodyException2 | 401                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\NotFoundError                                | 404                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\APIException                                 | 4XX, 5XX                                            | \*/\*                                               |