# RtpDetailsDestination

RTP destination details with network identifiers


## Fields

| Field                                                     | Type                                                      | Required                                                  | Description                                               | Example                                                   |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `remittanceData`                                          | *?string*                                                 | :heavy_minus_sign:                                        | Remittance information included in the transfer request   | ABC_123 Remittance Data                                   |
| `networkId`                                               | *?string*                                                 | :heavy_minus_sign:                                        | Unique identifier for the transfer within the RTP network | 20210617021214273T1BG27487110796028                       |
| `endToEndReferenceId`                                     | *?string*                                                 | :heavy_minus_sign:                                        | End-to-end reference identifier for the RTP transfer      | E2E-RTP-20210617-001                                      |