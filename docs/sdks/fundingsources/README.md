# FundingSources

## Overview

### Available Operations

* [get](#get) - Retrieve a funding source
* [updateOrRemove](#updateorremove) - Update or remove a funding source
* [getVanRouting](#getvanrouting) - Retrieve VAN account and routing numbers

## get

Returns detailed information for a specific funding source, including its type, status, and verification details. Supports bank accounts (via Open Banking), debit card funding sources, and Dwolla balance (verified customers only). Debit card funding sources include masked card details such as brand, last four digits, expiration date, and cardholder name, along with `dateOfBirth` and `countryOfBirth` when those optional identity fields were supplied.

### Example Usage: card_funding_source

<!-- UsageSnippet language="php" operationID="getFundingSource" method="get" path="/funding-sources/{id}" example="card_funding_source" -->
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
### Example Usage: settlement_account

<!-- UsageSnippet language="php" operationID="getFundingSource" method="get" path="/funding-sources/{id}" example="settlement_account" -->
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
### Example Usage: standard_bank_account

<!-- UsageSnippet language="php" operationID="getFundingSource" method="get" path="/funding-sources/{id}" example="standard_bank_account" -->
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

Updates a bank or debit card funding source's details, or soft deletes it.

For **bank** funding sources you can change the name (any status), or modify routing/account
numbers and account type (unverified status only).

For **debit card** funding sources you can change the name and any field within `cardDetails`,
including the optional cardholder identity fields `dateOfBirth`, `countryOfBirth`, and
`identification`. This is how you add or update those identity values on a card funding source
that already exists.

You must provide at least one updateable field. Bank funding sources cannot be updated with
card fields, and card funding sources cannot be updated with bank fields.

When removing, the funding source is soft deleted and can still be accessed but marked as removed.


### Example Usage: bank_updated_with_card_fields

<!-- UsageSnippet language="php" operationID="updateOrRemoveFundingSource" method="post" path="/funding-sources/{id}" example="bank_updated_with_card_fields" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Brick\DateTime\LocalDate;
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
    body: new Components\UpdateCardFundingSource(
        name: 'My Visa Debit Card',
        cardDetails: new Components\UpdateCardFundingSourceCardDetails(
            firstName: 'Jane',
            lastName: 'Doe',
            billingAddress: new Components\UpdateCardFundingSourceBillingAddress(
                address1: '123 Main St',
                address2: 'Apt 4B',
                address3: 'Unit 101',
                city: 'Dallas',
                stateProvinceRegion: 'TX',
                country: 'US',
                postalCode: '76034',
            ),
            dateOfBirth: LocalDate::parse('1990-01-15'),
            countryOfBirth: 'US',
            identification: new Components\UpdateCardFundingSourceIdentification(
                type: Components\UpdateCardFundingSourceType::Passport,
                number: 'P123456',
                country: 'GB',
            ),
        ),
    )

);

if ($response->object !== null) {
    // handle response
}
```
### Example Usage: card_updated_with_bank_fields

<!-- UsageSnippet language="php" operationID="updateOrRemoveFundingSource" method="post" path="/funding-sources/{id}" example="card_updated_with_bank_fields" -->
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
    body: new Components\UpdateUnverifiedBank(
        routingNumber: '222222226',
        accountNumber: '123456789',
        bankAccountType: 'checking',
        name: 'Jane Doe’s Checking',
    )

);

if ($response->object !== null) {
    // handle response
}
```
### Example Usage: invalid_country_of_birth

<!-- UsageSnippet language="php" operationID="updateOrRemoveFundingSource" method="post" path="/funding-sources/{id}" example="invalid_country_of_birth" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Brick\DateTime\LocalDate;
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
    body: new Components\UpdateCardFundingSource(
        name: 'My Visa Debit Card',
        cardDetails: new Components\UpdateCardFundingSourceCardDetails(
            firstName: 'Jane',
            lastName: 'Doe',
            billingAddress: new Components\UpdateCardFundingSourceBillingAddress(
                address1: '123 Main St',
                address2: 'Apt 4B',
                address3: 'Unit 101',
                city: 'Dallas',
                stateProvinceRegion: 'TX',
                country: 'US',
                postalCode: '76034',
            ),
            dateOfBirth: LocalDate::parse('1990-01-15'),
            countryOfBirth: 'US',
            identification: new Components\UpdateCardFundingSourceIdentification(
                type: Components\UpdateCardFundingSourceType::Passport,
                number: 'P123456',
                country: 'GB',
            ),
        ),
    )

);

if ($response->object !== null) {
    // handle response
}
```
### Example Usage: no_fields_to_update

<!-- UsageSnippet language="php" operationID="updateOrRemoveFundingSource" method="post" path="/funding-sources/{id}" example="no_fields_to_update" -->
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

| Parameter                                                                                                                                                                                   | Type                                                                                                                                                                                        | Required                                                                                                                                                                                    | Description                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                        | *string*                                                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                          | Funding source unique identifier                                                                                                                                                            |
| `body`                                                                                                                                                                                      | [Components\UpdateUnverifiedBank\|Components\UpdateVerifiedBank\|Components\UpdateCardFundingSource\|Components\RemoveBank](../../Models/Operations/UpdateOrRemoveFundingSourceRequestBody.md) | :heavy_check_mark:                                                                                                                                                                          | Parameters to update a customer funding source                                                                                                                                              |

### Response

**[?Operations\UpdateOrRemoveFundingSourceResponse](../../Models/Operations/UpdateOrRemoveFundingSourceResponse.md)**

### Errors

| Error Type                                                 | Status Code                                                | Content Type                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| Errors\UpdateFundingSourceValidationError                  | 400                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\UpdateOrRemoveFundingSourceDwollaV1HalJSONException | 403                                                        | application/vnd.dwolla.v1.hal+json                         |
| Errors\APIException                                        | 4XX, 5XX                                                   | \*/\*                                                      |

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