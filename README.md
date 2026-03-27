# dwolla-php

The official PHP SDK for the [Dwolla API](https://developers.dwolla.com/docs/api-reference). Supports server-side PHP calls to Dwolla’s endpoints with typed models, simple client helpers, and OAuth token handling to manage customers, funding sources, transfers, webhooks, and more.

> [!IMPORTANT]
> **Beta Release** – This SDK is currently in beta. We have run  smoke coverage (SDK build/clients) and a sandbox getting-started flow (root, list customers, create unverified customer, add funding source). Broader operation coverage and retry wiring are still in progress. Breaking changes may occur as we continue hardening and expanding tests; use with caution in production. We welcome beta users to integrate, report issues, and help us catch edge cases.

<!-- Start Summary [summary] -->
## Summary

Dwolla API: Dwolla API Documentation
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [dwolla-php](#dwolla-php)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

The SDK relies on [Composer](https://getcomposer.org/) to manage its dependencies.

To install the SDK and add it as a dependency to an existing `composer.json` file:
```bash
composer require "dwolla/dwolla-php"
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()->build();

$request = new Operations\CreateApplicationAccessTokenRequest(
    grantType: Operations\GrantType::ClientCredentials,
);
$requestSecurity = new Operations\CreateApplicationAccessTokenSecurity(
    basicAuth: '<YOUR_API_KEY_HERE>',
);

$response = $sdk->tokens->create(
    request: $request,
    security: $requestSecurity
);

if ($response->object !== null) {
    // handle response
}
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name                                         | Type   | Scheme                         |
| -------------------------------------------- | ------ | ------------------------------ |
| `clientID`<br/>`clientSecret`<br/>`tokenURL` | oauth2 | OAuth2 Client Credentials Flow |

You can set the security parameters through the `setSecurity` function on the `SDKBuilder` when initializing the SDK. For example:
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

### Per-Operation Security Schemes

Some operations in this SDK require the security scheme to be specified at the request level. For example:
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()->build();

$request = new Operations\CreateApplicationAccessTokenRequest(
    grantType: Operations\GrantType::ClientCredentials,
);
$requestSecurity = new Operations\CreateApplicationAccessTokenSecurity(
    basicAuth: '<YOUR_API_KEY_HERE>',
);

$response = $sdk->tokens->create(
    request: $request,
    security: $requestSecurity
);

if ($response->object !== null) {
    // handle response
}
```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Accounts](docs/sdks/accounts/README.md)

* [get](docs/sdks/accounts/README.md#get) - Retrieve account details

#### [Accounts.Exchanges](docs/sdks/accountsexchanges/README.md)

* [list](docs/sdks/accountsexchanges/README.md#list) - List exchanges for an account
* [create](docs/sdks/accountsexchanges/README.md#create) - Create an exchange for an account

#### [Accounts.FundingSources](docs/sdks/accountsfundingsources/README.md)

* [create](docs/sdks/accountsfundingsources/README.md#create) - Create a funding source for an account
* [list](docs/sdks/accountsfundingsources/README.md#list) - List funding sources for an account

#### [Accounts.MassPayments](docs/sdks/accountsmasspayments/README.md)

* [list](docs/sdks/accountsmasspayments/README.md#list) - List account mass payments

#### [Accounts.Transfers](docs/sdks/accountstransfers/README.md)

* [list](docs/sdks/accountstransfers/README.md#list) - List and search account transfers

### [BeneficialOwners](docs/sdks/beneficialowners/README.md)

* [get](docs/sdks/beneficialowners/README.md#get) - Retrieve beneficial owner
* [update](docs/sdks/beneficialowners/README.md#update) - Update beneficial owner
* [delete](docs/sdks/beneficialowners/README.md#delete) - Remove beneficial owner

#### [BeneficialOwners.Documents](docs/sdks/beneficialownersdocuments/README.md)

* [list](docs/sdks/beneficialownersdocuments/README.md#list) - List documents for beneficial owner
* [create](docs/sdks/beneficialownersdocuments/README.md#create) - Create a document for beneficial owner

### [BusinessClassifications](docs/sdks/businessclassifications/README.md)

* [list](docs/sdks/businessclassifications/README.md#list) - List business classifications
* [get](docs/sdks/businessclassifications/README.md#get) - Retrieve a business classification

### [ClientTokens](docs/sdks/clienttokens/README.md)

* [create](docs/sdks/clienttokens/README.md#create) - Create a client token

### [Customers](docs/sdks/customers/README.md)

* [list](docs/sdks/customers/README.md#list) - List and search customers
* [create](docs/sdks/customers/README.md#create) - Create a customer
* [get](docs/sdks/customers/README.md#get) - Retrieve a customer
* [update](docs/sdks/customers/README.md#update) - Update a customer
* [listAvailableConnections](docs/sdks/customers/README.md#listavailableconnections) - List available exchange connections

#### [Customers.BeneficialOwners](docs/sdks/customersbeneficialowners/README.md)

* [list](docs/sdks/customersbeneficialowners/README.md#list) - List customer beneficial owners
* [create](docs/sdks/customersbeneficialowners/README.md#create) - Create customer beneficial owner

#### [Customers.BeneficialOwnership](docs/sdks/beneficialownership/README.md)

* [get](docs/sdks/beneficialownership/README.md#get) - Retrieve beneficial ownership status
* [certify](docs/sdks/beneficialownership/README.md#certify) - Certify beneficial ownership

#### [Customers.Documents](docs/sdks/customersdocuments/README.md)

* [list](docs/sdks/customersdocuments/README.md#list) - List documents for customer
* [create](docs/sdks/customersdocuments/README.md#create) - Create a document for customer

#### [Customers.Exchanges](docs/sdks/customersexchanges/README.md)

* [list](docs/sdks/customersexchanges/README.md#list) - List exchanges for a customer
* [create](docs/sdks/customersexchanges/README.md#create) - Create an exchange for a customer

#### [Customers.ExchangeSessions](docs/sdks/customersexchangesessions/README.md)

* [create](docs/sdks/customersexchangesessions/README.md#create) - Create customer exchange session

#### [Customers.FundingSources](docs/sdks/customersfundingsources/README.md)

* [list](docs/sdks/customersfundingsources/README.md#list) - List customer funding sources
* [create](docs/sdks/customersfundingsources/README.md#create) - Create customer funding source

#### [Customers.Kba](docs/sdks/customerskba/README.md)

* [initiate](docs/sdks/customerskba/README.md#initiate) - Initiate a KBA session

#### [Customers.Labels](docs/sdks/customerslabels/README.md)

* [list](docs/sdks/customerslabels/README.md#list) - List labels for a customer
* [create](docs/sdks/customerslabels/README.md#create) - Create a label for a customer

#### [Customers.MassPayments](docs/sdks/customersmasspayments/README.md)

* [list](docs/sdks/customersmasspayments/README.md#list) - List mass payments for customer

#### [Customers.Transfers](docs/sdks/customerstransfers/README.md)

* [list](docs/sdks/customerstransfers/README.md#list) - List and search transfers for a customer

### [Documents](docs/sdks/documents/README.md)

* [get](docs/sdks/documents/README.md#get) - Retrieve a document

### [Events](docs/sdks/events/README.md)

* [list](docs/sdks/events/README.md#list) - List events
* [get](docs/sdks/events/README.md#get) - Retrieve event

### [ExchangePartners](docs/sdks/exchangepartners/README.md)

* [list](docs/sdks/exchangepartners/README.md#list) - List exchange partners
* [get](docs/sdks/exchangepartners/README.md#get) - Retrieve exchange partner

### [Exchanges](docs/sdks/exchanges/README.md)

* [get](docs/sdks/exchanges/README.md#get) - Retrieve exchange resource

#### [Exchanges.ExchangeSessions](docs/sdks/exchangesexchangesessions/README.md)

* [createReAuth](docs/sdks/exchangesexchangesessions/README.md#createreauth) - Create re-authentication exchange session

### [ExchangeSessions](docs/sdks/exchangesessions/README.md)

* [get](docs/sdks/exchangesessions/README.md#get) - Retrieve exchange session

### [FundingSources](docs/sdks/fundingsources/README.md)

* [get](docs/sdks/fundingsources/README.md#get) - Retrieve a funding source
* [updateOrRemove](docs/sdks/fundingsources/README.md#updateorremove) - Update or remove a funding source
* [getVanRouting](docs/sdks/fundingsources/README.md#getvanrouting) - Retrieve VAN account and routing numbers

#### [FundingSources.Balance](docs/sdks/balance/README.md)

* [get](docs/sdks/balance/README.md#get) - Retrieve funding source balance

#### [FundingSources.MicroDeposits](docs/sdks/microdeposits/README.md)

* [get](docs/sdks/microdeposits/README.md#get) - Retrieve micro-deposits details
* [initiate](docs/sdks/microdeposits/README.md#initiate) - Initiate micro-deposits
* [verify](docs/sdks/microdeposits/README.md#verify) - Verify micro-deposits

#### [FundingSources.OnDemandTransferAuthorizations](docs/sdks/ondemandtransferauthorizations/README.md)

* [create](docs/sdks/ondemandtransferauthorizations/README.md#create) - Create an on-demand transfer authorization

### [Kba](docs/sdks/kba/README.md)

* [getQuestions](docs/sdks/kba/README.md#getquestions) - Retrieve KBA Questions
* [verify](docs/sdks/kba/README.md#verify) - Verify KBA Questions

### [Labels](docs/sdks/labels/README.md)

* [get](docs/sdks/labels/README.md#get) - Retrieve a label
* [remove](docs/sdks/labels/README.md#remove) - Remove a label

#### [Labels.LedgerEntries](docs/sdks/ledgerentries/README.md)

* [list](docs/sdks/ledgerentries/README.md#list) - List label ledger entries
* [create](docs/sdks/ledgerentries/README.md#create) - Create a label ledger entry
* [get](docs/sdks/ledgerentries/README.md#get) - Retrieve a label ledger entry

#### [Labels.Reallocations](docs/sdks/reallocations/README.md)

* [create](docs/sdks/reallocations/README.md#create) - Create a label reallocation
* [get](docs/sdks/reallocations/README.md#get) - Retrieve a label reallocation

### [MassPayments](docs/sdks/masspayments/README.md)

* [create](docs/sdks/masspayments/README.md#create) - Initiate a mass payment
* [get](docs/sdks/masspayments/README.md#get) - Retrieve a mass payment
* [update](docs/sdks/masspayments/README.md#update) - Update a mass payment

#### [MassPayments.Items](docs/sdks/items/README.md)

* [list](docs/sdks/items/README.md#list) - List items for a mass payment
* [get](docs/sdks/items/README.md#get) - Retrieve mass payment item

### [Root](docs/sdks/root/README.md)

* [get](docs/sdks/root/README.md#get) - root

### [SandboxSimulations](docs/sdks/sandboxsimulations/README.md)

* [simulate](docs/sdks/sandboxsimulations/README.md#simulate) - Sandbox simulations (bank transfers, VAN transfers, or customer verification directives)

### [Tokens](docs/sdks/tokens/README.md)

* [create](docs/sdks/tokens/README.md#create) - Create an application access token

### [Transfers](docs/sdks/transfers/README.md)

* [create](docs/sdks/transfers/README.md#create) - Initiate a transfer
* [get](docs/sdks/transfers/README.md#get) - Retrieve a transfer
* [cancel](docs/sdks/transfers/README.md#cancel) - Cancel a transfer

#### [Transfers.Failure](docs/sdks/failure/README.md)

* [get](docs/sdks/failure/README.md#get) - Retrieve a transfer failure reason

#### [Transfers.Fees](docs/sdks/fees/README.md)

* [list](docs/sdks/fees/README.md#list) - List fees for a transfer

### [Webhooks](docs/sdks/webhooks/README.md)

* [get](docs/sdks/webhooks/README.md#get) - Retrieve a webhook
* [retry](docs/sdks/webhooks/README.md#retry) - Retry a webhook

#### [Webhooks.Retries](docs/sdks/retries/README.md)

* [list](docs/sdks/retries/README.md#list) - List retries for a webhook

### [WebhookSubscriptions](docs/sdks/webhooksubscriptions/README.md)

* [list](docs/sdks/webhooksubscriptions/README.md#list) - List webhook subscriptions
* [create](docs/sdks/webhooksubscriptions/README.md#create) - Create a webhook subscription
* [get](docs/sdks/webhooksubscriptions/README.md#get) - Retrieve a webhook subscription
* [update](docs/sdks/webhooksubscriptions/README.md#update) - Update a webhook subscription
* [delete](docs/sdks/webhooksubscriptions/README.md#delete) - Delete a webhook subscription

#### [WebhookSubscriptions.Webhooks](docs/sdks/webhooksubscriptionswebhooks/README.md)

* [list](docs/sdks/webhooksubscriptionswebhooks/README.md#list) - List webhooks for a webhook subscription

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or throw an exception.

By default an API error will raise a `Errors\APIException` exception, which has the following properties:

| Property       | Type                                    | Description           |
|----------------|-----------------------------------------|-----------------------|
| `$message`     | *string*                                | The error message     |
| `$statusCode`  | *int*                                   | The HTTP status code  |
| `$rawResponse` | *?\Psr\Http\Message\ResponseInterface*  | The raw HTTP response |
| `$body`        | *string*                                | The response content  |

When custom error responses are specified for an operation, the SDK may also throw their associated exception. You can refer to respective *Errors* tables in SDK docs for more details on possible exception types for each operation. For example, the `create` method throws the following exceptions:

| Error Type                   | Status Code | Content Type     |
| ---------------------------- | ----------- | ---------------- |
| Errors\UnauthorizedException | 401         | application/json |
| Errors\APIException          | 4XX, 5XX    | \*/\*            |

### Example

```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Errors;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()->build();

try {
    $request = new Operations\CreateApplicationAccessTokenRequest(
        grantType: Operations\GrantType::ClientCredentials,
    );
    $requestSecurity = new Operations\CreateApplicationAccessTokenSecurity(
        basicAuth: '<YOUR_API_KEY_HERE>',
    );

    $response = $sdk->tokens->create(
        request: $request,
        security: $requestSecurity
    );

    if ($response->object !== null) {
        // handle response
    }
} catch (Errors\UnauthorizedExceptionThrowable $e) {
    // handle $e->$container data
    throw $e;
} catch (Errors\APIException $e) {
    // handle default exception
    throw $e;
}
```
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally using the `setServer(string $serverName)` builder method when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name      | Server                           | Description       |
| --------- | -------------------------------- | ----------------- |
| `prod`    | `https://api.dwolla.com`         | Production server |
| `sandbox` | `https://api-sandbox.dwolla.com` | Sandbox server    |

#### Example

```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()
    ->setServer('prod')
    ->build();

$request = new Operations\CreateApplicationAccessTokenRequest(
    grantType: Operations\GrantType::ClientCredentials,
);
$requestSecurity = new Operations\CreateApplicationAccessTokenSecurity(
    basicAuth: '<YOUR_API_KEY_HERE>',
);

$response = $sdk->tokens->create(
    request: $request,
    security: $requestSecurity
);

if ($response->object !== null) {
    // handle response
}
```

### Override Server URL Per-Client

The default server can also be overridden globally using the `setServerUrl(string $serverUrl)` builder method when initializing the SDK client instance. For example:
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()
    ->setServerURL('https://api.dwolla.com')
    ->build();

$request = new Operations\CreateApplicationAccessTokenRequest(
    grantType: Operations\GrantType::ClientCredentials,
);
$requestSecurity = new Operations\CreateApplicationAccessTokenSecurity(
    basicAuth: '<YOUR_API_KEY_HERE>',
);

$response = $sdk->tokens->create(
    request: $request,
    security: $requestSecurity
);

if ($response->object !== null) {
    // handle response
}
```
<!-- End Server Selection [server] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

## Maturity

This SDK is currently in beta; expect potential breaking changes while we stabilize. We follow [Semantic Versioning](https://semver.org/) for published versions, but until GA we recommend pinning to an exact version and validating in your environment.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release.
