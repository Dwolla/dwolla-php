# Alerts

## Overview

Operations related to Alerts

### Available Operations

* [list](#list) - List alerts
* [get](#get) - Retrieve alert
* [update](#update) - Resolve alert

## list

Returns the alerts for your Dwolla account, newest first. Alerts notify you of activity that may need your attention, such as unusual transfer activity for one of your Customers. When an alert needs a response from you, it includes an `actionRequired` object whose `description` explains what to do. Each alert's `_links.self` is the alert's resource URI.

Alerts are in active development and must be enabled for your account. If alerts aren't enabled, listing alerts returns an empty list. To enable alerts, please [reach out to Dwolla](https://www.dwolla.com/contact?b=apidocs).

Requires an application access token for your account.

**Pagination** — Alerts are returned using cursor-based pagination. Each page holds up to `limit` alerts (25 by default, 200 at most):
- Request `GET /alerts` to get the first page, which contains your newest alerts. Add `limit` to choose the page size, such as `GET /alerts?limit=50`.
- Follow the `next` link in `_links` to get the next page of older alerts. `next` is omitted on the last page.
- Follow the `prev` link in `_links` to go back to the previous page of newer alerts. `prev` is omitted on the first page.

The `next` and `prev` link URLs contain an opaque cursor. Use the cursor exactly as returned; don't build, parse, or modify it. A modified cursor returns a `400 InvalidQueryParameter` error.

**Page size** — The `next` and `prev` links always include `limit`, even if your request omitted it, so following them keeps the same page size. To change the page size partway through, send the `next` or `prev` link with a different `limit` value; the new page size is honored. `limit` is the only parameter you may change between pages.

**Filtering by status** — To list only `open` or only `resolved` alerts, add the `status` query parameter to your first request, such as `GET /alerts?status=open`. Omit `status` to list every alert.
- The `next` and `prev` links keep the filter. Their URLs include `status` along with the cursor, so follow them as returned.
- A cursor belongs to the filtered list it came from. Sending a cursor with a different or missing `status` returns a `400 ValidationError` error.
- To change the filter, start again from `GET /alerts?status=…` without a cursor.


### Example Usage: first_page

<!-- UsageSnippet language="php" operationID="listAlerts" method="get" path="/alerts" example="first_page" -->
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



$responses = $sdk->alerts->list(
    limit: 25,
    status: Operations\Status::Open

);


foreach ($responses as $response) {
    if ($response->statusCode === 200) {
        // handle response
    }
}
```
### Example Usage: open_alerts_page

<!-- UsageSnippet language="php" operationID="listAlerts" method="get" path="/alerts" example="open_alerts_page" -->
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



$responses = $sdk->alerts->list(
    limit: 25,
    status: Operations\Status::Open

);


foreach ($responses as $response) {
    if ($response->statusCode === 200) {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                | Type                                                                                                                                     | Required                                                                                                                                 | Description                                                                                                                              | Example                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `limit`                                                                                                                                  | *?int*                                                                                                                                   | :heavy_minus_sign:                                                                                                                       | Maximum number of results to return                                                                                                      | 25                                                                                                                                       |
| `status`                                                                                                                                 | [?Operations\Status](../../Models/Operations/Status.md)                                                                                  | :heavy_minus_sign:                                                                                                                       | Filter by alert status. Case-insensitive. Specify at most once. Omit to list every alert. The `next` and `prev` links keep this filter.<br/> | open                                                                                                                                     |

### Response

**[?Operations\ListAlertsResponse](../../Models/Operations/ListAlertsResponse.md)**

### Errors

| Error Type                                            | Status Code                                           | Content Type                                          |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| Errors\ListAlertsInvalidQueryParameterError           | 400                                                   | application/vnd.dwolla.v1.hal+json                    |
| Errors\ListAlertsValidationError                      | 400                                                   | application/vnd.dwolla.v1.hal+json                    |
| Errors\ListAlertsUnauthorizedDwollaV1HalJSONException | 401                                                   | application/vnd.dwolla.v1.hal+json                    |
| Errors\ListAlertsForbiddenDwollaV1HalJSONException    | 403                                                   | application/vnd.dwolla.v1.hal+json                    |
| Errors\APIException                                   | 4XX, 5XX                                              | \*/\*                                                 |

## get

Returns a single alert for your Dwolla account. Alerts notify you of activity that may need your attention, such as unusual transfer activity for one of your Customers. When an alert needs a response from you, it includes an `actionRequired` object whose `description` explains what to do.

Alerts are in active development and must be enabled for your account. To enable alerts, please [reach out to Dwolla](https://www.dwolla.com/contact?b=apidocs).

If you can resolve the alert, its `_links` include a `resolve` link. To resolve it, send `{"status": "resolved"}` to `POST /alerts/{id}`.

Requires an application access token for your account. Returns a `404 NotFound` error if the alert doesn't exist.


### Example Usage

<!-- UsageSnippet language="php" operationID="getAlert" method="get" path="/alerts/{id}" example="open_unusual_transfer_activity" -->
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



$response = $sdk->alerts->get(
    id: 'd4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42'
);

if ($response->alert !== null) {
    // handle response
}
```

### Parameters

| Parameter                            | Type                                 | Required                             | Description                          | Example                              |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `id`                                 | *string*                             | :heavy_check_mark:                   | The alert's unique identifier.       | d4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42 |

### Response

**[?Operations\GetAlertResponse](../../Models/Operations/GetAlertResponse.md)**

### Errors

| Error Type                                          | Status Code                                         | Content Type                                        |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| Errors\GetAlertUnauthorizedDwollaV1HalJSONException | 401                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\GetAlertForbiddenDwollaV1HalJSONException    | 403                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\NotFoundError                                | 404                                                 | application/vnd.dwolla.v1.hal+json                  |
| Errors\APIException                                 | 4XX, 5XX                                            | \*/\*                                               |

## update

Resolves an alert for your Dwolla account by setting its `status` to `resolved`. Returns the updated alert, with `status` set to `resolved`, the `resolved` timestamp set, and no `resolve` link.

You can only resolve an alert that has a `resolve` link in its `_links`. The link is present only while the alert is `open` and can be resolved, so check for it before resolving an alert.

Resolving an alert changes only the alert itself: its `status` becomes `resolved`, and `actionRequired` is removed when no further action is needed. It doesn't release holds on transfers or change the Customer, and it doesn't take the action described in `actionRequired` for you.

Resolving an alert that's already resolved, or that you can't resolve, returns a `400 ValidationError` error with the embedded code `NotAllowed`, and the alert isn't changed.

Alerts are in active development and must be enabled for your account. To enable alerts, please [reach out to Dwolla](https://www.dwolla.com/contact?b=apidocs).

Requires an application access token for your account. Returns a `404 NotFound` error if the alert doesn't exist.


### Example Usage: resolve

<!-- UsageSnippet language="php" operationID="updateAlert" method="post" path="/alerts/{id}" example="resolve" -->
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

$body = new Components\UpdateAlert();

$response = $sdk->alerts->update(
    id: 'd4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42',
    body: $body

);

if ($response->alert !== null) {
    // handle response
}
```
### Example Usage: resolved_unusual_transfer_activity

<!-- UsageSnippet language="php" operationID="updateAlert" method="post" path="/alerts/{id}" example="resolved_unusual_transfer_activity" -->
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

$body = new Components\UpdateAlert();

$response = $sdk->alerts->update(
    id: 'd4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42',
    body: $body

);

if ($response->alert !== null) {
    // handle response
}
```
### Example Usage: status_invalid

<!-- UsageSnippet language="php" operationID="updateAlert" method="post" path="/alerts/{id}" example="status_invalid" -->
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

$body = new Components\UpdateAlert();

$response = $sdk->alerts->update(
    id: 'd4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42',
    body: $body

);

if ($response->alert !== null) {
    // handle response
}
```
### Example Usage: status_not_allowed

<!-- UsageSnippet language="php" operationID="updateAlert" method="post" path="/alerts/{id}" example="status_not_allowed" -->
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

$body = new Components\UpdateAlert();

$response = $sdk->alerts->update(
    id: 'd4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42',
    body: $body

);

if ($response->alert !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                        | Type                                                             | Required                                                         | Description                                                      | Example                                                          |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `id`                                                             | *string*                                                         | :heavy_check_mark:                                               | The alert's unique identifier.                                   | d4bd3a1e-7c6e-4e8a-9a5c-3b2f9d7e1a42                             |
| `body`                                                           | [Components\UpdateAlert](../../Models/Components/UpdateAlert.md) | :heavy_check_mark:                                               | Parameters to resolve an alert                                   |                                                                  |

### Response

**[?Operations\UpdateAlertResponse](../../Models/Operations/UpdateAlertResponse.md)**

### Errors

| Error Type                                             | Status Code                                            | Content Type                                           |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Errors\UpdateAlertStatusInvalidError                   | 400                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\UpdateAlertStatusNotAllowedError                | 400                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\UpdateAlertUnauthorizedDwollaV1HalJSONException | 401                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\UpdateAlertForbiddenDwollaV1HalJSONException    | 403                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\NotFoundError                                   | 404                                                    | application/vnd.dwolla.v1.hal+json                     |
| Errors\APIException                                    | 4XX, 5XX                                               | \*/\*                                                  |