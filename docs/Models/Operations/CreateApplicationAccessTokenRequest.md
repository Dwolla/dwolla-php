# CreateApplicationAccessTokenRequest

OAuth get token request. Client credentials are sent in the Authorization header using Basic authentication.


## Fields

| Field                                                        | Type                                                         | Required                                                     | Description                                                  | Example                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `grantType`                                                  | [Operations\GrantType](../../Models/Operations/GrantType.md) | :heavy_check_mark:                                           | Must be set to "client_credentials"                          | client_credentials                                           |