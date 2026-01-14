# Accounts.Exchanges

## Overview

### Available Operations

* [list](#list) - List exchanges for an account
* [create](#create) - Create an exchange for an account

## list

Returns all exchanges for your Dwolla account. Exchanges represent connections between external bank accounts and your account through open banking partners. Includes exchange status, creation date, and associated partner information.

### Example Usage

<!-- UsageSnippet language="php" operationID="listAccountExchanges" method="get" path="/exchanges" -->
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



$response = $sdk->accounts->exchanges->list(

);

if ($response->exchanges !== null) {
    // handle response
}
```

### Response

**[?Operations\ListAccountExchangesResponse](../../Models/Operations/ListAccountExchangesResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## create

Create an exchange for an account. The request body will vary based on the exchange partner.
For Finicity, the request body will include finicity-specific fields.
For MX Secure Exchange, the request body will include a token.
For Flinks Secure Exchange, the request body will include a token.
For Plaid Secure Exchange, the request body will include a token.


### Example Usage

<!-- UsageSnippet language="php" operationID="createAccountExchange" method="post" path="/exchanges" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Brick\DateTime\LocalDate;
use Dwolla;
use Dwolla\Models\Components;
use Dwolla\Utils;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();

$request = new Components\CreateFinicitySecureExchange(
    links: new Components\CreateFinicitySecureExchangeLinks(
        exchangePartner: new Components\CreateFinicitySecureExchangeExchangePartner(
            href: 'https://api.dwolla.com/exchange-partners/292317ec-e252-47d8-93c3-2d128e037aa4',
        ),
    ),
    finicity: new Components\Finicity(
        profile: 3,
        version: '1',
        receiptId: 'cr_4N47ou7SlppuIxq0ZUtACh10vYcloY',
        receiptVersion: '1',
        customerId: '5454874858510164117',
        partnerId: 2445583946651,
        products: [
            new Components\Product(
                product: 'moneyTransferDetails',
                accountId: '1015199035827334916',
                accessPeriod: new Components\AccessPeriod(
                    type: 'timeframe',
                    startTime: LocalDate::parse('2022-07-06'),
                    endTime: Utils\Utils::parseDateTime('2022-08-16T06:06:20Z'),
                ),
            ),
        ],
        timestamp: Utils\Utils::parseDateTime('2022-07-11T06:06:23Z'),
    ),
);

$response = $sdk->accounts->exchanges->create(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                              | Type                                                                                                                                   | Required                                                                                                                               | Description                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `$request`                                                                                                                             | [Components\CreateFinicitySecureExchange\|Components\CreateTokenBasedExchange](../../Models/Operations/CreateAccountExchangeRequest.md) | :heavy_check_mark:                                                                                                                     | The request object to use for the request.                                                                                             |

### Response

**[?Operations\CreateAccountExchangeResponse](../../Models/Operations/CreateAccountExchangeResponse.md)**

### Errors

| Error Type                                           | Status Code                                          | Content Type                                         |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| Errors\InvalidExchangeTokenException                 | 400                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\InvalidExchangeException                      | 400                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\CreateAccountExchangeDwollaV1HalJSONException | 401                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\ForbiddenError                                | 403                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\NotFoundError                                 | 404                                                  | application/vnd.dwolla.v1.hal+json                   |
| Errors\APIException                                  | 4XX, 5XX                                             | \*/\*                                                |