# ClientTokens

## Overview

### Available Operations

* [create](#create) - Create a client token

## create

Create a client token for secure authentication within Dwolla Drop-in components. Requires a granular permission action and a Customer link to define what operations the end user can perform within the component. Returns a short-lived token for configuring client-side Drop-in components including customer creation, verification, funding source management, and payment processing. Essential for implementing secure, embeddable UI components without exposing application credentials to the frontend.

### Example Usage

<!-- UsageSnippet language="php" operationID="createClientToken" method="post" path="/client-tokens" -->
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

$request = new Operations\CreateClientTokenRequest(
    action: 'customer.update',
    links: new Operations\CreateClientTokenLinks(
        customer: new Operations\CreateClientTokenCustomer(
            href: 'https://api-sandbox.dwolla.com/customers/707177c3-bf15-4e7e-b37c-55c3898d9bf4',
        ),
    ),
);

$response = $sdk->clientTokens->create(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                  | Type                                                                                       | Required                                                                                   | Description                                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `$request`                                                                                 | [Operations\CreateClientTokenRequest](../../Models/Operations/CreateClientTokenRequest.md) | :heavy_check_mark:                                                                         | The request object to use for the request.                                                 |

### Response

**[?Operations\CreateClientTokenResponse](../../Models/Operations/CreateClientTokenResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\BadRequestError             | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |