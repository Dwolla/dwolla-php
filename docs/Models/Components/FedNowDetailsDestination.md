# FedNowDetailsDestination

FedNow destination details with network identifiers


## Fields

| Field                                                        | Type                                                         | Required                                                     | Description                                                  | Example                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `remittanceData`                                             | *?string*                                                    | :heavy_minus_sign:                                           | Remittance information included in the transfer request      | ABC_123 Remittance Data                                      |
| `networkId`                                                  | *?string*                                                    | :heavy_minus_sign:                                           | Unique identifier for the transfer within the FedNow network | 20240115123456789FEDNOW123456                                |
| `endToEndReferenceId`                                        | *?string*                                                    | :heavy_minus_sign:                                           | End-to-end reference identifier for the FedNow transfer      | E2E-FEDNOW-20240115-001                                      |