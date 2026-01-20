# FundingSources.MicroDeposits

## Overview

### Available Operations

* [get](#get) - Retrieve micro-deposits details
* [initiate](#initiate) - Initiate micro-deposits
* [verify](#verify) - Verify micro-deposits

## get

Returns the status and details of micro-deposits for a funding source to check verification eligibility. Includes deposit status (pending, processed, failed), creation timestamp, and failure details with ACH return codes if deposits failed. Use this endpoint to determine when micro-deposits are ready for verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="getMicroDeposits" method="get" path="/funding-sources/{id}/micro-deposits" -->
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



$response = $sdk->fundingSources->microDeposits->get(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                     | Type                                                          | Required                                                      | Description                                                   |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `id`                                                          | *string*                                                      | :heavy_check_mark:                                            | The ID of the FS that previously had micro-deposits initiated |

### Response

**[?Operations\GetMicroDepositsResponse](../../Models/Operations/GetMicroDepositsResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## initiate

Initiates two small deposits to the customer's bank account for verification purposes. No request body is required.

### Example Usage

<!-- UsageSnippet language="php" operationID="initiateMicroDeposits" method="post" path="/funding-sources/{id}/micro-deposits#initiate" -->
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



$response = $sdk->fundingSources->microDeposits->initiate(
    id: '<id>'
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                   | Type                                                        | Required                                                    | Description                                                 |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `id`                                                        | *string*                                                    | :heavy_check_mark:                                          | The ID of the funding source to initiate micro-deposits for |

### Response

**[?Operations\InitiateMicroDepositsResponse](../../Models/Operations/InitiateMicroDepositsResponse.md)**

### Errors

| Error Type                                                    | Status Code                                                   | Content Type                                                  |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| Errors\InitiateMicroDepositsForbiddenDwollaV1HalJSONException | 403                                                           | application/vnd.dwolla.v1.hal+json                            |
| Errors\InitiateMicroDepositsNotFoundDwollaV1HalJSONException  | 404                                                           | application/vnd.dwolla.v1.hal+json                            |
| Errors\APIException                                           | 4XX, 5XX                                                      | \*/\*                                                         |

## verify

Verifies the micro-deposit amounts received in the customer's bank account to complete funding source verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="verifyMicroDeposits" method="post" path="/funding-sources/{id}/micro-deposits#verify" -->
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

$body = new Operations\VerifyMicroDepositsRequestBody(
    amount1: new Operations\Amount1(
        value: '0.02',
        currency: 'USD',
    ),
    amount2: new Operations\Amount2(
        value: '0.03',
        currency: 'USD',
    ),
);

$response = $sdk->fundingSources->microDeposits->verify(
    id: '<id>',
    body: $body

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                              | Type                                                                                                   | Required                                                                                               | Description                                                                                            |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                   | *string*                                                                                               | :heavy_check_mark:                                                                                     | The ID of the funding source to verify micro-deposits for                                              |
| `body`                                                                                                 | [Operations\VerifyMicroDepositsRequestBody](../../Models/Operations/VerifyMicroDepositsRequestBody.md) | :heavy_check_mark:                                                                                     | The micro-deposit amounts received in the bank account                                                 |

### Response

**[?Operations\VerifyMicroDepositsResponse](../../Models/Operations/VerifyMicroDepositsResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Errors\VerifyMicroDepositsBadRequestDwollaV1HalJSONException | 400                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\VerifyMicroDepositsForbiddenDwollaV1HalJSONException  | 403                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\VerifyMicroDepositsNotFoundDwollaV1HalJSONException   | 404                                                          | application/vnd.dwolla.v1.hal+json                           |
| Errors\APIException                                          | 4XX, 5XX                                                     | \*/\*                                                        |