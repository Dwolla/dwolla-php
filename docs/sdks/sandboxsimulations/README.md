# SandboxSimulations

## Overview

Sandbox-only operations for simulating processing of bank transfers

### Available Operations

* [simulate](#simulate) - Sandbox simulations (bank transfers, VAN transfers, or customer verification directives)

## simulate

Sandbox-only endpoint with three modes:

**Simulate bank transfer processing** — Omit the body or send an empty JSON object. Processes or fails
the last 500 bank transfers on the authorized application or Sandbox account (and initiated micro-deposits).
If webhooks are configured, events are delivered. If a bank-to-bank transaction involves two users,
call this twice to process debit and credit sides. Returns **200** with a HAL document including `total`.

**Simulate VAN (virtual) transfers** — Send a JSON body with `type` set to `virtual` and a `transfers`
array (up to 10 items). External transfers are created and processed immediately. Returns **202 Accepted**.

**Simulate verification directives** — For a business Verified Customer in **`retry`** or **`document`**
status, send `type`: `customer-verification`, `_links.customer.href` pointing at that customer, and
`errorCode` set to one of: `PersonalIDRequired`, `POBoxNotAllowed`, `AddressNotAssociatedWithBusiness`,
`EINDocumentRequired`. Returns **200** with HAL `_links.self` and `errorCode`. Then **GET** the Customer;
the same code appears in `_embedded.errors` for end-to-end testing.


### Example Usage: bankTransferProcessing

<!-- UsageSnippet language="php" operationID="simulateBankTransferProcessing" method="post" path="/sandbox-simulations" example="bankTransferProcessing" -->
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

$request = new Components\SandboxSimulationBankProcessingRequest();

$response = $sdk->sandboxSimulations->simulate(
    request: $request
);

if ($response->oneOf !== null) {
    // handle response
}
```
### Example Usage: customerVerificationDirective

<!-- UsageSnippet language="php" operationID="simulateBankTransferProcessing" method="post" path="/sandbox-simulations" example="customerVerificationDirective" -->
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

$request = new Components\SandboxSimulationVirtualAccountTransfersRequest(
    transfers: [],
);

$response = $sdk->sandboxSimulations->simulate(
    request: $request
);

if ($response->oneOf !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                                                                   | Type                                                                                                                                                                                                                        | Required                                                                                                                                                                                                                    | Description                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$request`                                                                                                                                                                                                                  | [Components\SandboxSimulationVirtualAccountTransfersRequest\|Components\SandboxSimulationCustomerVerificationRequest\|Components\SandboxSimulationBankProcessingRequest](../../Models/Components/SandboxSimulationRequest.md) | :heavy_check_mark:                                                                                                                                                                                                          | The request object to use for the request.                                                                                                                                                                                  |

### Response

**[?Operations\SimulateBankTransferProcessingResponse](../../Models/Operations/SimulateBankTransferProcessingResponse.md)**

### Errors

| Error Type                                                                | Status Code                                                               | Content Type                                                              |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Errors\BadRequestError                                                    | 400                                                                       | application/vnd.dwolla.v1.hal+json                                        |
| Errors\SimulateBankTransferProcessingUnauthorizedDwollaV1HalJSONException | 401                                                                       | application/vnd.dwolla.v1.hal+json                                        |
| Errors\SimulateBankTransferProcessingForbiddenDwollaV1HalJSONException    | 403                                                                       | application/vnd.dwolla.v1.hal+json                                        |
| Errors\APIException                                                       | 4XX, 5XX                                                                  | \*/\*                                                                     |