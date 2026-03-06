# ExternalProviderSessionData

Present for Checkout.com exchange sessions (Push to Card / debit card flow).
Use these fields to initialize the Checkout.com Flow component for card capture.



## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `id`                                                                 | *?string*                                                            | :heavy_minus_sign:                                                   | Checkout.com payment session ID (e.g. ps_xxx).                       | ps_39vhHjFxZuJRKOw5Hexbnv39fC7                                       |
| `paymentSessionSecret`                                               | *?string*                                                            | :heavy_minus_sign:                                                   | Checkout.com payment session secret.                                 | pss_2400dd88-171d-4a9c-bebf-e06b56d59bb6                             |
| `paymentSessionToken`                                                | *?string*                                                            | :heavy_minus_sign:                                                   | Checkout.com payment session token (base64) for Flow initialization. | YmFzZTY0:eyJpZCI6InBzXzM5dmhIakZ4WnVKUktPdzVIZXhibnYzOWZDNyIs...     |