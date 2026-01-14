# Customers.Labels

## Overview

### Available Operations

* [list](#list) - List labels for a customer
* [create](#create) - Create a label for a customer

## list

Returns all labels for a specified Verified Customer, sorted by creation date (most recent first). Supports pagination with limit and offset parameters. Each label includes its current amount and creation timestamp.

### Example Usage

<!-- UsageSnippet language="php" operationID="listCustomerLabels" method="get" path="/customers/{id}/labels" -->
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



$response = $sdk->customers->labels->list(
    id: '<id>'
);

if ($response->labels !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | ID of customer             |
| `limit`                    | *?string*                  | :heavy_minus_sign:         | How many results to return |
| `offset`                   | *?string*                  | :heavy_minus_sign:         | How many results to skip   |

### Response

**[?Operations\ListCustomerLabelsResponse](../../Models/Operations/ListCustomerLabelsResponse.md)**

### Errors

| Error Type                                                 | Status Code                                                | Content Type                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| Errors\ListCustomerLabelsForbiddenDwollaV1HalJSONException | 403                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\ListCustomerLabelsNotFoundDwollaV1HalJSONException  | 404                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\APIException                                        | 4XX, 5XX                                                   | \*/\*                                                      |

## create

Creates a new label for a Verified Customer with a specified amount. Labels help organize and track funds within a customer's balance. Returns the location of the created label resource in the response header.

### Example Usage

<!-- UsageSnippet language="php" operationID="createCustomerLabel" method="post" path="/customers/{id}/labels" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();

$body = new Operations\CreateCustomerLabelRequestBody(
    amount: new Operations\CreateCustomerLabelAmount(
        currency: 'USD',
        value: '12.34',
    ),
);

$response = $sdk->customers->labels->create(
    id: '<id>',
    body: $body

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                              | Type                                                                                                   | Required                                                                                               | Description                                                                                            |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                   | *string*                                                                                               | :heavy_check_mark:                                                                                     | ID of customer to create a label for                                                                   |
| `body`                                                                                                 | [Operations\CreateCustomerLabelRequestBody](../../Models/Operations/CreateCustomerLabelRequestBody.md) | :heavy_check_mark:                                                                                     | Parameters to create a customer label                                                                  |

### Response

**[?Operations\CreateCustomerLabelResponse](../../Models/Operations/CreateCustomerLabelResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| Errors\BadRequestError                                      | 400                                                         | application/vnd.dwolla.v1.hal+json                          |
| Errors\CreateCustomerLabelForbiddenDwollaV1HalJSONException | 403                                                         | application/vnd.dwolla.v1.hal+json                          |
| Errors\CreateCustomerLabelNotFoundDwollaV1HalJSONException  | 404                                                         | application/vnd.dwolla.v1.hal+json                          |
| Errors\APIException                                         | 4XX, 5XX                                                    | \*/\*                                                       |