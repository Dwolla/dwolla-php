# ExchangePartners

## Overview

### Available Operations

* [list](#list) - List exchange partners
* [get](#get) - Retrieve exchange partner

## list

Returns a list of all supported exchange partners. Each partner includes a unique ID, name, and status indicating whether they are active or inactive.

### Example Usage

<!-- UsageSnippet language="php" operationID="listExchangePartners" method="get" path="/exchange-partners" -->
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



$response = $sdk->exchangePartners->list(

);

if ($response->exchangePartners !== null) {
    // handle response
}
```

### Response

**[?Operations\ListExchangePartnersResponse](../../Models/Operations/ListExchangePartnersResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## get

Returns details for a specific open banking provider that integrates with Dwolla. Includes partner name, status, and creation date. Use this to verify partner availability before creating exchanges and funding sources.

### Example Usage

<!-- UsageSnippet language="php" operationID="getExchangePartner" method="get" path="/exchange-partners/{id}" -->
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



$response = $sdk->exchangePartners->get(
    id: '292317ec-e252-47d8-93c3-2d128e037aa4'
);

if ($response->exchangePartner !== null) {
    // handle response
}
```

### Parameters

| Parameter                                    | Type                                         | Required                                     | Description                                  | Example                                      |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| `id`                                         | *string*                                     | :heavy_check_mark:                           | Exchange Partner resource unique identifier. | 292317ec-e252-47d8-93c3-2d128e037aa4         |

### Response

**[?Operations\GetExchangePartnerResponse](../../Models/Operations/GetExchangePartnerResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |