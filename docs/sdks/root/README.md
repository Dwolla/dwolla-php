# Root

## Overview

Root API operations

### Available Operations

* [get](#get) - root

## get

Retrieve the API root entry point to discover available resources and endpoints based on your OAuth access token permissions. Returns HAL+JSON with navigation links to accessible resources including accounts, customers, events, and webhook subscriptions depending on token scope. Essential for API exploration, dynamic resource discovery, and building adaptive client applications that respond to available permissions.

### Example Usage

<!-- UsageSnippet language="php" operationID="getRoot" method="get" path="/" -->
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



$response = $sdk->root->get(

);

if ($response->root !== null) {
    // handle response
}
```

### Response

**[?Operations\GetRootResponse](../../Models/Operations/GetRootResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| Errors\GetRootDwollaV1HalJSONException | 401                                    | application/vnd.dwolla.v1.hal+json     |
| Errors\APIException                    | 4XX, 5XX                               | \*/\*                                  |