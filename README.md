# acurl 🔓
A simple authentication wrapper for cURL

## Usage
Usage is exactly like curl, with one exception.
If the first argument equals one of the blocks in the config file, it will not be sent to curl, but rather load the configuration.
- `acurl <curl args>` will use default configuration.
- `acurl test <curl args>` will use default + test configuration.

Example:

`acurl test https://example.com/ -iXPOST -H 'Content-Type: application/json' -d '{"x": 10}'`

## Configuration

acurl requires a config at `~/.config/acurl/config.json` with a few fields.

Currently only json responses are supported.
Here is an example where we fetch tokens from auth0:

```javascript
{
  "default": {
    "authorization_url": "https://example.eu.auth0.com/oauth/token",
    "request_body": {
      "grant_type": "client_credentials",
      "client_id": "default_client_id",
      "client_secret": "default_client_secret",
      "audience": "api_identifier"
    },
    "token_field": "access_token",
    "expiration_field": "expires_in"
  }
}
```

### Multiple configurations
Any other names than default can be used to override `default` configuration when calling `acurl`
Ex: `acurl test https://example.com/ -XPOST -H 'Content-Type: application/json' -d '{"x": 1}'`

Will use configuration from `test` block to override. 
So it will use `test_client_id` and `test_client_secret` rather than the default of `default_client_id` and `default_client_secret`.


```javascript
{
  "test": {
    "client_id": "test_client_id",
    "client_secret": "test_client_secret"
  },
  "default": {
    "authorization_url": "https://example.eu.auth0.com/oauth/token",
    "request_body": {
      "grant_type": "client_credentials",
      "client_id": "default_client_id",
      "client_secret": "default_client_secret",
      "audience": "api_identifier"
    },
    "token_field": "access_token",
    "expiration_field": "expires_in"
  }
}
```


