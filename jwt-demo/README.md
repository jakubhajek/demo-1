# Traefik Enterprise

## Applying static configuration

```
teectl apply --file=./static.yaml
```

# JWT
## Issuing JWT token

```
JWT=$(curl -L -X POST "https://keycloak.<REPLACE_ME>/auth/realms/traefiklabs/protocol/openid-connect/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "client_id=demo-app" \
  -d "client_assertion_type=" \
  -d "grant_type=password" \
  -d "client_secret=$CLIENT_SECRET" \
  -d "scope=openid" \
  -d "username=$KEYCLOAK_USR" \
  -d "password=$KEYCLOAK_PWD" | jq -r '.access_token')
```


## testing the app protected thorugh JWT Auth

```
curl -H "Authorization: Bearer $JWT" https://app.<REPLACE_ME>/  -Iv
```