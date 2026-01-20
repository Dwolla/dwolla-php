# WebhookSubscriptions

## Overview

### Available Operations

* [list](#list) - List webhook subscriptions
* [create](#create) - Create a webhook subscription
* [get](#get) - Retrieve a webhook subscription
* [update](#update) - Update a webhook subscription
* [delete](#delete) - Delete a webhook subscription

## list

Retrieve all webhook subscriptions that belong to an application including their configuration details and status. Returns subscription details including webhook endpoints, status, creation dates, and links to associated webhooks with total count. Essential for webhook management and monitoring subscription health.

### Example Usage

<!-- UsageSnippet language="php" operationID="listWebhookSubscriptions" method="get" path="/webhook-subscriptions" -->
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



$response = $sdk->webhookSubscriptions->list(

);

if ($response->object !== null) {
    // handle response
}
```

### Response

**[?Operations\ListWebhookSubscriptionsResponse](../../Models/Operations/ListWebhookSubscriptionsResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\ForbiddenError              | 403                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## create

Create a webhook subscription to deliver webhook notifications to a specified URL endpoint for your application. Requires a destination URL where Dwolla will send notifications and a secret key for webhook validation and security. Returns the location of the created subscription resource. Essential for establishing real-time event notifications and automated integrations with Dwolla's payment processing events.

### Example Usage

<!-- UsageSnippet language="php" operationID="createWebhookSubscription" method="post" path="/webhook-subscriptions" -->
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

$request = new Operations\CreateWebhookSubscriptionRequest(
    url: 'http://myapplication.com/webhooks',
    secret: 'sshhhhhh',
);

$response = $sdk->webhookSubscriptions->create(
    request: $request
);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                  | Type                                                                                                       | Required                                                                                                   | Description                                                                                                |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `$request`                                                                                                 | [Operations\CreateWebhookSubscriptionRequest](../../Models/Operations/CreateWebhookSubscriptionRequest.md) | :heavy_check_mark:                                                                                         | The request object to use for the request.                                                                 |

### Response

**[?Operations\CreateWebhookSubscriptionResponse](../../Models/Operations/CreateWebhookSubscriptionResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Errors\InvalidUrlFormatError        | 400                                 | application/vnd.dwolla.v1.hal+json  |
| Errors\SecretTooLongError           | 400                                 | application/vnd.dwolla.v1.hal+json  |
| Errors\MaxSubscriptionsReachedError | 400                                 | application/vnd.dwolla.v1.hal+json  |
| Errors\ForbiddenError               | 403                                 | application/vnd.dwolla.v1.hal+json  |
| Errors\NotFoundError                | 404                                 | application/vnd.dwolla.v1.hal+json  |
| Errors\APIException                 | 4XX, 5XX                            | \*/\*                               |

## get

Retrieve detailed information for a specific webhook subscription by its unique identifier. Returns subscription configuration including URL endpoint, creation date, and links to associated webhooks for comprehensive subscription management. Essential for monitoring webhook subscription status and accessing webhook delivery history.

### Example Usage

<!-- UsageSnippet language="php" operationID="getWebhookSubscription" method="get" path="/webhook-subscriptions/{id}" -->
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



$response = $sdk->webhookSubscriptions->get(
    id: '<id>'
);

if ($response->webhookSubscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                              | Type                                   | Required                               | Description                            |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| `id`                                   | *string*                               | :heavy_check_mark:                     | Webhook subscription unique identifier |

### Response

**[?Operations\GetWebhookSubscriptionResponse](../../Models/Operations/GetWebhookSubscriptionResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## update

Update a webhook subscription to pause or resume webhook delivery notifications. Allows toggling the paused status to temporarily stop webhook notifications without deleting the subscription. Returns the updated subscription resource with the new paused status. Use this endpoint to manage webhook delivery during maintenance or troubleshooting periods.

### Example Usage

<!-- UsageSnippet language="php" operationID="updateWebhookSubscription" method="post" path="/webhook-subscriptions/{id}" -->
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

$body = new Operations\UpdateWebhookSubscriptionRequestBody(
    paused: true,
);

$response = $sdk->webhookSubscriptions->update(
    id: '<id>',
    body: $body

);

if ($response->webhookSubscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                          | Type                                                                                                               | Required                                                                                                           | Description                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                               | *string*                                                                                                           | :heavy_check_mark:                                                                                                 | Webhook unique identifier                                                                                          |
| `body`                                                                                                             | [Operations\UpdateWebhookSubscriptionRequestBody](../../Models/Operations/UpdateWebhookSubscriptionRequestBody.md) | :heavy_check_mark:                                                                                                 | Parameters to update a webhook subscription                                                                        |

### Response

**[?Operations\UpdateWebhookSubscriptionResponse](../../Models/Operations/UpdateWebhookSubscriptionResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\BadRequestError             | 400                                | application/vnd.dwolla.v1.hal+json |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## delete

Delete a webhook subscription to permanently remove webhook notifications for your application. This action stops all future webhook deliveries and cannot be undone. Returns the deleted subscription resource for confirmation. Use this endpoint when webhook notifications are no longer needed or when cleaning up unused subscriptions.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete" method="delete" path="/webhook-subscriptions/{id}" -->
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



$response = $sdk->webhookSubscriptions->delete(
    id: '<id>'
);

if ($response->webhookSubscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                 | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `id`                      | *string*                  | :heavy_check_mark:        | Webhook unique identifier |

### Response

**[?Operations\DeleteResponse](../../Models/Operations/DeleteResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |