# Labels.Reallocations

## Overview

### Available Operations

* [create](#create) - Create a label reallocation
* [get](#get) - Retrieve a label reallocation

## create

Reallocates funds between two labels belonging to the same Verified Customer. Moves the specified amount from the source label to the destination label, creating ledger entries for both. The reallocation only succeeds if the source label has sufficient funds.

### Example Usage

<!-- UsageSnippet language="php" operationID="createLabelReallocation" method="post" path="/label-reallocations" -->
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

$request = new Operations\CreateLabelReallocationRequest(
    links: new Operations\CreateLabelReallocationLinks(
        from: new Operations\FromT(
            href: 'https://api.dwolla.com/labels/c91c501c-f49b-48be-a93b-12b45e152d45',
        ),
        to: new Operations\To(
            href: 'https://api.dwolla.com/labels/7e042ffe-e25e-40d2-b86e-748b98845ecc',
        ),
    ),
    amount: new Operations\CreateLabelReallocationAmount(
        currency: 'USD',
        value: '15.00',
    ),
);

$response = $sdk->labels->reallocations->create(
    request: $request
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                              | Type                                                                                                   | Required                                                                                               | Description                                                                                            |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `$request`                                                                                             | [Operations\CreateLabelReallocationRequest](../../Models/Operations/CreateLabelReallocationRequest.md) | :heavy_check_mark:                                                                                     | The request object to use for the request.                                                             |

### Response

**[?Operations\CreateLabelReallocationResponse](../../Models/Operations/CreateLabelReallocationResponse.md)**

### Errors

| Error Type                                                      | Status Code                                                     | Content Type                                                    |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| Errors\BadRequestError                                          | 400                                                             | application/vnd.dwolla.v1.hal+json                              |
| Errors\CreateLabelReallocationForbiddenDwollaV1HalJSONException | 403                                                             | application/vnd.dwolla.v1.hal+json                              |
| Errors\CreateLabelReallocationNotFoundDwollaV1HalJSONException  | 404                                                             | application/vnd.dwolla.v1.hal+json                              |
| Errors\APIException                                             | 4XX, 5XX                                                        | \*/\*                                                           |

## get

Retrieve details for a specific label reallocation that transfers funds between Labels. Returns reallocation information including source and destination Labels, amount transferred, status, and creation timestamp. Use this to track and audit fund movements between different Labels.

### Example Usage

<!-- UsageSnippet language="php" operationID="retrieveLabelReallocation" method="get" path="/label-reallocations/{reallocationId}" -->
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



$response = $sdk->labels->reallocations->get(
    reallocationId: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                            | Type                                 | Required                             | Description                          |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `reallocationId`                     | *string*                             | :heavy_check_mark:                   | Label reallocation unique identifier |

### Response

**[?Operations\RetrieveLabelReallocationResponse](../../Models/Operations/RetrieveLabelReallocationResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |