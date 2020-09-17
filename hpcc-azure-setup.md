# Creating an Azure AKS cluster for HPCC-k8s

### Login (not needed if using Azure Cloud Shell)
`az login`

### Create a resource group
`az group create --name jcshpccdemo-rg --location eastus2`

#### If don't have a SSH key pair, need to create one [or you can pass --generate-ssh-keys]
`ssh-keygen -m PEM -t rsa -b 4096`


### Create the AKS cluster
`az aks create --resource-group jcshpccdemo-rg --name jcshpccdemo-aks --node-vm-size Standard_B2s --node-count 1 --min-count 1 --max-count 4 --enable-cluster-autoscaler --enable-managed-identity --location eastus2`

### Configure credential access to k8s cluster
`az aks get-credentials --resource-group jcshpccdemo-rg --name jcshpccdemo-aks --admin --overwrite-existing`

***You now have a K8s AKS cluster ready to use.***

#### Some other useful commands
`az account list -o table` - list subscriptions (without -o table, it's more verbose yaml output)

`az account list-locations -o table` - list supported locations for your subscription

`az aks delete --resource-group jcshpccdemo-rg --name jcshpccdemo-aks --yes` - Delete the AKS cluster

`az group delete --name jcshpccdemo-rg` - delete entire resource group
