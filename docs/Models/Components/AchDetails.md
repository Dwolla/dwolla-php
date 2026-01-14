# AchDetails

ACH-specific details for the transfer. Present when transfer was processed via ACH network.


## Fields

| Field                                                                                 | Type                                                                                  | Required                                                                              | Description                                                                           |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `source`                                                                              | [?Components\Source](../../Models/Components/Source.md)                               | :heavy_minus_sign:                                                                    | Information sent to the source/originating bank account along with the transfer       |
| `destination`                                                                         | [?Components\AchDetailsDestination](../../Models/Components/AchDetailsDestination.md) | :heavy_minus_sign:                                                                    | Information sent to the destination/receiving bank account along with the transfer    |