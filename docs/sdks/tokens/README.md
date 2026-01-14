# Tokens

## Overview

Operations related to Application Access Tokens

### Available Operations

* [create](#create) - Create an application access token

## create

Generate an application access token using OAuth 2.0 client credentials flow for server-to-server authentication. Requires client ID and secret sent via Basic authentication header with grant_type=client_credentials in the request body. Returns a bearer access token with expiration time for authenticating API requests scoped to your application. Essential for secure API access.

### Example Usage

<!-- UsageSnippet language="php" operationID="createApplicationAccessToken" method="post" path="/token" -->
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

### Parameters

| Parameter                                                                                                          | Type                                                                                                               | Required                                                                                                           | Description                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| `$request`                                                                                                         | [Operations\CreateApplicationAccessTokenRequest](../../Models/Operations/CreateApplicationAccessTokenRequest.md)   | :heavy_check_mark:                                                                                                 | The request object to use for the request.                                                                         |
| `security`                                                                                                         | [Operations\CreateApplicationAccessTokenSecurity](../../Models/Operations/CreateApplicationAccessTokenSecurity.md) | :heavy_check_mark:                                                                                                 | The security requirements to use for the request.                                                                  |

### Response

**[?Operations\CreateApplicationAccessTokenResponse](../../Models/Operations/CreateApplicationAccessTokenResponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| Errors\UnauthorizedException | 401                          | application/json             |
| Errors\APIException          | 4XX, 5XX                     | \*/\*                        |