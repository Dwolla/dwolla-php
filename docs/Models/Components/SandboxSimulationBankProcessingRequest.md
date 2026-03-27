# SandboxSimulationBankProcessingRequest

Omit the request body or send an empty JSON object (`{}`). Triggers processing (or failure) for the last
500 bank transfers on the authorized application or Sandbox account, and initiated micro-deposits.
Successful response is 200 with a HAL body including total.



## Fields

| Field       | Type        | Required    | Description |
| ----------- | ----------- | ----------- | ----------- |