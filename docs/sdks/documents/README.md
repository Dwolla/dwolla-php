# Documents

## Overview

Operations related to Documents

### Available Operations

* [get](#get) - Retrieve a document

## get

Returns detailed information about a specific identity verification document, including its status, type, and verification results. Used to track document submission and verification progress during the business verification process.

### Example Usage

<!-- UsageSnippet language="php" operationID="retrieveDocument" method="get" path="/documents/{id}" -->
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



$response = $sdk->documents->get(
    id: '<id>'
);

if ($response->document !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | Document unique identifier |

### Response

**[?Operations\RetrieveDocumentResponse](../../Models/Operations/RetrieveDocumentResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |