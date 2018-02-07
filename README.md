# keyvault-vaults
reference deployment
```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "StorageAccountName": {
      "type": "string"
    },
    "ContainerName": {
      "type": "string"
    },
    "SasToken": {
      "type": "string"
    }
  },
  "variables": {
    "Provider": "/Microsoft.KeyVault",
    "Resource": "/vaults",
    "templateUri": "[concat('https://',parameters('StorageAccountName'),'.blob.core.windows.net/',parameters('ContainerName'),variables('Provider'),variables('Resource'))]"
  },
  "resources": [
    {
      "name": "BuildSKU",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2016-09-01",
      "dependsOn": [],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('templateUri'), '/sku.json', parameters('SasToken'))]",
          "contentVersion": "2017.09.01.0"
        },
        "parameters": {
          "family": {
            "value": "A"
          },
          "name": {
            "value": "Standard"
          }
        }
      }
    },
    {
      "name": "BuildUserIDPermissions",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2016-09-01",
      "dependsOn": [],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('templateUri'), '/permissions.json', parameters('SasToken'))]",
          "contentVersion": "2017.09.01.0"
        },
        "parameters": {
          "keys": {
            "value": "[createArray('get','list')]"
          },
          "secrets": {
            "value": "[createArray('get','list')]"
          },
          "certificates": {
            "value": "[createArray('get','list')]"
          },
          "storage": {
            "value": []
          }
        }
      }
    },
    {
      "name": "BuildUserIDAccessPolicy",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2016-09-01",
      "dependsOn": [
        "[concat('Microsoft.Resources/deployments/','BuildUserIDPermissions')]"
      ],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('templateUri'), '/accessPolicies.json', parameters('SasToken'))]",
          "contentVersion": "2017.09.01.0"
        },
        "parameters": {
          "tenantId": {
            "value": "9927a371-09a0-43e2-aacc-c87938810455"
          },
          "objectId": {
            "value": "user@tenantname.com"
          },
          "permissions": {
            "value": "[reference('BuildUserIDPermissions').outputs.permissions.value]"
          }
        }
      }
    },
    {
      "name": "BuildVaultProperties",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2016-09-01",
      "dependsOn": [
        "[concat('Microsoft.Resources/deployments/','BuildSKU')]",
        "[concat('Microsoft.Resources/deployments/','BuildUserIDAccessPolicy')]"
      ],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('templateUri'), '/properties.json', parameters('SasToken'))]",
          "contentVersion": "2017.09.01.0"
        },
        "parameters": {
          "tenantId": {
            "value": "9927a371-09a0-43e2-aacc-c87938810455"
          },
          "sku": {
            "value": "[reference('BuildSKU').outputs.sku.value]"
          },
          "accessPolicies": {
            "value": "[createarray(reference('BuildUserIDAccessPolicy').outputs.accessPolicies.value)]"
          },
          "enabledForDeployment": {
            "value": true
          },
          "enabledForDiskEncryption": {
            "value": false
          },
          "enabledForTemplateDeployment": {
            "value": true
          },
          "enableSoftDelete": {
            "value": false
          }
        }
      }
    },
    {
      "name": "DeployVault",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2016-09-01",
      "dependsOn": [
        "[concat('Microsoft.Resources/deployments/','BuildVaultProperties')]"
      ],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('templateUri'), '/vaults.json', parameters('SasToken'))]",
          "contentVersion": "2017.09.01.0"
        },
        "parameters": {
          "name": {
            "value": "KeyVault"
          },
          "VaultProperties": {
            "value": "[reference('BuildVaultProperties').outputs.properties.value]"
          }
        }
      }
    }
  ],
  "outputs": {
    "vaults": {
      "type": "object",
      "value": "[reference('DeployVault').outputs.vaults.value]"
    }
  }
}
```
