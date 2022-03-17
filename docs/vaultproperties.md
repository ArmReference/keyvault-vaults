# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
tenantId       | Yes      | The Azure Active Directory tenant ID that should be used for authenticating requests to the key vault. - globally unique identifier
softDeleteRetentionInDays | No       | softDelete data retention days. It accepts >=7 and <=90.
publicNetworkAccess | Yes      | Property to specify whether the vault will accept traffic from public internet. If set to 'disabled' all traffic except private endpoint traffic and that that originates from trusted services will be blocked. This will override the set firewall rules, meaning that even if the firewall rules are present we will not honor the rules.
networkAcls    | No       | A set of rules governing the network accessibility of a vault.
sku            | Yes      | SKU details
accessPolicies | No       | An array of 0 to 1024 identities that have access to the key vault. All identities in the array must use the same tenant ID as the key vault's tenant ID. 
enabledForDeployment | No       | Property to specify whether Azure Virtual Machines are permitted to retrieve certificates stored as secrets from the key vault.
enabledForDiskEncryption | No       | Property to specify whether Azure Disk Encryption is permitted to retrieve secrets from the vault and unwrap keys.
enabledForTemplateDeployment | No       | Property to specify whether Azure Resource Manager is permitted to retrieve secrets from the key vault.
enablePurgeProtection | No       | Property specifying whether protection against purge is enabled for this vault. Setting this property to true activates protection against purge for this vault and its content - only the Key Vault service may initiate a hard, irrecoverable deletion. The setting is effective only if soft delete is also enabled. Enabling this functionality is irreversible - that is, the property does not accept false as its value.
enableRbacAuthorization | No       | Property that controls how data actions are authorized. When true, the key vault will use Role Based Access Control (RBAC) for authorization of data actions, and the access policies specified in vault properties will be ignored. When false, the key vault will use the access policies specified in vault properties, and any policy stored on Azure Resource Manager will be ignored. If null or not specified, the vault is created with the default value of false. Note that management actions are always authorized with RBAC.
enableSoftDelete | No       | Property to specify whether the 'soft delete' functionality is enabled for this key vault. It does not accept false value.

### tenantId

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

The Azure Active Directory tenant ID that should be used for authenticating requests to the key vault. - globally unique identifier

### softDeleteRetentionInDays

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

softDelete data retention days. It accepts >=7 and <=90.

- Default value: `7`

### publicNetworkAccess

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Property to specify whether the vault will accept traffic from public internet. If set to 'disabled' all traffic except private endpoint traffic and that that originates from trusted services will be blocked. This will override the set firewall rules, meaning that even if the firewall rules are present we will not honor the rules.

- Allowed values: `Enabled`, `Disabled`

### networkAcls

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

A set of rules governing the network accessibility of a vault.

### sku

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

SKU details

### accessPolicies

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An array of 0 to 1024 identities that have access to the key vault. All identities in the array must use the same tenant ID as the key vault's tenant ID. 

### enabledForDeployment

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Property to specify whether Azure Virtual Machines are permitted to retrieve certificates stored as secrets from the key vault.

- Default value: `False`

### enabledForDiskEncryption

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Property to specify whether Azure Disk Encryption is permitted to retrieve secrets from the vault and unwrap keys.

- Default value: `False`

### enabledForTemplateDeployment

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Property to specify whether Azure Resource Manager is permitted to retrieve secrets from the key vault.

- Default value: `False`

### enablePurgeProtection

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Property specifying whether protection against purge is enabled for this vault. Setting this property to true activates protection against purge for this vault and its content - only the Key Vault service may initiate a hard, irrecoverable deletion. The setting is effective only if soft delete is also enabled. Enabling this functionality is irreversible - that is, the property does not accept false as its value.

- Default value: `True`

### enableRbacAuthorization

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Property that controls how data actions are authorized. When true, the key vault will use Role Based Access Control (RBAC) for authorization of data actions, and the access policies specified in vault properties will be ignored. When false, the key vault will use the access policies specified in vault properties, and any policy stored on Azure Resource Manager will be ignored. If null or not specified, the vault is created with the default value of false. Note that management actions are always authorized with RBAC.

- Default value: `False`

### enableSoftDelete

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Property to specify whether the 'soft delete' functionality is enabled for this key vault. It does not accept false value.

- Default value: `False`

## Outputs

Name | Type | Description
---- | ---- | -----------
properties | object | Azure KeyVault Properties

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
        "template": "reference/vaultproperties.json"
    },
    "parameters": {
        "tenantId": {
            "value": ""
        },
        "softDeleteRetentionInDays": {
            "value": 7
        },
        "publicNetworkAccess": {
            "value": ""
        },
        "networkAcls": {
            "value": {}
        },
        "sku": {
            "value": {}
        },
        "accessPolicies": {
            "value": []
        },
        "enabledForDeployment": {
            "value": false
        },
        "enabledForDiskEncryption": {
            "value": false
        },
        "enabledForTemplateDeployment": {
            "value": false
        },
        "enablePurgeProtection": {
            "value": true
        },
        "enableRbacAuthorization": {
            "value": false
        },
        "enableSoftDelete": {
            "value": false
        }
    }
}
```

### Command line

#### PowerShell

```powershell
New-AzResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile <path-to-template> -TemplateParameterFile <path-to-templateparameter>
```

#### Azure CLI

```text
az group deployment create --name <deployment-name> --resource-group <resource-group-name> --template-file <path-to-template> --parameters @<path-to-templateparameterfile>
```
