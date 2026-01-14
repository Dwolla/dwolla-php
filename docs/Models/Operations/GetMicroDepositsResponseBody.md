# GetMicroDepositsResponseBody

successful operation


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             | Example                                                                 |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `links`                                                                 | array<string, [Components\HalLink](../../Models/Components/HalLink.md)> | :heavy_minus_sign:                                                      | N/A                                                                     |                                                                         |
| `created`                                                               | [\DateTime](https://www.php.net/manual/en/class.datetime.php)           | :heavy_minus_sign:                                                      | N/A                                                                     | 2022-12-30T20:56:53.000Z                                                |
| `status`                                                                | *?string*                                                               | :heavy_minus_sign:                                                      | N/A                                                                     | failed                                                                  |
| `failure`                                                               | [?Operations\Failure](../../Models/Operations/Failure.md)               | :heavy_minus_sign:                                                      | N/A                                                                     |                                                                         |