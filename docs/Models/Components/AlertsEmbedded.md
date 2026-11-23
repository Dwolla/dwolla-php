# AlertsEmbedded


## Fields

| Field                                                                                     | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `alerts`                                                                                  | array<[Components\Alert](../../Models/Components/Alert.md)>                               | :heavy_check_mark:                                                                        | Up to `limit` alerts (25 by default), newest first. Empty when the account has no alerts. |