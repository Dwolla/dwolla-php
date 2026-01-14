# Customers.MassPayments

## Overview

### Available Operations

* [list](#list) - List mass payments for customer

## list

Retrieve all previously created mass payments for a Verified Customer account with optional correlation ID filtering and pagination support. Mass payments are returned ordered by date created with most recent appearing first. Returns paginated results including mass payment status, metadata, source funding information, and item links. Supports standard pagination parameters and correlation ID search for enhanced traceability.

### Example Usage

<!-- UsageSnippet language="php" operationID="listCustomerMassPayments" method="get" path="/customers/{id}/mass-payments" -->
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



$response = $sdk->customers->massPayments->list(
    id: '<id>'
);

if ($response->massPayments !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                      | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `id`                                                                           | *string*                                                                       | :heavy_check_mark:                                                             | Customer ID to get mass payments for                                           |
| `correlationId`                                                                | *?string*                                                                      | :heavy_minus_sign:                                                             | A string value to search on if `correlationId` was specified for a transaction |
| `limit`                                                                        | *?int*                                                                         | :heavy_minus_sign:                                                             | Number of search results to return. Defaults to 25                             |
| `offset`                                                                       | *?int*                                                                         | :heavy_minus_sign:                                                             | Number of search results to skip. Use for pagination                           |

### Response

**[?Operations\ListCustomerMassPaymentsResponse](../../Models/Operations/ListCustomerMassPaymentsResponse.md)**

### Errors

| Error Type                                                       | Status Code                                                      | Content Type                                                     |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| Errors\ListCustomerMassPaymentsForbiddenDwollaV1HalJSONException | 403                                                              | application/vnd.dwolla.v1.hal+json                               |
| Errors\ListCustomerMassPaymentsNotFoundDwollaV1HalJSONException  | 404                                                              | application/vnd.dwolla.v1.hal+json                               |
| Errors\APIException                                              | 4XX, 5XX                                                         | \*/\*                                                            |