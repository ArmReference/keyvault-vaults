# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
name           | Yes      | Name of resource
VaultProperties | Yes      | Properties of the vault
DependsOn      | No       | Pass dependencies

### name

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Name of resource

### VaultProperties

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Properties of the vault

### DependsOn

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Pass dependencies

## Outputs

Name | Type | Description
---- | ---- | -----------
vaults | object | Azure KeyVault template

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
        "template": "reference/vaults.json"
    },
    "parameters": {
        "name": {
            "value": ""
        },
        "VaultProperties": {
            "value": {}
        },
        "DependsOn": {
            "value": []
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
