# FundingSources

## Overview

### Available Operations

* [get](#get) - Retrieve a funding source
* [updateOrRemove](#updateorremove) - Update or remove a funding source
* [getVanRouting](#getvanrouting) - Retrieve VAN account and routing numbers

## get

Returns detailed information for a specific funding source, including its type, status, and verification details. Supports bank accounts (via Open Banking), debit card funding sources, and Dwolla balance (verified customers only). Debit card funding sources include masked card details such as brand, last four digits, expiration date, and cardholder name.

### Example Usage

<!-- UsageSnippet language="php" operationID="getFundingSource" method="get" path="/funding-sources/{id}" -->
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



$response = $sdk->fundingSources->get(
    id: '<id>'
);

if ($response->fundingSource !== null) {
    // handle response
}
```

### Parameters

| Parameter                        | Type                             | Required                         | Description                      |
| -------------------------------- | -------------------------------- | -------------------------------- | -------------------------------- |
| `id`                             | *string*                         | :heavy_check_mark:               | Funding source unique identifier |

### Response

**[?Operations\GetFundingSourceResponse](../../Models/Operations/GetFundingSourceResponse.md)**

### Errors

| Error Type                                      | Status Code                                     | Content Type                                    |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| Errors\GetFundingSourceDwollaV1HalJSONException | 404                                             | application/vnd.dwolla.v1.hal+json              |
| Errors\APIException                             | 4XX, 5XX                                        | \*/\*                                           |

## updateOrRemove

Updates a bank funding source's details or soft deletes it. When updating, you can change the name (any status) or modify routing/account numbers and account type (unverified status only). When removing, the funding source is soft deleted and can still be accessed but marked as removed.

### Example Usage

<!-- UsageSnippet language="php" operationID="updateOrRemoveFundingSource" method="post" path="/funding-sources/{id}" -->
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



$response = $sdk->fundingSources->updateOrRemove(
    id: '<id>',
    body: new Components\RemoveBank(
        removed: true,
    )

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                | Type                                                                                                                                                     | Required                                                                                                                                                 | Description                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                     | *string*                                                                                                                                                 | :heavy_check_mark:                                                                                                                                       | Funding source unique identifier                                                                                                                         |
| `body`                                                                                                                                                   | [Components\UpdateUnverifiedBank\|Components\UpdateVerifiedBank\|Components\RemoveBank](../../Models/Operations/UpdateOrRemoveFundingSourceRequestBody.md) | :heavy_check_mark:                                                                                                                                       | Parameters to update a customer funding source                                                                                                           |

### Response

**[?Operations\UpdateOrRemoveFundingSourceResponse](../../Models/Operations/UpdateOrRemoveFundingSourceResponse.md)**

### Errors

| Error Type                                                           | Status Code                                                          | Content Type                                                         |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Errors\UpdateOrRemoveFundingSourceBadRequestDwollaV1HalJSONException | 400                                                                  | application/vnd.dwolla.v1.hal+json                                   |
| Errors\UpdateOrRemoveFundingSourceForbiddenDwollaV1HalJSONException  | 403                                                                  | application/vnd.dwolla.v1.hal+json                                   |
| Errors\APIException                                                  | 4XX, 5XX                                                             | \*/\*                                                                |

## getVanRouting

Returns the unique account and routing numbers for a Virtual Account Number (VAN) funding source. These numbers can be used by external systems to initiate ACH transactions that pull funds from or push funds to the associated Dwolla balance.

### Example Usage

<!-- UsageSnippet language="php" operationID="getVanRouting" method="get" path="/funding-sources/{id}/ach-routing" -->
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



$response = $sdk->fundingSources->getVanRouting(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                        | Type                                             | Required                                         | Description                                      |
| ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ |
| `id`                                             | *string*                                         | :heavy_check_mark:                               | ID of VAN funding source to retrieve ACH details |

### Response

**[?Operations\GetVanRoutingResponse](../../Models/Operations/GetVanRoutingResponse.md)**

### Errors

| Error Type                                   | Status Code                                  | Content Type                                 |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| Errors\GetVanRoutingDwollaV1HalJSONException | 404                                          | application/vnd.dwolla.v1.hal+json           |
| Errors\APIException                          | 4XX, 5XX                                     | \*/\*                                        |