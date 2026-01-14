# Webhooks

## Overview

Operations related to Webhooks

### Available Operations

* [get](#get) - Retrieve a webhook
* [retry](#retry) - Retry a webhook

## get

Retrieve detailed information for a specific webhook by its unique identifier including delivery attempts and response data. Returns webhook details with topic, account information, delivery attempts containing request/response history, and links to subscription and retry resources. Essential for debugging webhook delivery issues, analyzing response data, and monitoring notification processing status.

### Example Usage

<!-- UsageSnippet language="php" operationID="getWebhook" method="get" path="/webhooks/{id}" -->
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



$response = $sdk->webhooks->get(
    id: '<id>'
);

if ($response->webhook !== null) {
    // handle response
}
```

### Parameters

| Parameter                 | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `id`                      | *string*                  | :heavy_check_mark:        | Webhook unique identifier |

### Response

**[?Operations\GetWebhookResponse](../../Models/Operations/GetWebhookResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## retry

Retry a webhook by its unique identifier to redeliver the notification to your endpoint. Creates a new retry attempt and returns the location of the new webhook resource. Essential for recovering from webhook delivery failures and ensuring reliable event notification processing in your application.

### Example Usage

<!-- UsageSnippet language="php" operationID="retryWebhook" method="post" path="/webhooks/{id}/retries" -->
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



$response = $sdk->webhooks->retry(
    id: '<id>'
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                 | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `id`                      | *string*                  | :heavy_check_mark:        | Webhook unique identifier |

### Response

**[?Operations\RetryWebhookResponse](../../Models/Operations/RetryWebhookResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |