# MassPayments

## Overview

### Available Operations

* [create](#create) - Initiate a mass payment
* [get](#get) - Retrieve a mass payment
* [update](#update) - Update a mass payment

## create

Create a mass payment containing up to 5,000 individual payment items from a Dwolla Main Account or Verified Customer funding source. Supports optional metadata, correlation IDs for traceability, deferred processing, and expedited transfer options including same-day ACH clearing. Returns the location of the created mass payment resource with a unique identifier for tracking and management.

### Example Usage

<!-- UsageSnippet language="php" operationID="initiateMassPayment" method="post" path="/mass-payments" -->
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

$body = new Operations\InitiateMassPaymentRequestBody(
    links: new Operations\InitiateMassPaymentLinks(
        source: new Operations\InitiateMassPaymentLinksSource(
            href: 'https://api.dwolla.com/funding-sources/707177c3-bf15-4e7e-b37c-55c3898d9bf4',
        ),
    ),
    items: [
        new Operations\Item(
            links: new Operations\ItemLinks(
                destination: new Operations\InitiateMassPaymentLinksDestination(
                    href: 'https://api.dwolla.com/funding-sources/9c7f8d57-cd45-4e7a-bf7a-914dbd6131db',
                ),
            ),
            amount: new Components\TransferAmount(
                value: '5.00',
                currency: 'USD',
            ),
            processingChannel: new Operations\InitiateMassPaymentProcessingChannel(
                destination: 'real-time-payments',
            ),
            clearing: new Operations\ItemClearing(
                destination: 'next-available',
            ),
            achDetails: new Operations\ItemAchDetails(
                destination: new Operations\InitiateMassPaymentAchDetailsDestination(
                    addenda: new Operations\ItemAddenda(
                        values: [
                            'XYZ987_AddendaValue',
                        ],
                    ),
                ),
            ),
            correlationId: 'ad6ca82d-59f7-45f0-a8d2-94c2cd4e8841',
        ),
    ],
    status: 'deferred',
    achDetails: new Operations\InitiateMassPaymentAchDetails(
        source: new Operations\InitiateMassPaymentAchDetailsSource(
            addenda: new Operations\InitiateMassPaymentSourceAddenda(
                values: [
                    'ZYX987_AddendaValue',
                ],
            ),
        ),
    ),
    clearing: new Operations\InitiateMassPaymentClearing(
        source: 'next-available',
    ),
    correlationId: 'ad6ca82d-59f7-45f0-a8d2-94c2cd4e8841',
);

$response = $sdk->massPayments->create(
    body: $body,
    idempotencyKey: '19051a62-3403-11e6-ac61-9e71128cae77'

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                              | Type                                                                                                   | Required                                                                                               | Description                                                                                            | Example                                                                                                |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `body`                                                                                                 | [Operations\InitiateMassPaymentRequestBody](../../Models/Operations/InitiateMassPaymentRequestBody.md) | :heavy_check_mark:                                                                                     | Parameters for initiating a mass payment                                                               |                                                                                                        |
| `idempotencyKey`                                                                                       | *?string*                                                                                              | :heavy_minus_sign:                                                                                     | N/A                                                                                                    | 19051a62-3403-11e6-ac61-9e71128cae77                                                                   |

### Response

**[?Operations\InitiateMassPaymentResponse](../../Models/Operations/InitiateMassPaymentResponse.md)**

### Errors

| Error Type                                         | Status Code                                        | Content Type                                       |
| -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| Errors\BadRequestError                             | 400                                                | application/vnd.dwolla.v1.hal+json                 |
| Errors\InitiateMassPaymentDwollaV1HalJSONException | 403                                                | application/vnd.dwolla.v1.hal+json                 |
| Errors\APIException                                | 4XX, 5XX                                           | \*/\*                                              |

## get

Retrieve detailed information for a mass payment by its unique identifier. Returns the current processing status (pending, processing, or complete), creation date, metadata, and links to the source funding source and payment items. Use this endpoint to monitor mass payment processing progress and determine when to check individual item results.

### Example Usage

<!-- UsageSnippet language="php" operationID="getMassPayment" method="get" path="/mass-payments/{id}" -->
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



$response = $sdk->massPayments->get(
    id: '<id>'
);

if ($response->massPayment !== null) {
    // handle response
}
```

### Parameters

| Parameter                      | Type                           | Required                       | Description                    |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| `id`                           | *string*                       | :heavy_check_mark:             | Mass payment unique identifier |

### Response

**[?Operations\GetMassPaymentResponse](../../Models/Operations/GetMassPaymentResponse.md)**

### Errors

| Error Type                                             | Status Code                                            | Content Type                                           |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Errors\GetMassPaymentForbiddenDwollaV1HalJSONException | 403                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\GetMassPaymentNotFoundDwollaV1HalJSONException  | 404                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\APIException                                    | 4XX, 5XX                                               | \*/\*                                                  |

## update

Update the status of a deferred mass payment to control its processing lifecycle. Set status to `pending` to trigger processing and begin fund transfers, or `cancelled` to permanently cancel the mass payment before processing begins. Only applies to mass payments created with deferred status. Returns the updated mass payment resource with the new status.

### Example Usage

<!-- UsageSnippet language="php" operationID="updateMassPayment" method="post" path="/mass-payments/{id}" -->
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

$body = new Operations\UpdateMassPaymentRequestBody(
    status: 'pending',
);

$response = $sdk->massPayments->update(
    id: '<id>',
    body: $body

);

if ($response->massPayment !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                          | Type                                                                                               | Required                                                                                           | Description                                                                                        |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `id`                                                                                               | *string*                                                                                           | :heavy_check_mark:                                                                                 | ID of mass payment to update                                                                       |
| `body`                                                                                             | [Operations\UpdateMassPaymentRequestBody](../../Models/Operations/UpdateMassPaymentRequestBody.md) | :heavy_check_mark:                                                                                 | Parameters for updating a mass payment                                                             |

### Response

**[?Operations\UpdateMassPaymentResponse](../../Models/Operations/UpdateMassPaymentResponse.md)**

### Errors

| Error Type                                                | Status Code                                               | Content Type                                              |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| Errors\BadRequestError                                    | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\UpdateMassPaymentForbiddenDwollaV1HalJSONException | 403                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\UpdateMassPaymentNotFoundDwollaV1HalJSONException  | 404                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\APIException                                       | 4XX, 5XX                                                  | \*/\*                                                     |