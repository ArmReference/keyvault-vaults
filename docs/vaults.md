# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
name           | Yes      | Name of resource
location       | No       | The supported Azure location where the key vault should be created.
VaultProperties | Yes      | Properties of the vault
tags           | No       | The tags that will be assigned to the key vault.
DependsOn      | No       | Pass dependencies

### name

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Name of resource

### location

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The supported Azure location where the key vault should be created.

- Default value: `[resourceGroup().location]`

### VaultProperties

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Properties of the vault

### tags

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The tags that will be assigned to the key vault.

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
    "contentVersion": "1.0.0.1",
    "metadata": {
        "template": "reference/vaults.json"
    },
    "parameters": {
        "name": {
            "value": ""
        },
        "location": {
            "value": "[resourceGroup().location]"
        },
        "VaultProperties": {
            "value": {}
        },
        "tags": {
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
