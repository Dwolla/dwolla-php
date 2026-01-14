# ListMassPaymentsRequest


## Fields

| Field                               | Type                                | Required                            | Description                         | Example                             |
| ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- |
| `id`                                | *string*                            | :heavy_check_mark:                  | Account's unique identifier         |                                     |
| `limit`                             | *?int*                              | :heavy_minus_sign:                  | Maximum number of results to return | 25                                  |
| `offset`                            | *?int*                              | :heavy_minus_sign:                  | How many results to skip.           | 0                                   |
| `correlationId`                     | *?string*                           | :heavy_minus_sign:                  | Correlation ID to search by.        |                                     |