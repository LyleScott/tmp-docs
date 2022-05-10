# Authentication

For auth, we've standardized on a VTG's (Video Technology Group) unified auth (UAuth)
pattern against an internal auth server. If you do not have an account, request one in
`#i-vidtech-airspace` or `#i-vidtech-devops`.

The auth workflow follows the typical JWT token pattern:

1. fetch an access token by logging in with valid credentials
2. use this token on all other requests by including it in a header

## Fetch Access Token

If you have access to `curl`, you may verify your credentials can fetch an access_token.

```bash
# replace your.user.name and your.user.password
curl --location --request POST \
  'https://airspace.cbsivideo.com/v1/login' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'username=your.user.name' \
  --data-urlencode 'password=your.user.password'
```

If successful, you'll see a response similar to:

```json
{"access_token":"eyJhInR5cCI6I....rsLyuQ","token_type":"Bearer"}
```

## Use Access Token

Attach the access token to any further requests.

```shell
curl --location --request GET \
  'https://airspace.cbsivideo.com/v1/organizations' \
  --header 'Authorization: Bearer {{access_token}}'
```

## JWT Anatomy

While this is irrelevant to most, the JWT anatomy is similar to the following.

A token lasts for 4 hours.

### JWT Header

```json
{
  "alg": "RS256",
  "typ": "JWT"
}
```

`RS256` uses a public/private key to validate the token behind the scenes. If you need
to verify tokens yourself, use the unified auth server's public key.

```shell
curl --location --request GET \
  'https://uauth-prod-api.cbsivideo.com/auth/public_key'
```

### JWT Payload

You can use https://jwt.io to decode the JWT token into its parts.

```json
{
  "sub": "your.user.name",
  "groups": "[]",
  "iat": 1651856158,
  "exp": 1651870558,
  "iss": "CBS-VTG"
}
```

- `sub` - your username
- `iat` - issued at epoch timestamp
- `exp` - expires at epoch timestamp
- `iss` - issuer
