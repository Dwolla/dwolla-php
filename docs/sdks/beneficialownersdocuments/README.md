# BeneficialOwners.Documents

## Overview

### Available Operations

* [list](#list) - List documents for beneficial owner
* [create](#create) - Create a document for beneficial owner

## list

Returns all identity verification documents submitted for a beneficial owner. Includes document status, verification results, document type (passport, driver's license, etc.), and failure reasons if verification was rejected. Used to track document submission and verification progress during the business verification process.

### Example Usage

<!-- UsageSnippet language="php" operationID="listBeneficialOwnerDocuments" method="get" path="/beneficial-owners/{id}/documents" -->
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



$response = $sdk->beneficialOwners->documents->list(
    id: '<id>'
);

if ($response->documents !== null) {
    // handle response
}
```

### Parameters

| Parameter                          | Type                               | Required                           | Description                        |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `id`                               | *string*                           | :heavy_check_mark:                 | beneficial owner unique identifier |

### Response

**[?Operations\ListBeneficialOwnerDocumentsResponse](../../Models/Operations/ListBeneficialOwnerDocumentsResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## create

Uploads an identity verification document for a beneficial owner using multipart form-data. Required when a beneficial owner has "document" status during the business verification process.

### Example Usage

<!-- UsageSnippet language="php" operationID="createBeneficialOwnerDocument" method="post" path="/beneficial-owners/{id}/documents" -->
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

$body = new Operations\CreateBeneficialOwnerDocumentRequestBody(
    documentType: Operations\CreateBeneficialOwnerDocumentDocumentType::License,
    file: new Operations\CreateBeneficialOwnerDocumentFile(
        fileName: 'example.file',
        content: file_get_contents('example.file');,
    ),
);

$response = $sdk->beneficialOwners->documents->create(
    id: '<id>',
    body: $body

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                  | Type                                                                                                                       | Required                                                                                                                   | Description                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                       | *string*                                                                                                                   | :heavy_check_mark:                                                                                                         | beneficial owner unique identifier                                                                                         |
| `body`                                                                                                                     | [Operations\CreateBeneficialOwnerDocumentRequestBody](../../Models/Operations/CreateBeneficialOwnerDocumentRequestBody.md) | :heavy_check_mark:                                                                                                         | Upload a document for a beneficial owner.                                                                                  |

### Response

**[?Operations\CreateBeneficialOwnerDocumentResponse](../../Models/Operations/CreateBeneficialOwnerDocumentResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Errors\MaximumNumberOfResourcesSchemaException               | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\InvalidFileTypeSchemaException                        | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\DuplicateResourceSchemaException                      | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\ForbiddenError                                        | 403                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\NotFoundError                                         | 404                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\CreateBeneficialOwnerDocumentDwollaV1HalJSONException | 413                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\APIException                                          | 4XX, 5XX                                                     | \*/\*                                                        |