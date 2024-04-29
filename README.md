
### Overview
---
In this exercise, you learn how to perform the following actions:
- Create a resource group for the container
- Create a container
- Verify the container is running

   
### Key Aspects
---
Azure Container Instance

### Environment
---
Microsoft Azure Portal
- Valid Subscription

### Actions
---
Prepare the environment
  - Open Azure Cloud Shell (https://portal.azure.com/#cloudshell/)

  - Create a resource group for the resources needed for this exercise
```
z account list-locations --output table
DEFAULT_LOCATION="eastus2"
CURRENT_MOMENT="20240429151700"
DEFAULT_RESOURCEGROUP="myresourcegroup${CURRENT_MOMENT}"
az group create --name ${DEFAULT_RESOURCEGROUP} --location ${DEFAULT_LOCATION}
```

- Create an Azure Container Instance
```
DEFAULT_CONTAINER="mycontainer${CURRENT_MOMENT}"
DEFAULT_DNS="aci${CURRENT_MOMENT}"
az container create --resource-group ${DEFAULT_RESOURCEGROUP} --name ${DEFAULT_CONTAINER} --image mcr.microsoft.com/azuredocs/aci-helloworld --ports 80 --dns-name-label ${DEFAULT_DNS}
```

Run the image in the ACI
- Check if the container is running
```
az container show --resource-group ${DEFAULT_RESOURCEGROUP} --name ${DEFAULT_CONTAINER} --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" --out table
```

Clean up resources
- Delete the Resource Groups and its content
```
az group delete --name ${DEFAULT_RESOURCEGROUP} --no-wait
```

### Media
---
![image](https://github.com/ViCunha/Lab-Azure-AzureContainerInstance-OnAzurePortal/assets/65992033/3f68fbb3-2435-4278-84ea-c87b82f5367a)

---
![image](https://github.com/ViCunha/Lab-Azure-AzureContainerInstance-OnAzurePortal/assets/65992033/ee3db6ae-1054-4adf-9260-796d9e2f0722)


### References
---
- [Exercise - Deploy a container instance by using the Azure CLI](https://learn.microsoft.com/en-us/training/modules/create-run-container-images-azure-container-instances/3-run-azure-container-instances-cloud-shell)
