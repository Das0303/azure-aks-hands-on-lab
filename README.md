# ☁️ Azure Kubernetes Service (AKS) Hands-on Lab

This repository documents a complete hands-on lab demonstrating how to deploy, scale, and manage an **Azure Kubernetes Service (AKS)** cluster using the **Azure CLI** and **kubectl**, followed by deploying the **Azure Store** multi-container sample application.

---

## 📘 Project Overview

This project is based on the official Microsoft Learn [AKS Quickstart Guide](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli) and serves as a practical exercise to:
- Create and configure an AKS cluster using Azure CLI commands.
- Understand Kubernetes fundamentals (nodes, pods, deployments, services).
- Scale and manage AKS node pools.
- Deploy and test a containerized sample application.
- Practice cleanup and cost management procedures.

The repository is designed to demonstrate real-world DevOps workflows for infrastructure as code, container orchestration, and managed cluster operations in Azure.

---

## 🧱 Architecture

The lab deploys a **managed Kubernetes cluster** with:
- 1 System Node Pool (Linux node)
- Azure-managed control plane
- System-assigned managed identity
- A sample microservices application consisting of:  
  - Store Front (web UI)  
  - Product Service  
  - Order Service  
  - RabbitMQ (message broker)

## [AKS Architecture Diagram]
<img width="764" height="275" alt="image" src="https://github.com/user-attachments/assets/2803222e-7c0c-433b-8760-8e2015cdd43b" />


---

## ⚙️ Prerequisites

Ensure you have the following before starting:

- **Azure Subscription** (Free or Paid)
- **Azure CLI v2.61+**
- **kubectl** installed or accessible via [Azure Cloud Shell](https://shell.azure.com)
- Basic familiarity with CLI and Kubernetes commands

---

## 🚀 Step-by-Step Commands

### 1. Set Variables
export RANDOM_ID=$(openssl rand -hex 3)
MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
REGION="westus"



(Optional) To use an existing resource group:
export MY_RESOURCE_GROUP_NAME="ExistingRGName"



### 2. Create Resource Group
az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION



### 3. Create an AKS Cluster
az aks create
--resource-group $MY_RESOURCE_GROUP_NAME
--name $MY_AKS_CLUSTER_NAME
--node-count 1
--generate-ssh-keys



### 4. Connect to the Cluster
az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER_NAME
kubectl get nodes



### 5. Deploy the Sample Application
kubectl apply -f manifests/aks-store-quickstart.yaml

Verify deployment:
kubectl get pods -A
kubectl get svc store-front


Access your application via the **EXTERNAL-IP** output in a browser.

### 6. Scale Node Pool (Optional)
az aks nodepool add
--resource-group $MY_RESOURCE_GROUP_NAME
--cluster-name $MY_AKS_CLUSTER_NAME
--name agentpool2
--node-count 2


### 7. Cleanup Resources
az group delete --name $MY_RESOURCE_GROUP_NAME --yes --no-wait


---

## 📂 Repository Structure

<img width="208" height="300" alt="image" src="https://github.com/user-attachments/assets/2a2a981d-7412-465b-83cd-092f7f35b916" />



---

## 🧠 Key Learnings

- Hands-on experience in **AKS provisioning** and **kubectl management**.
- Understanding how AKS uses separate resource groups for cluster and node resources.
- Exposure to **multi-container deployments**, **LoadBalancer services**, and **cluster scaling**.
- Practical DevOps workflow for **infrastructure automation** and **observability** in Azure.

---

## 🧩 Next Steps

- Integrate with **Azure Container Registry (ACR)** for CI/CD pipelines.
- Experiment with **KEDA autoscaling** or **Azure Monitor for Containers**.
- Extend this setup with **GitHub Actions** for automated deployments.

---

## 🏁 Outcome

Upon completion, you will have:

✔️ A fully functional AKS cluster  
✔️ A deployed sample microservices app  
✔️ Working knowledge of AKS scaling and management  
✔️ A portfolio-ready DevOps project to showcase in interviews  

---

## 📜 References

- [Microsoft Learn: Quickstart using Azure CLI](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli)
- [Azure-Samples/aks-store-demo](https://github.com/Azure-Samples/aks-store-demo)
- [Azure Kubernetes Service Documentation](https://learn.microsoft.com/en-us/azure/aks/)

---

**Author:** AYUSMITA DAS <br>
**Role:** Azure Infrastructure & DevOps Engineer <br>
**Project Type:** Hands-on Lab | Cloud & Kubernetes | DevOps Portfolio
