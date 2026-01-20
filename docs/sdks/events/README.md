# Events

## Overview

Operations related to Events

### Available Operations

* [list](#list) - List events
* [get](#get) - Retrieve event

## list

Returns a paginated list of events representing state changes to resources in your Dwolla application. Events track actions on customers, transfers, funding sources, and other resources, sorted by creation date (newest first). Events are retained for 30 days and are essential for webhook notifications and system activity monitoring.

### Example Usage

<!-- UsageSnippet language="php" operationID="listEvents" method="get" path="/events" -->
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



$response = $sdk->events->list(

);

if ($response->events !== null) {
    // handle response
}
```

### Parameters

| Parameter                  | Type                       | Required                   | Description                |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `limit`                    | *?int*                     | :heavy_minus_sign:         | How many results to return |
| `offset`                   | *?int*                     | :heavy_minus_sign:         | How many results to skip   |

### Response

**[?Operations\ListEventsResponse](../../Models/Operations/ListEventsResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |

## get

Returns detailed information for a specific event representing a state change that occurred on a resource in your Dwolla application. Includes the event topic, timestamp, resource links, and correlation ID if applicable.

### Example Usage

<!-- UsageSnippet language="php" operationID="getEvent" method="get" path="/events/{id}" -->
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



$response = $sdk->events->get(
    id: '<id>'
);

if ($response->event !== null) {
    // handle response
}
```

### Parameters

| Parameter                      | Type                           | Required                       | Description                    |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| `id`                           | *string*                       | :heavy_check_mark:             | ID of application event to get |

### Response

**[?Operations\GetEventResponse](../../Models/Operations/GetEventResponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| Errors\NotFoundError               | 404                                | application/vnd.dwolla.v1.hal+json |
| Errors\APIException                | 4XX, 5XX                           | \*/\*                              |