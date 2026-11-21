# ResolveHalLink

Resolves the alert. Present only while the alert is `open` and can be resolved. To resolve the alert, send a `POST` request to this link with `{"status": "resolved"}`. Check for this link before resolving an alert.


## Fields

| Field                              | Type                               | Required                           | Description                        | Example                            |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `href`                             | *?string*                          | :heavy_minus_sign:                 | N/A                                | https://api.dwolla.com             |
| `type`                             | *?string*                          | :heavy_minus_sign:                 | N/A                                | application/vnd.dwolla.v1.hal+json |
| `resourceType`                     | *?string*                          | :heavy_minus_sign:                 | N/A                                | resource-type                      |