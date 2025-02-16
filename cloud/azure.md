# Azure CLI Cheatsheet

A comprehensive guide for managing Azure resources using the Azure CLI.

## Table of Contents

- [Authentication & Setup](#authentication--setup)
- [Resource Management](#resource-management)
- [Virtual Machines (VMs)](#virtual-machines-vms)
- [Storage (Blob, File, Disk)](#storage-blob-file-disk)
- [Networking](#networking)
- [Kubernetes (AKS)](#kubernetes-aks)
- [Database Services](#database-services)
- [Monitoring & Logging](#monitoring--logging)
- [Security & Identity](#security--identity)

## Authentication & Setup

Login to Azure:

```bash
az login
```

Set default subscription:

```bash
az account set --subscription "<subscription-id>"
```

List all subscriptions:

```bash
az account list --output table
```

## Resource Management

List all resource groups:

```bash
az group list --output table
```

Create a resource group:

```bash
az group create --name MyResourceGroup --location eastus
```

Delete a resource group:

```bash
az group delete --name MyResourceGroup --yes --no-wait
```

## Virtual Machines (VMs)

List all VMs:

```bash
az vm list --output table
```

Create a VM:

```bash
az vm create --resource-group MyResourceGroup --name MyVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys
```

Start/Stop a VM:

```bash
az vm start --resource-group MyResourceGroup --name MyVM
az vm stop --resource-group MyResourceGroup --name MyVM
```

Delete a VM:

```bash
az vm delete --resource-group MyResourceGroup --name MyVM --yes
```

## Storage (Blob, File, Disk)

List storage accounts:

```bash
az storage account list --output table
```

Create a storage account:

```bash
az storage account create --name mystorageaccount --resource-group MyResourceGroup --location eastus --sku Standard_LRS
```

Upload a blob to a storage container:

```bash
az storage blob upload --account-name mystorageaccount --container-name mycontainer --name myblob.txt --file myfile.txt
```

## Networking

List all virtual networks:

```bash
az network vnet list --output table
```

Create a virtual network:

```bash
az network vnet create --resource-group MyResourceGroup --name MyVNet --address-prefix 10.0.0.0/16
```

List all public IPs:

```bash
az network public-ip list --output table
```

## Kubernetes (AKS)

List all AKS clusters:

```bash
az aks list --output table
```

Create an AKS cluster:

```bash
az aks create --resource-group MyResourceGroup --name MyAKSCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys
```

Get credentials for an AKS cluster:

```bash
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```

## Database Services

List all SQL databases:

```bash
az sql db list --resource-group MyResourceGroup --server myserver --output table
```

Create a SQL database:

```bash
az sql db create --resource-group MyResourceGroup --server myserver --name mydatabase --service-objective S0
```

Delete a SQL database:

```bash
az sql db delete --resource-group MyResourceGroup --server myserver --name mydatabase --yes
```

## Monitoring & Logging

View Azure Monitor logs:

```bash
az monitor log-profiles list --output table
```

View activity logs:

```bash
az monitor activity-log list --output table
```

## Security & Identity

List all Azure AD users:

```bash
az ad user list --output table
```

Create an Azure AD user:

```bash
az ad user create --display-name "User Name" --user-principal-name user@example.com --password "Password123!"
```

Assign a role to a user:

```bash
az role assignment create --assignee user@example.com --role "Contributor" --scope /subscriptions/<subscription-id>
```