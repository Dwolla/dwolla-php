# BusinessClassifications

## Overview

### Available Operations

* [list](#list) - List business classifications
* [get](#get) - Retrieve a business classification

## list

Returns a directory of business and industry classifications required for creating business verified customers. Each business classification contains multiple industry classifications. The industry classification ID must be provided in the businessClassification parameter during business customer creation for verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="listBusinessClassifications" method="get" path="/business-classifications" -->
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



$response = $sdk->businessClassifications->list(

);

if ($response->businessClassifications !== null) {
    // handle response
}
```

### Response

**[?Operations\ListBusinessClassificationsResponse](../../Models/Operations/ListBusinessClassificationsResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## get

Returns a specific business classification with its embedded industry classifications. Use this endpoint to browse available industry options within a business category and obtain the industry classification ID required for the businessClassification parameter when creating business verified customers.

### Example Usage

<!-- UsageSnippet language="php" operationID="retrieveBusinessClassification" method="get" path="/business-classifications/{id}" -->
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



$response = $sdk->businessClassifications->get(
    id: '<id>'
);

if ($response->businessClassification !== null) {
    // handle response
}
```

### Parameters

| Parameter                                 | Type                                      | Required                                  | Description                               |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| `id`                                      | *string*                                  | :heavy_check_mark:                        | business classification unique identifier |

### Response

**[?Operations\RetrieveBusinessClassificationResponse](../../Models/Operations/RetrieveBusinessClassificationResponse.md)**

### Errors

| Error Type                                                    | Status Code                                                   | Content Type                                                  |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| Errors\RetrieveBusinessClassificationDwollaV1HalJSONException | 404                                                           | application/vnd.dwolla.v1.hal+json                            |
| Errors\APIException                                           | 4XX, 5XX                                                      | \*/\*                                                         |