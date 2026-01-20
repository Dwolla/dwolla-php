# SandboxSimulations

## Overview

Sandbox-only operations for simulating processing of bank transfers

### Available Operations

* [simulate](#simulate) - Simulate bank transfer processing (Sandbox only)

## simulate

Triggers processing for the last 500 bank transfers on the authorized application or Sandbox account. This endpoint is only available in the Sandbox environment. It will process or fail pending bank-to-bank transactions (including both sides of a transfer when applicable) and initiated micro-deposits. If webhooks are configured, corresponding events will be delivered.

If a bank-to-bank transaction is initiated between two users, call this endpoint twice to process both the debit and credit sides.


### Example Usage

<!-- UsageSnippet language="php" operationID="simulateBankTransferProcessing" method="post" path="/sandbox-simulations" -->
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



$response = $sdk->sandboxSimulations->simulate(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                            | Type                                                                                                                 | Required                                                                                                             | Description                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `$request`                                                                                                           | [Operations\SimulateBankTransferProcessingRequest](../../Models/Operations/SimulateBankTransferProcessingRequest.md) | :heavy_check_mark:                                                                                                   | The request object to use for the request.                                                                           |

### Response

**[?Operations\SimulateBankTransferProcessingResponse](../../Models/Operations/SimulateBankTransferProcessingResponse.md)**

### Errors

| Error Type                                                                | Status Code                                                               | Content Type                                                              |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Errors\SimulateBankTransferProcessingUnauthorizedDwollaV1HalJSONException | 401                                                                       | application/vnd.dwolla.v1.hal+json                                        |
| Errors\SimulateBankTransferProcessingForbiddenDwollaV1HalJSONException    | 403                                                                       | application/vnd.dwolla.v1.hal+json                                        |
| Errors\APIException                                                       | 4XX, 5XX                                                                  | \*/\*                                                                     |