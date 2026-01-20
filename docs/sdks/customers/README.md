# Customers

## Overview

Operations related to Customers

### Available Operations

* [list](#list) - List and search customers
* [create](#create) - Create a customer
* [get](#get) - Retrieve a customer
* [update](#update) - Update a customer
* [listAvailableConnections](#listavailableconnections) - List available exchange connections

## list

Returns a paginated list of customers sorted by creation date. Supports fuzzy search across customer names, business names, and email addresses, plus exact filtering by email and verification status. Default limit is 25 customers per page, maximum 200.

### Example Usage

<!-- UsageSnippet language="php" operationID="listAndSearchCustomers" method="get" path="/customers" -->
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



$response = $sdk->customers->list(

);

if ($response->customers !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `limit`                    | *?int*                     | :heavy_minus_sign:         | How many results to return |
| `offset`                   | *?int*                     | :heavy_minus_sign:         | How many results to skip   |
| `search`                   | *?string*                  | :heavy_minus_sign:         | Searches on certain fields |
| `status`                   | *?string*                  | :heavy_minus_sign:         | Filter by customer status  |

### Response

**[?Operations\ListAndSearchCustomersResponse](../../Models/Operations/ListAndSearchCustomersResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## create

Creates a new customer with different verification levels and capabilities. Supports personal verified customers (individuals), business verified customers (businesses), unverified customers, and receive-only users. Customer type determines transaction limits, verification requirements, and available features.

### Example Usage

<!-- UsageSnippet language="php" operationID="createCustomer" method="post" path="/customers" -->
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

$request = new Components\CreateReceiveOnlyUser(
    firstName: 'Account',
    lastName: 'Admin',
    email: 'accountAdmin@email.com',
    ipAddress: '143.156.7.8',
    phone: '5555555555',
    correlationId: 'fc451a7a-ae30-4404-aB95-e3553fcd733',
    businessName: 'Jane Corp llc',
);

$response = $sdk->customers->create(
    request: $request
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                 | Type                                                                                                                                                                                                                                                                                                                                      | Required                                                                                                                                                                                                                                                                                                                                  | Description                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$request`                                                                                                                                                                                                                                                                                                                                | [Components\CreateReceiveOnlyUser\|Components\CreateUnverifiedCustomer\|Components\CreateVerifiedPersonalCustomer\|Components\CreateVerifiedSolePropCustomer\|Components\CreateVerifiedBusinessCustomerWithController\|Components\CreateVerifiedBusinessCustomerWithInternationalController](../../Models/Operations/CreateCustomerRequest.md) | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                        | The request object to use for the request.                                                                                                                                                                                                                                                                                                |

### Response

**[?Operations\CreateCustomerResponse](../../Models/Operations/CreateCustomerResponse.md)**

### Errors

| Error Type                                             | Status Code                                            | Content Type                                           |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Errors\BadRequestError                                 | 400                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\CreateCustomerForbiddenDwollaV1HalJSONException | 403                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\CreateCustomerNotFoundDwollaV1HalJSONException  | 404                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\APIException                                    | 4XX, 5XX                                               | \*/\*                                                  |

## get

Retrieve identifying information for a specific customer. The returned data varies by customer type - verified customers include contact details, address information, and verification status, while unverified customers and receive-only users contain basic contact information only.

### Example Usage

<!-- UsageSnippet language="php" operationID="getCustomer" method="get" path="/customers/{id}" -->
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



$response = $sdk->customers->get(
    id: '<id>'
);

if ($response->oneOf !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | Customer unique identifier |

### Response

**[?Operations\GetCustomerResponse](../../Models/Operations/GetCustomerResponse.md)**

### Errors

| Error Type                                          | Status Code                                         | Content Type                                        |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| Errors\GetCustomerForbiddenDwollaV1HalJSONException | 403                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\GetCustomerNotFoundDwollaV1HalJSONException  | 404                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\APIException                                 | 4XX, 5XX                                            | \*/\*                                               |

## update

Update Customer information, upgrade an unverified Customer to a verified Customer, suspend a Customer, deactivate a Customer, reactivate a Customer, and update a verified Customer's information to retry verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="update" method="post" path="/customers/{id}" -->
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



$response = $sdk->customers->update(
    id: '<id>',
    body: [
        'firstName' => 'Account',
        'lastName' => 'Admin',
        'email' => 'accountAdmin@email.com',
        'ipAddress' => '143.156.7.8',
        'type' => 'business',
        'address1' => '99-99 33rd St',
        'city' => 'Some City',
        'state' => 'NY',
        'postalCode' => '11101',
        'controller' => [
            'firstName' => 'John',
            'lastName' => 'Controller',
            'title' => 'CEO',
            'ssn' => '6789',
            'dateOfBirth' => '1980-01-31',
            'address' => [
                'address1' => '1749 18th st',
                'address2' => 'apt 12',
                'city' => 'Des Moines',
                'stateProvinceRegion' => 'IA',
                'postalCode' => '50266',
                'country' => 'US',
            ],
        ],
        'businessClassification' => '9ed3f670-7d6f-11e3-b1ce-5404a6144203',
        'businessType' => 'llc',
        'businessName' => 'Jane Corp',
        'ein' => '00-0000000',
    ]

);

if ($response->oneOf !== null) {
    // handle response
}
```

### Parameters

| Parameter                          | Type                               | Required                           | Description                        |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `id`                               | *string*                           | :heavy_check_mark:                 | Customer unique identifier         |
| `body`                             | *mixed*                            | :heavy_check_mark:                 | Parameters for updating a Customer |

### Response

**[?Operations\UpdateResponse](../../Models/Operations/UpdateResponse.md)**

### Errors

| Error Type                                      | Status Code                                     | Content Type                                    |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| Errors\UpdateBadRequestDwollaV1HalJSONException | 400                                             | application/vnd.dwolla.v1.hal+json              |
| Errors\UpdateForbiddenDwollaV1HalJSONException  | 403                                             | application/vnd.dwolla.v1.hal+json              |
| Errors\APIException                             | 4XX, 5XX                                        | \*/\*                                           |

## listAvailableConnections

Returns available exchange connections for a customer's bank accounts authorized through MX Connect. Each connection includes an account name and availableConnectionToken required to create exchanges and funding sources for transfers.

### Example Usage

<!-- UsageSnippet language="php" operationID="listAvailableExchangeConnections" method="get" path="/customers/{id}/available-exchange-connections" -->
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



$response = $sdk->customers->listAvailableConnections(
    id: '<id>'
);

if ($response->availableExchangeConnections !== null) {
    // handle response
}
```

### Parameters

| Parameter                    | Type                         | Required                     | Description                  |
| ---------------------------- | ---------------------------- | ---------------------------- | ---------------------------- |
| `id`                         | *string*                     | :heavy_check_mark:           | Customer's unique identifier |

### Response

**[?Operations\ListAvailableExchangeConnectionsResponse](../../Models/Operations/ListAvailableExchangeConnectionsResponse.md)**

### Errors

| Error Type                                                      | Status Code                                                     | Content Type                                                    |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| Errors\ListAvailableExchangeConnectionsDwollaV1HalJSONException | 404                                                             | application/vnd.dwolla.v1.hal+json                              |
| Errors\APIException                                             | 4XX, 5XX                                                        | \*/\*                                                           |