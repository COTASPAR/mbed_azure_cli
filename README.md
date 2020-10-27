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
   
  1. Create a resource under free tier, we set partion count equal to 2 since we are on the Free tier Azure won't allow any other default (values)[https://stackoverflow.com/questions/59178667/when-im-going-through-azure-iot-hub-tutorial-creating-end-with-error-partition]
  
     ```
     az iot hub create --name mbedHubTest --resource-group MbedDemoGroupTest --location eastus --sku F1 --partition-count 2
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

