# SimulateBankTransferProcessingResponseBody

Success. **Bank transfer processing** returns HAL with `total`. **Customer verification directives**
return HAL `_links.self` and `errorCode` (retrieve the Customer for `_embedded.errors`).



## Supported Types

### `Components\SandboxSimulationBankProcessingResponse`

```php
/**
* @var Components\SandboxSimulationBankProcessingResponse
*/
Components\SandboxSimulationBankProcessingResponse $value = /* values here */
```

### `Components\SandboxSimulationCustomerVerificationResponse`

```php
/**
* @var Components\SandboxSimulationCustomerVerificationResponse
*/
Components\SandboxSimulationCustomerVerificationResponse $value = /* values here */
```

