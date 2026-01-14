# FundingSources.OnDemandTransferAuthorizations

## Overview

### Available Operations

* [create](#create) - Create an on-demand transfer authorization

## create

Create an on-demand transfer authorization that allows Customers to pre-authorize variable amount ACH transfers from their bank account for future payments. This authorization is used when creating Customer funding sources to enable flexible payment processing. Returns UI text elements including authorization body text and button text for display in your application's bank account addition flow.

### Example Usage

<!-- UsageSnippet language="php" operationID="createOnDemandTransferAuthorization" method="post" path="/on-demand-authorizations" -->
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



$response = $sdk->fundingSources->onDemandTransferAuthorizations->create(

);

if ($response->onDemandAuthorization !== null) {
    // handle response
}
```

### Response

**[?Operations\CreateOnDemandTransferAuthorizationResponse](../../Models/Operations/CreateOnDemandTransferAuthorizationResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |