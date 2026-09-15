# UpdateCardFundingSource

Request body for updating a debit card funding source.

Every field is optional, but you must provide at least one. Only the fields you send are
changed; omitted fields keep their current values. Use this operation to add or update the
optional cardholder identity fields - `dateOfBirth`, `countryOfBirth`, and `identification` -
on a card funding source that already exists.

Card funding sources cannot be updated with bank fields such as `routingNumber`,
`accountNumber`, `bankAccountType`, or `bankAccountHolderType`.



## Fields

| Field                                                                                                           | Type                                                                                                            | Required                                                                                                        | Description                                                                                                     | Example                                                                                                         |
| --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `name`                                                                                                          | *?string*                                                                                                       | :heavy_minus_sign:                                                                                              | Arbitrary nickname for the debit card funding source. Must be 50 characters or less.                            | My Visa Debit Card                                                                                              |
| `cardDetails`                                                                                                   | [?Components\UpdateCardFundingSourceCardDetails](../../Models/Components/UpdateCardFundingSourceCardDetails.md) | :heavy_minus_sign:                                                                                              | Cardholder details to add or update. Provide only the fields you want to change.                                |                                                                                                                 |