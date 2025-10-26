## Deploy the application
To deploy the application, you use a manifest file to create all the objects required to run the AKS Store application. A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

## Screenshot of Azure Store sample architecture.
<img width="1424" height="525" alt="image" src="https://github.com/user-attachments/assets/550e380b-47c3-4074-b71a-2afde3b84393" />

Store front: Web application for customers to view products and place orders. <br>
Product service: Shows product information.<br>
Order service: Places orders.<br>
RabbitMQ: Message queue for an order queue.<br>

## REFERENCE

https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli
