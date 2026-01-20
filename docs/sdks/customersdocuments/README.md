# Customers.Documents

## Overview

### Available Operations

* [list](#list) - List documents for customer
* [create](#create) - Create a document for customer

## list

Returns all identity verification documents submitted for a customer. Includes document status, verification results, document type (passport, driver's license, etc.), and failure reasons if verification was rejected. Used to track document submission and verification progress during the business verification process.

### Example Usage

<!-- UsageSnippet language="php" operationID="listCustomerDocuments" method="get" path="/customers/{id}/documents" -->
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



$response = $sdk->customers->documents->list(
    id: '<id>'
);

if ($response->documents !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | customer unique identifier |

### Response

**[?Operations\ListCustomerDocumentsResponse](../../Models/Operations/ListCustomerDocumentsResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## create

Uploads an identity verification document for a customer using multipart form-data. Required when a customer has "document" status during the verification process.

### Example Usage

<!-- UsageSnippet language="php" operationID="createCustomerDocument" method="post" path="/customers/{id}/documents" -->
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

$body = new Operations\CreateCustomerDocumentRequestBody(
    documentType: Operations\CreateCustomerDocumentDocumentType::License,
    file: new Operations\CreateCustomerDocumentFile(
        fileName: 'example.file',
        content: file_get_contents('example.file');,
    ),
);

$response = $sdk->customers->documents->create(
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
| `id`                                                                                                         | *string*                                                                                                     | :heavy_check_mark:                                                                                           | customer unique identifier                                                                                   |
| `body`                                                                                                       | [Operations\CreateCustomerDocumentRequestBody](../../Models/Operations/CreateCustomerDocumentRequestBody.md) | :heavy_check_mark:                                                                                           | Upload a document for a customer.                                                                            |

### Response

**[?Operations\CreateCustomerDocumentResponse](../../Models/Operations/CreateCustomerDocumentResponse.md)**

### Errors

| Error Type                                                                 | Status Code                                                                | Content Type                                                               |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Errors\MaximumNumberOfResourcesSchemaException                             | 400                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\InvalidFileTypeSchemaException                                      | 400                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\DuplicateResourceSchemaException                                    | 400                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\InvalidResourceStateSchemaException                                 | 403                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\NotAuthorizedSchemaException                                        | 403                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\CreateCustomerDocumentNotFoundDwollaV1HalJSONException              | 404                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\CreateCustomerDocumentRequestEntityTooLargeDwollaV1HalJSONException | 413                                                                        | application/vnd.dwolla.v1.hal+json                                         |
| Errors\APIException                                                        | 4XX, 5XX                                                                   | \*/\*                                                                      |