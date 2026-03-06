# Customers.FundingSources

## Overview

### Available Operations

* [list](#list) - List customer funding sources
* [create](#create) - Create customer funding source

## list

Returns all funding sources for a customer, including bank accounts, debit card funding sources, and Dwolla balance (verified customers only). Shows verification status, limited account details, and creation dates. Card funding sources include masked card information. Supports filtering to exclude removed funding sources using the removed parameter.

### Example Usage

<!-- UsageSnippet language="php" operationID="listCustomerFundingSources" method="get" path="/customers/{id}/funding-sources" -->
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



$response = $sdk->customers->fundingSources->list(
    id: '<id>'
);

if ($response->fundingSources !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                         | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `id`                                                              | *string*                                                          | :heavy_check_mark:                                                | Customer's unique identifier                                      |
| `removed`                                                         | *?string*                                                         | :heavy_minus_sign:                                                | Filter removed funding sources. Boolean value. Defaults to `true` |

### Response

**[?Operations\ListCustomerFundingSourcesResponse](../../Models/Operations/ListCustomerFundingSourcesResponse.md)**

### Errors

| Error Type                                                         | Status Code                                                        | Content Type                                                       |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| Errors\ListCustomerFundingSourcesForbiddenDwollaV1HalJSONException | 403                                                                | application/vnd.dwolla.v1.hal+json                                 |
| Errors\ListCustomerFundingSourcesNotFoundDwollaV1HalJSONException  | 404                                                                | application/vnd.dwolla.v1.hal+json                                 |
| Errors\APIException                                                | 4XX, 5XX                                                           | \*/\*                                                              |

## create

Creates a bank account or debit card funding source for a customer. Supports multiple methods including manual entry with routing/account numbers, instant verification using existing open banking connections, debit card addition via Exchange, and virtual account numbers. Bank funding sources require verification before transfers can be initiated.

### Example Usage

<!-- UsageSnippet language="php" operationID="createCustomerFundingSource" method="post" path="/customers/{id}/funding-sources" -->
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



$response = $sdk->customers->fundingSources->create(
    id: '<id>',
    body: new Components\CreateCustomerExchangeFundingSource(
        links: new Components\CreateCustomerExchangeFundingSourceLinks(
            exchange: new Components\CreateCustomerExchangeFundingSourceExchange(
                href: 'https://api-sandbox.dwolla.com/exchanges/6bc9109a-04fd-49b6-ace6-ca06fd282d65',
            ),
            onDemandAuthorization: new Components\CreateCustomerExchangeFundingSourceOnDemandAuthorization(
                href: 'https://api-sandbox.dwolla.com/on-demand-authorizations/30e7c028-0bdf-e511-80de-0aa34a9b2388',
            ),
        ),
        bankAccountType: Components\CreateCustomerExchangeFundingSourceBankAccountType::Checking,
        name: 'Jane Doe\'s Checking',
    )

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                                                                                                  | *string*                                                                                                                                                                                                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                    | Customer's unique identifier                                                                                                                                                                                                                                                                                                          |
| `body`                                                                                                                                                                                                                                                                                                                                | [Components\CreateCustomerBankFundingSourceWithAccountNumbers\|Components\CreateCustomerBankFundingSourceWithPlaid\|Components\CreateCustomerExchangeFundingSource\|Components\CreateCustomerVirtualAccountFundingSource\|Components\CreateCustomerCardFundingSourceWithExchange](../../Models/Components/CreateCustomerFundingSource.md) | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                    | Parameters for creating a funding source                                                                                                                                                                                                                                                                                              |

### Response

**[?Operations\CreateCustomerFundingSourceResponse](../../Models/Operations/CreateCustomerFundingSourceResponse.md)**

### Errors

| Error Type                                                          | Status Code                                                         | Content Type                                                        |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Errors\InactiveExchangeError                                        | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\InvalidExchangeTokenError                                    | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\DuplicateFundingSourceError                                  | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\UnsupportedCardCountryError                                  | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\InvalidTokenError                                            | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\MaximumCardsExceededError                                    | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\CardMissingRequiredFieldsError                               | 400                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\CreateCustomerFundingSourceForbiddenDwollaV1HalJSONException | 403                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\CreateCustomerFundingSourceNotFoundDwollaV1HalJSONException  | 404                                                                 | application/vnd.dwolla.v1.hal+json                                  |
| Errors\APIException                                                 | 4XX, 5XX                                                            | \*/\*                                                               |