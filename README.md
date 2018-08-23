# acurl 🔓
A simple authentication wrapper for cURL

## Usage
acurl requires a config at ~/.config/acurl/config.json with a few fields.

Here is an example where we fetch tokens from auth0.
Currently only json responses are supported.

```javascript
{
    "authorization_url": "https://example.eu.auth0.com/oauth/token",
    "request_body": {
        "grant_type": "client_credentials",
        "client_id": "client_id",
        "client_secret": "client_secret",
        "audience": "api_identifier"
    },
    "token_field": "access_token",
    "expiration_field": "expires_in"
}
```


