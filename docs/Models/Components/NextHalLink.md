# NextHalLink

Link to the next page of older alerts. Keeps the `status` filter, if any, and always includes `limit`. Omitted on the last page. Use the URL as-is, changing only `limit` if you want a different page size.


## Fields

| Field                              | Type                               | Required                           | Description                        | Example                            |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `href`                             | *?string*                          | :heavy_minus_sign:                 | N/A                                | https://api.dwolla.com             |
| `type`                             | *?string*                          | :heavy_minus_sign:                 | N/A                                | application/vnd.dwolla.v1.hal+json |
| `resourceType`                     | *?string*                          | :heavy_minus_sign:                 | N/A                                | resource-type                      |