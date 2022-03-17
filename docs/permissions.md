# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
keys           | No       | Permissions to keys - encrypt, decrypt, wrapKey, unwrapKey, sign, verify, get, list, create, update, import, delete, backup, restore, recover, purge
secrets        | No       | Permissions to secrets - get, list, set, delete, backup, restore, recover, purge
certificates   | No       | Permissions to certificates - get, list, delete, create, import, update, managecontacts, getissuers, listissuers, setissuers, deleteissuers, manageissuers, recover, purge
storage        | No       | Permissions to storage accounts - get, list, delete, set, update, regeneratekey, setsas, listsas, getsas, deletesas

### keys

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Permissions to keys - encrypt, decrypt, wrapKey, unwrapKey, sign, verify, get, list, create, update, import, delete, backup, restore, recover, purge

### secrets

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Permissions to secrets - get, list, set, delete, backup, restore, recover, purge

### certificates

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Permissions to certificates - get, list, delete, create, import, update, managecontacts, getissuers, listissuers, setissuers, deleteissuers, manageissuers, recover, purge

### storage

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Permissions to storage accounts - get, list, delete, set, update, regeneratekey, setsas, listsas, getsas, deletesas

## Outputs

Name | Type | Description
---- | ---- | -----------
permissions | object | Azure KeyVault Permissions Object

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
        "template": "reference/permissions.json"
    },
    "parameters": {
        "keys": {
            "value": []
        },
        "secrets": {
            "value": []
        },
        "certificates": {
            "value": []
        },
        "storage": {
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
