# Developer Policy vs Azure Built-in Roles Comparison

## Keys Permissions Comparison

### Developer Policy Keys Permissions:
- `Microsoft.KeyVault/vaults/keys/read`
- `Microsoft.KeyVault/vaults/keys/update/action`
- `Microsoft.KeyVault/vaults/keys/create/action`
- `Microsoft.KeyVault/vaults/keys/delete`

### Key Vault Crypto User Role (Additional Permissions):
- `Microsoft.KeyVault/vaults/keys/backup/action` ⭐ NEW - Ability to backup cryptographic keys
- `Microsoft.KeyVault/vaults/keys/encrypt/action` ⭐ NEW - Encrypt data using keys
- `Microsoft.KeyVault/vaults/keys/decrypt/action` ⭐ NEW - Decrypt data using keys
- `Microsoft.KeyVault/vaults/keys/wrap/action` ⭐ NEW - Wrap keys for secure transfer
- `Microsoft.KeyVault/vaults/keys/unwrap/action` ⭐ NEW - Unwrap keys
- `Microsoft.KeyVault/vaults/keys/sign/action` ⭐ NEW - Sign data with keys
- `Microsoft.KeyVault/vaults/keys/verify/action` ⭐ NEW - Verify signed data

**Summary**: Developer policy has basic CRUD operations for keys, while Key Vault Crypto User adds 7 additional cryptographic operations for backup, encryption/decryption, key wrapping, and digital signing.

## Secrets Permissions Comparison

### Developer Policy Secrets Permissions:
- `Microsoft.KeyVault/vaults/secrets/getSecret/action` - Retrieve secret values
- `Microsoft.KeyVault/vaults/secrets/readMetadata/action` - Read secret metadata
- `Microsoft.KeyVault/vaults/secrets/setSecret/action` - Create new secrets
- `Microsoft.KeyVault/vaults/secrets/update/action` - Update existing secrets
- `Microsoft.KeyVault/vaults/secrets/delete` - Delete secrets

### Key Vault Secrets Officer Role:
- `Microsoft.KeyVault/vaults/secrets/*` (includes ALL secrets operations including any future ones)

**Missing in Developer Policy*ull Cryptographic Operations**: When backup, encryption/decryption, signing are needed
✅ **Certificate Authority Management**: For managing CAs and certificate contacts
✅ **Azure Service Integration**: When RBAC, monitoring, deployment access is beneficial
✅ **Future-Proofing**: To automatically include new Microsoft operations
✅ **Administrative Roles**: For Key Vault administrators who need comprehensive access

### Hybrid Approach Recommendation:
Consider combining the developer policy with specific additional permissions for a balanced approach:
- Start with developer policy as base
- Add only the specific missing permissions needed (e.g., add `encrypt/action` if encryption is required)
- Avoid broad wildcards unless absolutely necessary

**Security Best Practice**: Always start with the most restrictive policy and add permissions only when a legitimate business need is identified.
