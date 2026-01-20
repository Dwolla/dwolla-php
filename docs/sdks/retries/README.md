# Webhooks.Retries

## Overview

### Available Operations

* [list](#list) - List retries for a webhook

## list

Retrieve all retry attempts for a specific webhook including timestamps and delivery details. Returns a list of retry attempts with unique identifiers, timestamps, and links to the parent webhook with total count. Essential for tracking webhook delivery failures, analyzing retry patterns, and debugging webhook notification issues to ensure reliable event processing.

### Example Usage

<!-- UsageSnippet language="php" operationID="listWebhookRetries" method="get" path="/webhooks/{id}/retries" -->
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



$response = $sdk->webhooks->retries->list(
    id: '<id>'
);

if ($response->webhookRetries !== null) {
    // handle response
}
```

### Parameters

| Parameter                 | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `id`                      | *string*                  | :heavy_check_mark:        | Webhook unique identifier |

### Response

**[?Operations\ListWebhookRetriesResponse](../../Models/Operations/ListWebhookRetriesResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |