# Accounts.FundingSources

## Overview

### Available Operations

* [create](#create) - Create a funding source for an account
* [list](#list) - List funding sources for an account

## create

Create a funding source by adding a bank account to a Main Dwolla Account. This endpoint allows you to connect a checking or savings account using either manual bank account details or an exchange resource.

For more information about funding sources, see the [Funding Sources API Reference](https://developers.dwolla.com/docs/api-reference/funding-sources).


### Example Usage

<!-- UsageSnippet language="php" operationID="createFundingSource" method="post" path="/funding-sources" -->
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

$request = new Components\CreateAccountFundingSource(
    name: '<value>',
    bankAccountType: Components\CreateAccountFundingSourceBankAccountType::Checking,
    accountNumber: '<value>',
    routingNumber: '<value>',
);

$response = $sdk->accounts->fundingSources->create(
    request: $request
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                      | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `$request`                                                                                     | [Components\CreateAccountFundingSource](../../Models/Components/CreateAccountFundingSource.md) | :heavy_check_mark:                                                                             | The request object to use for the request.                                                     |

### Response

**[?Operations\CreateFundingSourceResponse](../../Models/Operations/CreateFundingSourceResponse.md)**

### Errors

| Error Type                                         | Status Code                                        | Content Type                                       |
| -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| Errors\BadRequestSchemaException                   | 400                                                | application/vnd.dwolla.v1.hal+json                 |
| Errors\DuplicateResourceSchemaException            | 400                                                | application/vnd.dwolla.v1.hal+json                 |
| Errors\CreateFundingSourceDwollaV1HalJSONException | 403                                                | application/vnd.dwolla.v1.hal+json                 |
| Errors\APIException                                | 4XX, 5XX                                           | \*/\*                                              |

## list

Get a list of all funding sources associated with a specific Main Dwolla Account. This endpoint returns both bank accounts and balance funding sources, with detailed information about each funding source's status, type, and available processing channels.


### Example Usage

<!-- UsageSnippet language="php" operationID="listFundingSources" method="get" path="/accounts/{id}/funding-sources" -->
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



$response = $sdk->accounts->fundingSources->list(
    id: '<id>'
);

if ($response->fundingSources !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                         | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `id`                                                              | *string*                                                          | :heavy_check_mark:                                                | Account's unique identifier                                       |
| `removed`                                                         | *?string*                                                         | :heavy_minus_sign:                                                | Filter removed funding sources. Boolean value. Defaults to `true` |

### Response

**[?Operations\ListFundingSourcesResponse](../../Models/Operations/ListFundingSourcesResponse.md)**

### Errors

| Error Type                                                 | Status Code                                                | Content Type                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| Errors\ListFundingSourcesForbiddenDwollaV1HalJSONException | 403                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\ListFundingSourcesNotFoundDwollaV1HalJSONException  | 404                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\APIException                                        | 4XX, 5XX                                                   | \*/\*                                                      |