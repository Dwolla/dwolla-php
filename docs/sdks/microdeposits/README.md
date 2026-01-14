# FundingSources.MicroDeposits

## Overview

### Available Operations

* [getMicroDeposits](#getmicrodeposits) - Retrieve micro-deposits details
* [initiateOrVerify](#initiateorverify) - Initiate or Verify micro-deposits

## getMicroDeposits

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



$response = $sdk->fundingSources->microDeposits->getMicroDeposits(
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

## initiateOrVerify

Handles micro-deposit bank verification process. Make a request without a request body to initiate two small deposits to the customer's bank account. Include deposit amounts to verify the received values and complete verification.

### Example Usage

<!-- UsageSnippet language="php" operationID="initiateOrVerifyMicroDeposits" method="post" path="/funding-sources/{id}/micro-deposits" -->
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



$response = $sdk->fundingSources->microDeposits->initiateOrVerify(
    id: '<id>',
    body: new Operations\InitiateMicroDeposits()

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                   | Type                                                                                                                                                                        | Required                                                                                                                                                                    | Description                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                        | *string*                                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                          | The ID of the FS to initiate or verify micro-deposit                                                                                                                        |
| `body`                                                                                                                                                                      | [Operations\InitiateMicroDeposits\|Components\VerifyMicroDeposits\|null](../../Models/Operations/InitiateOrVerifyMicroDepositsRequestBody.md)                               | :heavy_minus_sign:                                                                                                                                                          | Optional request body for verifying micro-deposits.<br/>- If omitted: Endpoint will initiate micro-deposits<br/>- If provided: Must contain micro-deposit amounts for verification<br/> |

### Response

**[?Operations\InitiateOrVerifyMicroDepositsResponse](../../Models/Operations/InitiateOrVerifyMicroDepositsResponse.md)**

### Errors

| Error Type                                                            | Status Code                                                           | Content Type                                                          |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Errors\InitiateOrVerifyMicroDepositsForbiddenDwollaV1HalJSONException | 403                                                                   | application/vnd.dwolla.v1.hal+json                                    |
| Errors\InitiateOrVerifyMicroDepositsNotFoundDwollaV1HalJSONException  | 404                                                                   | application/vnd.dwolla.v1.hal+json                                    |
| Errors\APIException                                                   | 4XX, 5XX                                                              | \*/\*                                                                 |