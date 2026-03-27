# SandboxSimulationVirtualAccountTransfersRequest

Simulate Virtual Account Number (VAN) / external transfers in Sandbox. Up to 10 transfers per request;
transfers are created and processed immediately. Successful response is 202 Accepted.



## Fields

| Field                                                                                                                     | Type                                                                                                                      | Required                                                                                                                  | Description                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `type`                                                                                                                    | *string*                                                                                                                  | :heavy_check_mark:                                                                                                        | Must be set to virtual for VAN transfer simulation.                                                                       |
| `transfers`                                                                                                               | array<[Components\SandboxSimulationVirtualTransferItem](../../Models/Components/SandboxSimulationVirtualTransferItem.md)> | :heavy_check_mark:                                                                                                        | Transfers to simulate (max 10 per request).                                                                               |