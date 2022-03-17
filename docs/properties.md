# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
tenantId       | Yes      | The Azure Active Directory tenant ID that should be used for authenticating requests to the key vault. - globally unique identifier
sku            | Yes      | SKU details
accessPolicies | No       | An array of 0 to 16 identities that have access to the key vault. All identities in the array must use the same tenant ID as the key vault's tenant ID.
enabledForDeployment | No       | Property to specify whether Azure Virtual Machines are permitted to retrieve certificates stored as secrets from the key vault.
enabledForDiskEncryption | No       | Property to specify whether Azure Disk Encryption is permitted to retrieve secrets from the vault and unwrap keys.
enabledForTemplateDeployment | No       | Property to specify whether Azure Resource Manager is permitted to retrieve secrets from the key vault.
enableSoftDelete | No       | Property to specify whether the 'soft delete' functionality is enabled for this key vault. It does not accept false value.

### tenantId

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

The Azure Active Directory tenant ID that should be used for authenticating requests to the key vault. - globally unique identifier

### sku

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

SKU details

### accessPolicies

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An array of 0 to 16 identities that have access to the key vault. All identities in the array must use the same tenant ID as the key vault's tenant ID.

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
        "template": "reference/properties.json"
    },
    "parameters": {
        "tenantId": {
            "value": ""
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
