<!-- Start SDK Example Usage [usage] -->
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