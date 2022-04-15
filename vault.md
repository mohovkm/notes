### Before working we need to export address, where we will connect to:
```bash
export VAULT_ADDR=https://your_addres.com
```

### Enable auth method
```bash
vault auth enable approle
vault auth enable jwt
```

### Create token for policy
```bash
vault token create \
-policy=my-policy \
-display-name=token-name \
-orphan=true
```

### Create approle for policy
```bash
vault write auth/approle/role/{your-app-role} \
    secret_id_ttl="" \
    secret_id_num_uses=0 \
    token_policies="{your-policy}" \
    token_ttl=5m \
    token_max_ttl=10m
```

### Get role-id and secret-id
```bas
vault read auth/approle/role/{your-app-role}/role-id
```

```bash
vault write -f auth/approle/role/{your-app-role}/secret-id
```

[Link for description](https://www.vaultproject.io/api-docs/auth/approle#secret_id_bound_cidrs)

- `secret_id_ttl` (string: "") - Duration in either an integer number of seconds (3600) or an integer time unit (60m) after which any SecretID expires.
- `secret_id_num_uses` (integer: 0) - Number of times any particular SecretID can be used to fetch a token from this AppRole, after which the SecretID will expire. A value of zero will allow unlimited uses.
- `token_ttl` (integer: 0 or string: "") - The incremental lifetime for generated tokens. This current value of this will be referenced at renewal time.
- `token_max_ttl` (integer: 0 or string: "") - The maximum lifetime for generated tokens. This current value of this will be referenced at renewal time.
- `token_policies` (array: [] or comma-delimited string: "") - List of policies to encode onto generated tokens. Depending on the auth method, this list may be supplemented by user/group/other value

### List policy
```bash
vault policy list
```

### Read policy info
```bash
vault policy read {your-policy}
```

### Read token info
```bash
vault token lookup $YOUR_TOKEN
```

### List secret engines
```bash
vault secrets list -detailed
```

### Flow to integrate with Gitlab
https://docs.gitlab.com/ee/ci/secrets/
https://www.vaultproject.io/api-docs/auth/approle

1. Enable Vault jwt auth
2. Create policy for gitlab to read secrets and roles
```
path "auth/approle/role/*" {
    capabilities = [ "create", "read", "update" ]
}
```
3. Create/check bound claim
4. Get role_id from kv approle
5. Get secret_id from kv approle


