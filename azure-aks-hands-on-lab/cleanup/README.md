## 1. Delete the AKS Cluster
This removes the cluster and all associated node pools (VMs):

    az aks delete --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER_NAME --yes --no-wait

## 2. Delete the Resource Group
This nukes everything inside the group — AKS, LoadBalancers, Public IPs, NSGs, etc. Use only if you're done with all resources:

    az group delete --name $MY_RESOURCE_GROUP_NAME --yes --no-wait

## 3. Delete Container Registry (if created)

    az acr delete --name <your-acr-name> --resource-group $MY_RESOURCE_GROUP_NAME

## 4. Delete Public IPs (if not in RG)
Sometimes public IPs get created outside the AKS resource group:

    az network public-ip list --query "[?contains(name, 'aks')].{Name:name, RG:resourceGroup}" -o table

Then delete Manually :

    az network public-ip delete --name <ip-name> --resource-group <rg-name>

## 5. Delete Disk Resources (if orphaned)
Check for leftover managed disks:

    az disk list --query "[?contains(name, 'aks')].{Name:name, RG:resourceGroup}" -o table

Then Delete :

    az disk delete --name <disk-name> --resource-group <rg-name> --yes

## 6. Delete Load Balancers (if not auto-deleted)

    az network lb list --query "[?contains(name, 'aks')].{Name:name, RG:resourceGroup}" -o table    
    az network lb delete --name <lb-name> --resource-group <rg-name>

## Final Tip: Confirm with Azure Portal
Go to portal.azure.com, filter by your resource group, and double-check for:

Public IPs

Disks

Load balancers

NSGs

Storage accounts
