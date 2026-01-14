# DwollaBalanceResponse

Response for retrieving balance of a Dwolla Balance funding source


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             | Example                                                                 |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `links`                                                                 | array<string, [Components\HalLink](../../Models/Components/HalLink.md)> | :heavy_check_mark:                                                      | N/A                                                                     |                                                                         |
| `balance`                                                               | [Operations\Balance](../../Models/Operations/Balance.md)                | :heavy_check_mark:                                                      | N/A                                                                     |                                                                         |
| `total`                                                                 | [Operations\Total](../../Models/Operations/Total.md)                    | :heavy_check_mark:                                                      | N/A                                                                     |                                                                         |
| `lastUpdated`                                                           | *string*                                                                | :heavy_check_mark:                                                      | N/A                                                                     | 2017-04-18T15:20:25.880Z                                                |