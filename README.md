# mbed_azure_cli
Potentially useful commands for Azure CLI


  
  1. Log in to your Azure account  
  
      ```
      az login
      ```
<!--
My info:
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "f34e5979-57d9-4aaa-ad4d-b122a662184d",
    "id": "f90ce610-592a-41bd-9e48-9b07ec7fdd88",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Free Trial",
    "state": "Enabled",
    "tenantId": "f34e5979-57d9-4aaa-ad4d-b122a662184d",
    "user": {
      "homeAccountId": "dffe89eb-3d86-4d74-81c4-23904346f991.f34e5979-57d9-4aaa-ad4d-b122a662184d",
      "name": "Carlo.Grisafi@arm.com",
      "type": "user"
    }
-->      
   
  1. Get the IoT extension 
  
      ```
      az extension add --name azure-iot
      ```
  1. Create a resource group 
  
      ```
      az group create -l eastus -n MbedDemoGroupTest
      ```
<!-- 
{
  "id": "/subscriptions/f90ce610-592a-41bd-9e48-9b07ec7fdd88/resourceGroups/MbedDemoGroupTest",
  "location": "eastus",
  "managedBy": null,
  "name": "MbedDemoGroupTest",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
-->
   
  1. Create a resource under free tier, we set partion count equal to 2 since we are on the Free tier Azure won't allow any other default [values](https://stackoverflow.com/questions/59178667/when-im-going-through-azure-iot-hub-tutorial-creating-end-with-error-partition). Note: if you have created a Hub in the past with your Azure account and you are on the Free tier then you'll have to get rid of it for this to work as only a single Hub can be had under Free tier.
  
     ```
     az iot hub create --name mbedHubTest --resource-group MbedDemoGroupTest --location eastus --sku F1 --partition-count 2
     ```
 
<!--
{
  "etag": "AAAABBKxS+E=",
  "id": "/subscriptions/f90ce610-592a-41bd-9e48-9b07ec7fdd88/resourceGroups/MbedDemoGroupTest/providers/Microsoft.Devices/IotHubs/mbedHubTest",
  "identity": {
    "type": "None"
  },
  "location": "eastus",
  "name": "mbedHubTest",
  "properties": {
    "authorizationPolicies": null,
    "cloudToDevice": {
      "defaultTtlAsIso8601": "1:00:00",
      "feedback": {
        "lockDurationAsIso8601": "0:00:05",
        "maxDeliveryCount": 10,
        "ttlAsIso8601": "1:00:00"
      },
      "maxDeliveryCount": 10
    },
    "comments": null,
    "enableFileUploadNotifications": false,
    "eventHubEndpoints": {
      "events": {
        "endpoint": "sb://ihsuprodblres091dednamespace.servicebus.windows.net/",
        "partitionCount": 2,
        "partitionIds": [
          "0",
          "1"
        ],
        "path": "iothub-ehub-mbedhubtes-5547811-474d3b7af9",
        "retentionTimeInDays": 1
      }
    },
    "features": "None",
    "hostName": "mbedHubTest.azure-devices.net",
    "ipFilterRules": [],
    "locations": [
      {
        "location": "East US",
        "role": "primary"
      },
      {
        "location": "West US",
        "role": "secondary"
      }
    ],
    "messagingEndpoints": {
      "fileNotifications": {
        "lockDurationAsIso8601": "0:01:00",
        "maxDeliveryCount": 10,
        "ttlAsIso8601": "1:00:00"
      }
    },
    "minTlsVersion": null,
    "privateEndpointConnections": null,
    "provisioningState": "Succeeded",
    "publicNetworkAccess": null,
    "routing": {
      "endpoints": {
        "eventHubs": [],
        "serviceBusQueues": [],
        "serviceBusTopics": [],
        "storageContainers": []
      },
      "enrichments": null,
      "fallbackRoute": {
        "condition": "true",
        "endpointNames": [
          "events"
        ],
        "isEnabled": true,
        "name": "$fallback"
      },
      "routes": []
    },
    "state": "Active",
    "storageEndpoints": {
      "$default": {
        "authenticationType": null,
        "connectionString": "",
        "containerName": "",
        "sasTtlAsIso8601": "1:00:00"
      }
    }
  },
  "resourcegroup": "MbedDemoGroupTest",
  "sku": {
    "capacity": 1,
    "name": "F1",
    "tier": "Free"
  },
  "subscriptionid": "f90ce610-592a-41bd-9e48-9b07ec7fdd88",
  "tags": {},
  "type": "Microsoft.Devices/IotHubs"
}
-->
 
 
 
 
 
 
 
<!--
1. Add endpoint 
 
     ```
     az iot hub routing-endpoint create --resource-group MbedDemoGroupTest --hub-name mbedHubTest --endpoint-name EndPTest --endpoint-type eventhub --endpoint-resource-group {ResourceGroup} --endpoint-subscription-id {SubscriptionId} --connection-string {ConnectionString}
     ``` 
     -->
1. Register a device

    ```
    az iot hub device-identity create --hub-name mbedHubTest --device-id MbedDeviceTest
    ```
<!--
{
  "authentication": {
    "symmetricKey": {
      "primaryKey": "BQaa/4t2QApcB+1uYgSu9QMGiaj1m/sBDwhtVQpJXEk=",
      "secondaryKey": "IiOFEEpl9/cQOescUqlowTjOCpmpSvZF1ntkon44ARM="
    },
    "type": "sas",
    "x509Thumbprint": {
      "primaryThumbprint": null,
      "secondaryThumbprint": null
    }
  },
  "capabilities": {
    "iotEdge": false
  },
  "cloudToDeviceMessageCount": 0,
  "connectionState": "Disconnected",
  "connectionStateUpdatedTime": "0001-01-01T00:00:00",
  "deviceId": "MbedDeviceTest",
  "deviceScope": null,
  "etag": "MTU4MjY3MDc5",
  "generationId": "637394137160664574",
  "lastActivityTime": "0001-01-01T00:00:00",
  "status": "enabled",
  "statusReason": null,
  "statusUpdatedTime": "0001-01-01T00:00:00"
}
-->

1. Get device connection string, open mbed_app.json and paste this string into the value field of iothub_connection_string.

    ```
    az iot hub device-identity connection-string show --hub-name mbedHubTest --device-id MbedDeviceTest --output table
    ```

<!--
HostName=mbedHubTest.azure-devices.net;DeviceId=MbedDeviceTest;SharedAccessKey=BQaa/4t2QApcB+1uYgSu9QMGiaj1m/sBDwhtVQpJXEk=
-->
