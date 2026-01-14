# CreateCustomerFundingSource

Parameters for creating customer funding sources using different methods:
- Bank Account: Traditional method using routing/account numbers
- Exchange: Using IAV through exchange partners (Plaid, MX, etc.)
- Virtual Account: Creating Virtual Account Numbers (VANs)
- Card: Creating debit card funding sources using tokenized card data



## Supported Types

### `Components\CreateCustomerBankFundingSourceWithAccountNumbers`

```php
/**
* @var Components\CreateCustomerBankFundingSourceWithAccountNumbers
*/
Components\CreateCustomerBankFundingSourceWithAccountNumbers $value = /* values here */
```

### `Components\CreateCustomerBankFundingSourceWithPlaid`

```php
/**
* @var Components\CreateCustomerBankFundingSourceWithPlaid
*/
Components\CreateCustomerBankFundingSourceWithPlaid $value = /* values here */
```

### `Components\CreateCustomerExchangeFundingSource`

```php
/**
* @var Components\CreateCustomerExchangeFundingSource
*/
Components\CreateCustomerExchangeFundingSource $value = /* values here */
```

### `Components\CreateCustomerVirtualAccountFundingSource`

```php
/**
* @var Components\CreateCustomerVirtualAccountFundingSource
*/
Components\CreateCustomerVirtualAccountFundingSource $value = /* values here */
```

### `Components\CreateCustomerCardFundingSource`

```php
/**
* @var Components\CreateCustomerCardFundingSource
*/
Components\CreateCustomerCardFundingSource $value = /* values here */
```

