# Labels.LedgerEntries

## Overview

### Available Operations

* [list](#list) - List label ledger entries
* [create](#create) - Create a label ledger entry
* [get](#get) - Retrieve a label ledger entry

## list

Returns all ledger entries for a specific Label, sorted by creation date (newest first). Supports pagination with limit and offset parameters. Each ledger entry includes its amount, currency, and creation timestamp.

### Example Usage

<!-- UsageSnippet language="php" operationID="listLabelLedgerEntries" method="get" path="/labels/{id}/ledger-entries" -->
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



$response = $sdk->labels->ledgerEntries->list(
    id: '<id>'
);

if ($response->labelLedgerEntries !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | A label unique identifier  |
| `limit`                    | *?int*                     | :heavy_minus_sign:         | How many results to return |
| `offset`                   | *?int*                     | :heavy_minus_sign:         | How many results to skip   |

### Response

**[?Operations\ListLabelLedgerEntriesResponse](../../Models/Operations/ListLabelLedgerEntriesResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\BadRequestError             | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## create

Create a new ledger entry to track fund adjustments on a Label by specifying a positive or negative amount value. Returns the location of the created ledger entry in the response header. Label amounts cannot go negative, so validation errors occur if the entry would result in a negative Label balance.

### Example Usage

<!-- UsageSnippet language="php" operationID="createLabelLedgerEntry" method="post" path="/labels/{id}/ledger-entries" -->
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

$body = new Operations\CreateLabelLedgerEntryRequestBody(
    amount: new Operations\CreateLabelLedgerEntryAmount(
        value: '-5.00',
        currency: 'USD',
    ),
);

$response = $sdk->labels->ledgerEntries->create(
    id: '<id>',
    body: $body

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                    | Type                                                                                                         | Required                                                                                                     | Description                                                                                                  |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                         | *string*                                                                                                     | :heavy_check_mark:                                                                                           | The Id of the Label to update.                                                                               |
| `body`                                                                                                       | [Operations\CreateLabelLedgerEntryRequestBody](../../Models/Operations/CreateLabelLedgerEntryRequestBody.md) | :heavy_check_mark:                                                                                           | Parameters to create a label ledger entry                                                                    |

### Response

**[?Operations\CreateLabelLedgerEntryResponse](../../Models/Operations/CreateLabelLedgerEntryResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\BadRequestError             | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## get

Returns detailed information for a specific ledger entry on a Label, including its amount, currency, and creation timestamp.

### Example Usage

<!-- UsageSnippet language="php" operationID="getLabelLedgerEntry" method="get" path="/ledger-entries/{ledgerEntryId}" -->
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



$response = $sdk->labels->ledgerEntries->get(
    ledgerEntryId: '<id>'
);

if ($response->labelLedgerEntry !== null) {
    // handle response
}
```

### Parameters

| Parameter                              | Type                                   | Required                               | Description                            |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| `ledgerEntryId`                        | *string*                               | :heavy_check_mark:                     | A label ledger entry unique identifier |

### Response

**[?Operations\GetLabelLedgerEntryResponse](../../Models/Operations/GetLabelLedgerEntryResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |