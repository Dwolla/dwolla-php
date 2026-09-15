# CreateCustomerExchangeSessionForCardCardDetails

Optional. Opt into Account Name Inquiry (ANI) for this session by providing the expected
cardholder name. Retrieve the resulting match on the Exchange with `GET /exchanges/{id}`.



## Fields

| Field                                                                                | Type                                                                                 | Required                                                                             | Description                                                                          | Example                                                                              |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `firstName`                                                                          | *string*                                                                             | :heavy_check_mark:                                                                   | The cardholder first name you expect on the card.                                    | John                                                                                 |
| `lastName`                                                                           | *string*                                                                             | :heavy_check_mark:                                                                   | The cardholder last name you expect on the card.                                     | Doe                                                                                  |
| `accountNameInquiry`                                                                 | *bool*                                                                               | :heavy_check_mark:                                                                   | Set to `true` to request an Account Name Inquiry (ANI) name-match check on the card. | true                                                                                 |