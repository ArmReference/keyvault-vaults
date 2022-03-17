# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
id             | Yes      | Full resource id of a vnet subnet
ignoreMissingVnetServiceEndpoint | Yes      | Property to specify whether NRP will ignore the check if parent subnet has serviceEndpoints configured.

### id

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Full resource id of a vnet subnet

### ignoreMissingVnetServiceEndpoint

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Property to specify whether NRP will ignore the check if parent subnet has serviceEndpoints configured.

## Outputs

Name | Type | Description
---- | ---- | -----------
VirtualNetworkRule | object | Azure KeyVault VirtualNetworkRule

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
        "template": "reference/virtualnetworkrule.json"
    },
    "parameters": {
        "id": {
            "value": ""
        },
        "ignoreMissingVnetServiceEndpoint": {
            "value": null
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
