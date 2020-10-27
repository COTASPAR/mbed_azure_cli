# mbed_azure_cli
Potentially useful commands for Azure CLI

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
  
  1. Log in to your Azure account  
  
      ```
      az login
      ```
  
  1. Create a resource under free tier
  
    ```
    az iot hub create --name mbedHubTest --resource-group MbedDemoGroupTest --location eastus --sku Free
    ```
 
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
1. Get device connection string

    ```
    az iot hub device-identity connection-string show --hub-name mbedHubTest --device-id MbedDeviceTest --output table
    ```

