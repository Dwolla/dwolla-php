# Exchanges.ExchangeSessions

## Overview

### Available Operations

* [createReAuth](#createreauth) - Create re-authentication exchange session

## createReAuth

Creates a re-authentication exchange session to refresh a user's bank account connection when their existing authorization is no longer valid. Required when receiving an UpdateCredentials error during bank balance checks or when user re-authentication is needed.

### Example Usage

<!-- UsageSnippet language="php" operationID="createReAuthExchangeSession" method="post" path="/exchanges/{id}/exchange-sessions" -->
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



$response = $sdk->exchanges->exchangeSessions->createReAuth(
    id: '<id>',
    body: new Components\CreateReAuthExchangeSessionWithRedirect(
        links: new Components\CreateReAuthExchangeSessionWithRedirectLinks(
            redirectUrl: new Components\CreateReAuthExchangeSessionWithRedirectRedirectUrl(
                href: 'https://example.com/app123',
            ),
        ),
    )

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                 | Type                                                                                                                                                                      | Required                                                                                                                                                                  | Description                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                      | *string*                                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                        | Exchange's unique identifier                                                                                                                                              |
| `body`                                                                                                                                                                    | [Components\CreateReAuthExchangeSessionForWeb\|Components\CreateReAuthExchangeSessionWithRedirect\|null](../../Models/Operations/CreateReAuthExchangeSessionRequestBody.md) | :heavy_minus_sign:                                                                                                                                                        | Request body containing the redirect URL.<br/>Required for:<br/>- Plaid mobile sessions<br/>Not required for:<br/>- Plaid web sessions<br/>                               |

### Response

**[?Operations\CreateReAuthExchangeSessionResponse](../../Models/Operations/CreateReAuthExchangeSessionResponse.md)**

### Errors

| Error Type                                                           | Status Code                                                          | Content Type                                                         |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Errors\CreateReAuthExchangeSessionBadRequestDwollaV1HalJSONException | 400                                                                  | application/vnd.dwolla.v1.hal+json                                   |
| Errors\CreateReAuthExchangeSessionForbiddenDwollaV1HalJSONException  | 403                                                                  | application/vnd.dwolla.v1.hal+json                                   |
| Errors\APIException                                                  | 4XX, 5XX                                                             | \*/\*                                                                |