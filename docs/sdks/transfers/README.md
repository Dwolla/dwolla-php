# Transfers

## Overview

Operations related to Transfers

### Available Operations

* [create](#create) - Initiate a transfer
* [get](#get) - Retrieve a transfer
* [cancel](#cancel) - Cancel a transfer

## create

Initiate a transfer between funding sources from a Dwolla Account or API Customer resource. Supports ACH, Instant Payments (RTP/FedNow), Push-to-Debit Card, and wire transfers with optional expedited clearing, facilitator fees, metadata, and correlation IDs for enhanced traceability. Includes idempotency key support to prevent duplicate transfers and extensive customization options for addenda records and processing channels. Returns the location of the created transfer resource for tracking and management.

### Example Usage

<!-- UsageSnippet language="php" operationID="initiateTransfer" method="post" path="/transfers" -->
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

$body = new Operations\InitiateTransferRequestBody(
    links: new Operations\InitiateTransferLinks(),
    amount: new Components\TransferAmount(
        value: '5.00',
        currency: 'USD',
    ),
    fees: [
        new Operations\Fee(
            amount: new Components\TransferAmount(
                value: '5.00',
                currency: 'USD',
            ),
        ),
    ],
    rtpDetails: new Operations\RtpDetails(
        destination: new Operations\RtpDetailsDestination(
            remittanceData: 'ABC_123 Remittance Data',
        ),
    ),
    instantDetails: new Operations\InstantDetails(
        destination: new Operations\InstantDetailsDestination(
            remittanceData: 'ABC_123 Remittance Data',
        ),
    ),
    processingChannel: new Operations\InitiateTransferProcessingChannel(
        destination: Operations\DestinationEnum::Instant,
    ),
);

$response = $sdk->transfers->create(
    body: $body,
    idempotencyKey: '19051a62-3403-11e6-ac61-9e71128cae77'

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      | Example                                                                                          |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `body`                                                                                           | [Operations\InitiateTransferRequestBody](../../Models/Operations/InitiateTransferRequestBody.md) | :heavy_check_mark:                                                                               | Parameters to initiate a transfer                                                                |                                                                                                  |
| `idempotencyKey`                                                                                 | *?string*                                                                                        | :heavy_minus_sign:                                                                               | N/A                                                                                              | 19051a62-3403-11e6-ac61-9e71128cae77                                                             |

### Response

**[?Operations\InitiateTransferResponse](../../Models/Operations/InitiateTransferResponse.md)**

### Errors

| Error Type                                                | Status Code                                               | Content Type                                              |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| Errors\SourceNotFoundError                                | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\ReceiverNotFoundError                              | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidSourceFundingSourceError                    | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\SenderRestrictedError                              | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\ReceiverRestrictedError                            | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidMetadataError                               | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\OperationBlockedError                              | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidAmountLimitError                            | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\CannotParseAmountError                             | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InsufficientFundsError                             | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\FacilitatorFeeAccountNotFoundError                 | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\FacilitatorFeeSumTooLargeError                     | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\FacilitatorFeeBelowMinimumError                    | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\HighRiskError                                      | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\IncompatibleHoldingsError                          | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\DirectAccountWithoutBankError                      | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\SourceSameAsDestinationError                       | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidFacilitatorError                            | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidFacilitatorFeeCollectFromError              | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidFacilitatorFeeCollectFromCombinationError   | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidDestinationFundingSourceError               | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidOrRemovedCardDestinationError               | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidFacilitatorFeeAmountError                   | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WeeklyReceiveLimitReachedError                     | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidDestinationClearingTypeError                | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidAmountForDestinationClearingTypeError       | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidCorrelationIdError                          | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\SourceAddendaMaxLengthError                        | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\DestinationAddendaMaxLengthError                   | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\AchAddendaEntriesNotEnabledForAccountError         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\PointOfSaleAddendaEntriesNotEnabledForAccountError | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\IncompatibleAddendaEntriesError                    | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidPointOfSaleAddendaIdentificationCodeError   | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidPointOfSaleAddendaSerialNumberError         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidPointOfSaleAddendaDateError                 | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidPointOfSaleAddendaAddressError              | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidPointOfSaleAddendaCityError                 | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidPointOfSaleAddendaStateError                | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\TransferExpiredForFeeError                         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidFeeOdfiError                                | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidSourceBankAccountTypeError                  | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidDestinationBankAccountTypeError             | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\IncompatibleSourceAndDestinationTypesError         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\SourceNotCardNetworkSettlementError                | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\CardSourceNotAllowedError                          | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\IncompatibleSourceForRtpDestinationError           | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidAmountForDestinationProcessingChannelError  | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\RtpFacilitatorFeeNotSupportedError                 | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\RtpUnverifiedSenderNotSupportedError               | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\RtpPersonalToPersonalNotSupportedError             | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\DestinationProcessingChannelNotSupportedError      | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\DestinationRemittanceDataMaxLengthError            | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidAmountError                         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidFundingSourceError                  | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawAccountRestrictedError                     | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidAmountForClearingTypeError          | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidWireBeneficiaryLocalityError        | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidWireBeneficiaryRegionError          | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidWireBeneficiaryCountryError         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawInvalidWireOriginatorToBeneficiaryError    | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawProcessingChannelNotSupportedError         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawRtpUnverifiedSenderNotSupportedError       | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WithdrawRtpPersonalWithdrawalNotSupportedError     | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\DepositAccountRestrictedError                      | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WireInvalidImadError                               | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WireAccountRestrictedError                         | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WireNotEnabledError                                | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\WireAccountNotFoundError                           | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\PrefundingSourceNotAllowedError                    | 400                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidAttemptToFacilitateFundsError               | 403                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidAttemptToPayInFundsError                    | 403                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\InvalidAttemptToPayOutFundsError                   | 403                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\RtpAccountSettingNotEnabledError                   | 403                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\TooManyRequestsErrorError                          | 429                                                       | application/vnd.dwolla.v1.hal+json                        |
| Errors\APIException                                       | 4XX, 5XX                                                  | \*/\*                                                     |

## get

Retrieve detailed information for a specific transfer by its unique identifier belonging to an Account or Customer. Returns transfer status, amount, creation date, clearing details, and links to source and destination funding sources for complete transaction tracking. Includes cancellation links when applicable and references to related funding transfers. Essential for monitoring transfer lifecycle and transaction reconciliation.

### Example Usage

<!-- UsageSnippet language="php" operationID="getTransfer" method="get" path="/transfers/{id}" -->
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



$response = $sdk->transfers->get(
    id: '<id>'
);

if ($response->transfer !== null) {
    // handle response
}
```

### Parameters

| Parameter                      | Type                           | Required                       | Description                    |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| `id`                           | *string*                       | :heavy_check_mark:             | ID of transfer to be retrieved |

### Response

**[?Operations\GetTransferResponse](../../Models/Operations/GetTransferResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## cancel

Cancel a pending transfer by setting its status to cancelled. Only transfers in pending status can be cancelled before processing begins. Returns the updated transfer resource with cancelled status. Use this endpoint to stop a bank transfer from further processing.

### Example Usage

<!-- UsageSnippet language="php" operationID="cancelTransfer" method="post" path="/transfers/{id}" -->
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

$body = new Operations\CancelTransferRequestBody();

$response = $sdk->transfers->cancel(
    id: '<id>',
    body: $body

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                    | Type                                                                                         | Required                                                                                     | Description                                                                                  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `id`                                                                                         | *string*                                                                                     | :heavy_check_mark:                                                                           | ID of transfer                                                                               |
| `body`                                                                                       | [Operations\CancelTransferRequestBody](../../Models/Operations/CancelTransferRequestBody.md) | :heavy_check_mark:                                                                           | Parameters to cancel a transfer                                                              |

### Response

**[?Operations\CancelTransferResponse](../../Models/Operations/CancelTransferResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\BadRequestError             | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\StatusInvalidError          | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\StatusNotAllowedError       | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |