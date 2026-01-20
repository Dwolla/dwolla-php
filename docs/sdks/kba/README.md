# Kba

## Overview

Operations related to Knowledge-Based Authentication

### Available Operations

* [getQuestions](#getquestions) - Retrieve KBA Questions
* [verify](#verify) - Verify KBA Questions

## getQuestions

Returns the KBA questions for a specific KBA session. The questions are used to verify the customer's identity during the KBA process.

### Example Usage

<!-- UsageSnippet language="php" operationID="getKbaQuestions" method="get" path="/kba/{id}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();



$response = $sdk->kba->getQuestions(
    id: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                           | Type                                                | Required                                            | Description                                         |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| `id`                                                | *string*                                            | :heavy_check_mark:                                  | The ID of the KBA session to retrieve questions for |

### Response

**[?Operations\GetKbaQuestionsResponse](../../Models/Operations/GetKbaQuestionsResponse.md)**

### Errors

| Error Type                                     | Status Code                                    | Content Type                                   |
| ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| Errors\ForbiddenError                          | 403                                            | application/vnd.dwolla.v1.hal+json             |
| Errors\GetKbaQuestionsDwollaV1HalJSONException | 404                                            | application/vnd.dwolla.v1.hal+json             |
| Errors\APIException                            | 4XX, 5XX                                       | \*/\*                                          |

## verify

Submits customer answers to KBA questions for identity verification. Requires four question-answer pairs with questionId and answerId values. Returns verification status indicating whether the customer passed or failed the KBA authentication.

### Example Usage

<!-- UsageSnippet language="php" operationID="verifyKbaQuestions" method="post" path="/kba/{id}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Dwolla;
use Dwolla\Models\Components;
use Dwolla\Models\Operations;

$sdk = Dwolla\Dwolla::builder()
    ->setSecurity(
        new Components\Security(
            clientID: '<YOUR_CLIENT_ID_HERE>',
            clientSecret: '<YOUR_CLIENT_SECRET_HERE>',
        )
    )
    ->build();

$body = new Operations\VerifyKbaQuestionsRequestBody(
    answers: [],
);

$response = $sdk->kba->verify(
    id: '<id>',
    body: $body

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `id`                                                                                                 | *string*                                                                                             | :heavy_check_mark:                                                                                   | The id of the KBA session to verify questions for.                                                   |
| `body`                                                                                               | [Operations\VerifyKbaQuestionsRequestBody](../../Models/Operations/VerifyKbaQuestionsRequestBody.md) | :heavy_check_mark:                                                                                   | Parameters for verifying KBA questions                                                               |

### Response

**[?Operations\VerifyKbaQuestionsResponse](../../Models/Operations/VerifyKbaQuestionsResponse.md)**

### Errors

| Error Type                                        | Status Code                                       | Content Type                                      |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| Errors\ForbiddenError                             | 403                                               | application/vnd.dwolla.v1.hal+json                |
| Errors\InvalidKbaSessionError                     | 403                                               | application/vnd.dwolla.v1.hal+json                |
| Errors\ExpiredKbaSessionError                     | 403                                               | application/vnd.dwolla.v1.hal+json                |
| Errors\VerifyKbaQuestionsDwollaV1HalJSONException | 404                                               | application/vnd.dwolla.v1.hal+json                |
| Errors\APIException                               | 4XX, 5XX                                          | \*/\*                                             |