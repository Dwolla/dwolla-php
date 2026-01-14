# Labels

## Overview

Operations related to Labels

### Available Operations

* [get](#get) - Retrieve a label
* [remove](#remove) - Remove a label

## get

Retrieve details for a specific Label used to categorize and track funds within your account. Returns Label information including unique identifier, current amount with currency, and creation timestamp.

### Example Usage

<!-- UsageSnippet language="php" operationID="getLabel" method="get" path="/labels/{id}" -->
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



$response = $sdk->labels->get(
    id: '<id>'
);

if ($response->label !== null) {
    // handle response
}
```

### Parameters

| Parameter               | Type                    | Required                | Description             |
| ----------------------- | ----------------------- | ----------------------- | ----------------------- |
| `id`                    | *string*                | :heavy_check_mark:      | Label unique identifier |

### Response

**[?Operations\GetLabelResponse](../../Models/Operations/GetLabelResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## remove

Delete a Label to stop tracking funds and remove it from your account. Returns success status if the Label is successfully removed. Use this to streamline your account management and remove unused Labels from your system.

### Example Usage

<!-- UsageSnippet language="php" operationID="removeLabel" method="delete" path="/labels/{id}" -->
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



$response = $sdk->labels->remove(
    id: '<id>'
);

if ($response->label !== null) {
    // handle response
}
```

### Parameters

| Parameter                 | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `id`                      | *string*                  | :heavy_check_mark:        | A label unique identifier |

### Response

**[?Operations\RemoveLabelResponse](../../Models/Operations/RemoveLabelResponse.md)**

### Errors

| Error Type                                 | Status Code                                | Content Type                               |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| Errors\RemoveLabelDwollaV1HalJSONException | 403                                        | application/vnd.dwolla.v1.hal+json         |
| Errors\NotFoundError                       | 404                                        | application/vnd.dwolla.v1.hal+json         |
| Errors\APIException                        | 4XX, 5XX                                   | \*/\*                                      |