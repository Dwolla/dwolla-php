# SimulateBankTransferProcessingResponseBody

Success. **Bank transfer processing** returns HAL with `total`. **Customer verification directives**
return HAL `_links.self` and `errorCode` (retrieve the Customer for `_embedded.errors`).



## Supported Types

### `Components\SandboxSimulationBankProcessingResponse`

```php
/**
* @var \Dwolla\Models\Components\SandboxSimulationBankProcessingResponse
*/
Components\SandboxSimulationBankProcessingResponse $value = /* values here */
```

### `Components\SandboxSimulationCustomerVerificationResponse`

```php
/**
* @var \Dwolla\Models\Components\SandboxSimulationCustomerVerificationResponse
*/
Components\SandboxSimulationCustomerVerificationResponse $value = /* values here */
```

