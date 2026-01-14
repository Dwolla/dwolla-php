# WebhookSubscriptions.Webhooks

## Overview

### Available Operations

* [list](#list) - List webhooks for a webhook subscription

## list

Retrieve all fired webhooks for a specific webhook subscription with comprehensive filtering and pagination support. Returns webhook delivery history including topics, attempts, request/response details, and delivery status over a rolling 30-day period. Supports filtering by resource ID, date ranges, and pagination parameters for detailed webhook delivery analysis. Critical for debugging webhook delivery issues and monitoring event notification success rates.

### Example Usage

<!-- UsageSnippet language="php" operationID="listWebhooks" method="get" path="/webhook-subscriptions/{id}/webhooks" -->
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

$request = new Operations\ListWebhooksRequest(
    id: '<id>',
);

$response = $sdk->webhookSubscriptions->webhooks->list(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `$request`                                                                       | [Operations\ListWebhooksRequest](../../Models/Operations/ListWebhooksRequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |

### Response

**[?Operations\ListWebhooksResponse](../../Models/Operations/ListWebhooksResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |