# Provision Cloud Infrastructure

> Currently, we have automated infra provision scripts available for azure cloud service provider. If you are using any other cloud service provider, provision infrastructure manually as per the pre-requisites or write automation scripts for the same and contribute.&#x20;



**Provisioning infrastructure on Azure**

You can run the following steps to create azure infrastructure using ansible.

Easiest way to use the script will be to use azure cloud shell, as the cloud shell comes with all prerequisites bundled.

* login to portal.azure.com
* click on the cloudshell -> select bash ( if you’re using it for the first time )

If you want to run this on your local machine, Follow this [guide](https://docs.microsoft.com/en-us/azure/developer/ansible/install-on-linux-vm?tabs=azure-cli#install-ansible-on-the-virtual-machine).

```
git clone https://github.com/project-sunbird/sunbird-devops -b release-6.0.0
cd sunbird-devops/deploy
# Update the necessary variables in playbook like ssh public key path, resource group name, AKS version, Storage account name, container registry etc. 
ansible-playbook -c local azure-provision.yaml
# Resulting infrastructure infromation will be stored in sunbird-devops/deploy/azure-resources.txt file.
```

**Creating the AKS cluster from Azure console**

> Incase if you are having trouble in creating AKS cluster using the above script, follow the steps given below to create the Kubernetes cluster in Azure. The AKS cluster and VM’s should be in same vnet. If they are in different vnet, you have to peer the vnets. To successfully peer, the IP address of the vnets should not overlap.

* Create a service principal and assign contributor role to service principal. Ref: [https://learn.microsoft.com/en-us/cli/azure/azure-cli-sp-tutorial-1?tabs=bash](https://learn.microsoft.com/en-us/cli/azure/azure-cli-sp-tutorial-1?tabs=bash)
* Get the secrets and client id of service principal
* Create the AKS cluster either via Azure portal or using `az aks` command line
* Refer to Azure documentation for all the available options
* Below is a sample command which you can use -

```bash
  az aks create --resource-group <resouse-group-name> --node-resource-group <k8s-resource-group-name> --name <cluster name>  --node-count 5 --admin-username deployer --kubernetes-version 1.24 --service-principal "<service principal id>" --node-vm-size Standard_D4s_v3 --client-secret "<client id>" --network-plugin azure --ssh-key-value @deployer.pub -l <region> --vm-set-type VirtualMachineScaleSets --vnet-subnet-id /subscriptions/<subscription id>/resourceGroups/<resouse-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet name>
```

> Note: Ensure you have allocated at least 1024 IP’s for your Kubernetes subnet (CIDR notation as x.x.x.x/22)

Get the kubeconfig file for your cluster with the below command -

```bash
  az aks get-credentials --resource-group <resource group name> --name <cluster name> --file  k8s.yaml
```

#### Configuring the Azure storage account <a href="#configuring-the-azure-storage-account" id="configuring-the-azure-storage-account"></a>

* Update the CORS rule for the storage account as follows:

```bash
    Allowed Origins: *
    Allowed Methods: GET,HEAD,OPTIONS, PUT
    Allowed Headers: Access-Control-Allow-Origin,Access-Control-Allow-Method,Origin,x-ms-meta-qq,x-ms-blob-type,x-ms-blob-content-type,Content-Type
    Exposed Headers: Access-Control-Allow-Origin,Access-Control-Allow-Methods
    Max Age: 200

```

* Disable **Secure transfer required** in storage account configuration

**Provisioning infrastructure on other cloud service providers except Azure**

* Object storage with CORS enabled
* Virtual network to host VM's and Kubernetes cluster
* Kubernetes cluster with 4 worker nodes each node with 4 Core, 16GB RAM configuration
* Create Compute Instances/VM's as mentioned in pre-requisites section
* Make sure kubernetes cluster and VM's can communicate with each other