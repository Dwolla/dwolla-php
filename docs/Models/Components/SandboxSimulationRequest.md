# SandboxSimulationRequest

Bank transfer processing (omit body or `{}`), VAN transfer simulation (`type` virtual + transfers), or
verification directive simulation (`type` customer-verification, customer link, and errorCode). Typed bodies
are mutually exclusive; use only an omitted body or `{}` for bank processing.



## Supported Types

### `Components\SandboxSimulationVirtualAccountTransfersRequest`

```php
/**
* @var Components\SandboxSimulationVirtualAccountTransfersRequest
*/
Components\SandboxSimulationVirtualAccountTransfersRequest $value = /* values here */
```

### `Components\SandboxSimulationCustomerVerificationRequest`

```php
/**
* @var Components\SandboxSimulationCustomerVerificationRequest
*/
Components\SandboxSimulationCustomerVerificationRequest $value = /* values here */
```

### `Components\SandboxSimulationBankProcessingRequest`

```php
/**
* @var Components\SandboxSimulationBankProcessingRequest
*/
Components\SandboxSimulationBankProcessingRequest $value = /* values here */
```

