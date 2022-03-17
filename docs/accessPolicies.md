# Azure template

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
tenantId       | Yes      | The Azure Active Directory tenant ID that should be used for authenticating requests to the key vault. - globally unique identifier
objectId       | Yes      | The object ID of a user, service principal or security group in the Azure Active Directory tenant for the vault. The object ID must be unique for the list of access policies.
applicationId  | No       | Application ID of the client making request on behalf of a principal - globally unique identifier
permissions    | Yes      | Permissions the identity has for keys, secrets and certificates

### tenantId

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

The Azure Active Directory tenant ID that should be used for authenticating requests to the key vault. - globally unique identifier

### objectId

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

The object ID of a user, service principal or security group in the Azure Active Directory tenant for the vault. The object ID must be unique for the list of access policies.

### applicationId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Application ID of the client making request on behalf of a principal - globally unique identifier

### permissions

![Parameter Setting](https://img.shields.io/badge/parameter-required-orange?style=flat-square)

Permissions the identity has for keys, secrets and certificates

## Outputs

Name | Type | Description
---- | ---- | -----------
accessPolicies | object | Azure KeyVault Access Policy

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.1",
    "metadata": {
        "template": "reference/accessPolicies.json"
    },
    "parameters": {
        "tenantId": {
            "value": ""
        },
        "objectId": {
            "value": ""
        },
        "applicationId": {
            "value": ""
        },
        "permissions": {
            "value": {}
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
