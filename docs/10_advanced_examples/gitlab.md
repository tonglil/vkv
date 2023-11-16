# Gitlab CI

**This works for alpine based jobs**

Gitlab-CI Example for reading Secrets from Vault using vkv 

```yaml
variables:
  # vaults env vars
  # all of vault env vars are supported (https://developer.hashicorp.com/vault/docs/commands#environment-variables)
  # required:
  VAULT_ADDR: ""

  # optional
  VAULT_NAMESPACE: ""
  VAULT_TLS_SKIP_VERIFY: "true"

  # vkv env vars
  VKV_VERSION: "0.4.0" # https://github.com/FalcoSuessgott/vkv/releases/tag/v0.4.0
  VKV_EXPORT_PATH: "secrets"
  VKV_EXPORT_FORMAT: "export"

# default sets global default settings that are inherited to all jobs
default:
  # global before_scripts block
  before_script:
    # download vkv
    - apk add --no-cache curl
    - curl -LO "https://github.com/FalcoSuessgott/vkv/releases/download/v${VKV_VERSION}/vkv_${VKV_VERSION}_linux_amd64.apk"
    # install vkv
    - apk add --allow-untrusted ./vkv_${VKV_VERSION}_linux_amd64.apk
    # auth to vault (requires jwt auth configuration, https://docs.gitlab.com/ee/ci/examples/authenticating-with-hashicorp-vault/)
    - export VAULT_TOKEN="$(vault write -field=token auth/jwt/login role="${CI_PROJECT_ROOT_NAMESPACE}" jwt="${VAULT_JWT_TOKEN}")"
    # source env vars into shell
    - eval $(vkv export)
  # global jwt token 
  id_tokens:
    # set jwt aud field to gitlab ci server host
    VAULT_JWT_TOKEN:
      aud: "${CI_SERVER_HOST}"

# job
test:
  stage: test
  script:
    - make test 
```