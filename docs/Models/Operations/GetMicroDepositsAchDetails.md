# GetMicroDepositsAchDetails

ACH details for each micro-deposit. Optional; only returned when ACH details are available for the micro-deposits. `deposit1` or `deposit2` may be omitted if details for that deposit are unavailable.


## Fields

| Field                                                       | Type                                                        | Required                                                    | Description                                                 |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `deposit1`                                                  | [?Operations\Deposit1](../../Models/Operations/Deposit1.md) | :heavy_minus_sign:                                          | ACH details for the first micro-deposit                     |
| `deposit2`                                                  | [?Operations\Deposit2](../../Models/Operations/Deposit2.md) | :heavy_minus_sign:                                          | ACH details for the second micro-deposit                    |