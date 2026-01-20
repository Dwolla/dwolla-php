# Transfers.Failure

## Overview

### Available Operations

* [get](#get) - Retrieve a transfer failure reason

## get

Retrieve detailed failure information for a failed bank or VAN transfer including the ACH return code, description, and explanation. Returns failure details with links to the failed funding source and associated Customer for comprehensive error analysis. Available only for transfers with failure status and accessed through the failure link from transfer retrieval. Critical for troubleshooting payment failures and understanding ACH return reasons.

### Example Usage

<!-- UsageSnippet language="php" operationID="getTransferFailureReason" method="get" path="/transfers/{id}/failure" -->
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



$response = $sdk->transfers->failure->get(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `id`                       | *string*                   | :heavy_check_mark:         | Transfer unique identifier |

### Response

**[?Operations\GetTransferFailureReasonResponse](../../Models/Operations/GetTransferFailureReasonResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |