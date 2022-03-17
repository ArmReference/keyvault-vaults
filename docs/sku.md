# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
family         | Yes      | SKU family name
name           | Yes      | SKU name to specify whether the key vault is a standard vault or a premium vault.

### family

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

SKU family name

- Allowed values: `A`

### name

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

SKU name to specify whether the key vault is a standard vault or a premium vault.

- Allowed values: `Standard`, `Premium`

## Outputs

Name | Type | Description
---- | ---- | -----------
sku  | object | Azure KeyVault SKU

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.1",
    "metadata": {
        "template": "reference/sku.json"
    },
    "parameters": {
        "family": {
            "value": ""
        },
        "name": {
            "value": ""
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
