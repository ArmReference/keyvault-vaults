# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
bypass         | No       | Tells what traffic can bypass network rules. This can be 'AzureServices' or 'None'. If not specified the default is 'AzureServices'.
defaultAction  | Yes      | The default action when no rule from ipRules and from virtualNetworkRules match. This is only used after the bypass property has been evaluated.
ipRules        | No       | The list of IP address rules.
virtualNetworkRules | No       | The list of virtual network rules.

### bypass

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Tells what traffic can bypass network rules. This can be 'AzureServices' or 'None'. If not specified the default is 'AzureServices'.

- Default value: `AzureServices`

- Allowed values: `AzureServices`, `None`

### defaultAction

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

The default action when no rule from ipRules and from virtualNetworkRules match. This is only used after the bypass property has been evaluated.

- Allowed values: `Allow`, `Deny`

### ipRules

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The list of IP address rules.

### virtualNetworkRules

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The list of virtual network rules.

## Outputs

Name | Type | Description
---- | ---- | -----------
NetworkRuleSet | object | Azure KeyVault NetworkRuleSet

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
        "template": "reference/networkruleset.json"
    },
    "parameters": {
        "bypass": {
            "value": "AzureServices"
        },
        "defaultAction": {
            "value": ""
        },
        "ipRules": {
            "value": []
        },
        "virtualNetworkRules": {
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
