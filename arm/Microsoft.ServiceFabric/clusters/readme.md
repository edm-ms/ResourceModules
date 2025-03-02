# ServiceFabric Cluster `[Microsoft.ServiceFabric/clusters]`

This module deploys a service fabric cluster.

## Resource Types

| Resource Type | API Version |
| :-- | :-- |
| `Microsoft.Authorization/locks` | 2016-09-01 |
| `Microsoft.Authorization/roleAssignments` | 2020-04-01-preview |
| `Microsoft.ServiceFabric/clusters` | 2021-06-01 |
| `Microsoft.ServiceFabric/clusters/applicationTypes` | 2021-06-01 |

## Parameters

| Parameter Name | Type | Default Value | Possible Values | Description |
| :-- | :-- | :-- | :-- | :-- |
| `addOnFeatures` | array | `[]` | `[BackupRestoreService, DnsService, RepairManager, ResourceMonitorService]` | Optional. The list of add-on features to enable in the cluster. |
| `applicationTypes` | _[applicationTypes](applicationTypes/readme.md)_ array | `[]` |  | Optional. Array of Service Fabric cluster application types. |
| `azureActiveDirectory` | object | `{object}` |  | Optional. The settings to enable AAD authentication on the cluster. |
| `certificate` | object | `{object}` |  | Optional. Describes the certificate details like thumbprint of the primary certificate, thumbprint of the secondary certificate and the local certificate store location |
| `certificateCommonNames` | object | `{object}` |  | Optional. Describes a list of server certificates referenced by common name that are used to secure the cluster. |
| `clientCertificateCommonNames` | array | `[]` |  | Optional. The list of client certificates referenced by common name that are allowed to manage the cluster. |
| `clientCertificateThumbprints` | array | `[]` |  | Optional. The list of client certificates referenced by thumbprint that are allowed to manage the cluster. |
| `clusterCodeVersion` | string |  |  | Optional. The Service Fabric runtime version of the cluster. This property can only by set the user when upgradeMode is set to "Manual". To get list of available Service Fabric versions for new clusters use ClusterVersion API. To get the list of available version for existing clusters use availableClusterVersions. |
| `cuaId` | string |  |  | Optional. Customer Usage Attribution ID (GUID). This GUID must be previously registered |
| `diagnosticsStorageAccountConfig` | object | `{object}` |  | Optional. The storage account information for storing Service Fabric diagnostic logs. |
| `eventStoreServiceEnabled` | bool |  |  | Optional. Indicates if the event store service is enabled. |
| `fabricSettings` | array | `[]` |  | Optional. The list of custom fabric settings to configure the cluster. |
| `infrastructureServiceManager` | bool |  |  | Optional. Indicates if infrastructure service manager is enabled. |
| `location` | string | `[resourceGroup().location]` |  | Optional. Location for all resources. |
| `lock` | string | `NotSpecified` | `[CanNotDelete, NotSpecified, ReadOnly]` | Optional. Specify the type of lock. |
| `managementEndpoint` | string |  |  | Required. The http management endpoint of the cluster. |
| `maxUnusedVersionsToKeep` | int | `3` |  | Required. Number of unused versions per application type to keep. |
| `name` | string |  |  | Required. Name of the Service Fabric cluster. |
| `nodeTypes` | array | `[]` |  | Required. The list of node types in the cluster. |
| `notifications` | array | `[]` |  | Optional. Indicates a list of notification channels for cluster events. |
| `reliabilityLevel` | string |  | `[Bronze, Gold, None, Platinum, Silver]` | Optional. The reliability level sets the replica set size of system services. Learn about ReliabilityLevel (https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-capacity). - None - Run the System services with a target replica set count of 1. This should only be used for test clusters. - Bronze - Run the System services with a target replica set count of 3. This should only be used for test clusters. - Silver - Run the System services with a target replica set count of 5. - Gold - Run the System services with a target replica set count of 7. - Platinum - Run the System services with a target replica set count of 9. |
| `reverseProxyCertificate` | object | `{object}` |  | Optional. Describes the certificate details. |
| `reverseProxyCertificateCommonNames` | object | `{object}` |  | Optional. Describes a list of server certificates referenced by common name that are used to secure the cluster. |
| `roleAssignments` | array | `[]` |  | Optional. Array of role assignment objects that contain the 'roleDefinitionIdOrName' and 'principalId' to define RBAC role assignments on this resource. In the roleDefinitionIdOrName attribute, you can provide either the display name of the role definition, or it's fully qualified ID in the following format: '/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11' |
| `sfZonalUpgradeMode` | string | `Hierarchical` | `[Hierarchical, Parallel]` | Optional. This property controls the logical grouping of VMs in upgrade domains (UDs). This property cannot be modified if a node type with multiple Availability Zones is already present in the cluster. |
| `tags` | object | `{object}` |  | Optional. Tags of the resource. |
| `upgradeDescription` | object | `{object}` |  | Optional. Describes the policy used when upgrading the cluster. |
| `upgradeMode` | string | `Automatic` | `[Automatic, Manual]` | Optional. The upgrade mode of the cluster when new Service Fabric runtime version is available. |
| `upgradePauseEndTimestampUtc` | string |  |  | Optional. Indicates the end date and time to pause automatic runtime version upgrades on the cluster for an specific period of time on the cluster (UTC). |
| `upgradePauseStartTimestampUtc` | string |  |  | Optional. Indicates the start date and time to pause automatic runtime version upgrades on the cluster for an specific period of time on the cluster (UTC). |
| `upgradeWave` | string | `Wave0` | `[Wave0, Wave1, Wave2]` | Optional. Indicates when new cluster runtime version upgrades will be applied after they are released. By default is Wave0. |
| `vmImage` | string |  |  | Optional. The VM image VMSS has been configured with. Generic names such as Windows or Linux can be used |
| `vmssZonalUpgradeMode` | string | `Hierarchical` | `[Hierarchical, Parallel]` | Optional. This property defines the upgrade mode for the virtual machine scale set, it is mandatory if a node type with multiple Availability Zones is added. |
| `waveUpgradePaused` | bool |  |  | Optional. Boolean to pause automatic runtime version upgrades to the cluster. |

### Parameter Usage: `notifications`

```json
"notifications": {
    "value": [
        {
            "isEnabled": true, // Required. Indicates if the notification is enabled.
            "notificationCategory": "WaveProgress", // Required. The category of notification. Possible values include: "WaveProgress".
            "notificationLevel": "Critical", // Required. The level of notification. Possible values include: "Critical", "All".
            "notificationTargets": [
                {
                    "notificationChannel": "EmailUser", // Required. The notification channel indicates the type of receivers subscribed to the notification, either user or subscription. Possible values include: "EmailUser", "EmailSubscription".
                    "receivers": [
                        "SomeReceiver" // Required. List of targets that subscribe to the notification.
                    ]
                }
            ]
        }
    ]
}
```

### Parameter Usage: `roleAssignments`

```json
"roleAssignments": {
    "value": [
        {
            "roleDefinitionIdOrName": "Reader",
            "principalIds": [
                "12345678-1234-1234-1234-123456789012", // object 1
                "78945612-1234-1234-1234-123456789012" // object 2
            ]
        },
        {
            "roleDefinitionIdOrName": "/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11",
            "principalIds": [
                "12345678-1234-1234-1234-123456789012" // object 1
            ]
        }
    ]
}
```

### Parameter Usage: `tags`

Tag names and tag values can be provided as needed. A tag can be left without a value.

```json
"tags": {
    "value": {
        "Environment": "Non-Prod",
        "Contact": "test.user@testcompany.com",
        "PurchaseOrder": "1234",
        "CostCenter": "7890",
        "ServiceName": "DeploymentValidation",
        "Role": "DeploymentValidation"
    }
}
```

## Outputs

| Output Name | Type | Description |
| :-- | :-- | :-- |
| `endpoint` | string | The Service Fabric Cluster endpoint. |
| `name` | string | The Service Fabric Cluster name. |
| `resourceGroupName` | string | The Service Fabric Cluster resource group. |
| `resourceId` | string | The Service Fabric Cluster resource ID. |

## Template references

- [Clusters](https://docs.microsoft.com/en-us/azure/templates/Microsoft.ServiceFabric/2021-06-01/clusters)
- [Clusters/Applicationtypes](https://docs.microsoft.com/en-us/azure/templates/Microsoft.ServiceFabric/2021-06-01/clusters/applicationTypes)
- [Locks](https://docs.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2016-09-01/locks)
- [Roleassignments](https://docs.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2020-04-01-preview/roleAssignments)
