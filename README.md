# Azure Container Apps Hands-on-Labs

## Overview 
Martha, the CTO of the boutique cloud-native technologies consulting firm - StartUps & More Inc. (SUM Inc.), requires  her consultants to be conversant with emergent technologies and methodologies at a consistent yet fast pace. One of the key decisions she makes with the  advent of every new technology is to determine - it's fit-to-purpose and efficacy - before having her consultants delve deeper themselves and consequently having them help their firm's clients.

Azure Container Apps (ACA) - the newest offering from Microsoft providing a serverless platform for running containerized microservices  - is on the top of Martha's emerging tech list for a few  important reasons that she has heard so far -
1. ACA can empower developers to build cloud-native solutions focusing on their apps rather than cloud infrastructure. 

   *Something that resonated even more - considering startup teams would rather focus on product differentiation, speedy go-to-market as compared to foundational infrastructure setup, security and Day-2 operations.*

2. ACA is built on the foundation of open-source  Cloud Native Computing Foundation (CNCF) projects like - Kubernetes Event Driven Autoscaling (KEDA) and Distributed Application Runime (Dapr) which are gaining adoption amongst cloud nativedevelopers and ACA inherently utilizing the CNCF Graduated prooject - Envoy - for its service-proxy functionality.

   *Serverless PaaS powered by CNCF projects to enable developers - sounded like an attractive proposition*

BUT all of this was *still* a surmise ; Martha has looped in and tasked two of her top engineers Alice and Bob to conduct a timeboxed evaluation resulting in key findings based on hands-on evaluation. 
This time-boxed evaluation methodology has proven to be a strategic advantage to Martha's firm for many years.

Alice is a Kubernetes expert having worked with several of SUM Inc.'s clients on anything ranging from - large DIY Kubernetes clusters - to - vendor managed Kubernetes offerings including the Azure Kubernetes Service (AKS) from Microsoft. She has recently aced the Certified Kubernetes Administrator & Certified Kuberneted Application Developer - exams from the Linux Foundation.

Bob is a polyglot developer - addressing  the full-stack of cloud native application development. He is familiar with containerization and orchestration but would rather spend his time building high-performant microservices and applying the needed development rigor driven by well-adopted software development patterns.

Alice and Bob - proceed on the quest set forth by Martha.

## The First Take and next steps

*Alice and Bob - read up on some key documentation, announcements from the Microsoft Product Group and some reference material to utilize as part of the ongoing assessment.*


*To be done*

## Executive summary

*Crisp tabulation of Alice and Bob's findings reported back to Martha before getting the approval to proceed on the hands-on-evaluation and labs*

*To be done*

## The Labs


### Lab 1 – Create an Azure Container App using the Azure Portal and implement traffic-split functionality

**Objectives**

1. Create the environment and test a sample container app using the Azure Portal.   
2. Utilize multiple revisions and test Traffic Split functionality with 2 different versions of the same app.  
As part of the Azure Container App environment creation and deployment,  get familiar with the Azure Portal UI and learn the Azure Container App specific terminologies & features.
3. Optionally, work through and complete the listed challenges.
  ***

**Steps**
1. **Create the sample app** - Follow instructions in the [Lab 1 - Create Azure Container App - Azure Portal.pdf] in the [Lab 1] folder.
   
   Test and verify that you are able to navigate to the ingress URI created and see the expected browser result.
  
   *Please note that the container image for this sample app is pulled from a public Docker repository.   
   If you choose to utilize your own container image repository, utilize the [Lab1\src] folder and the associated Dockerfile to build and push the image to your          repository and substitute the values in the Container App creation step for the [Registry login server] and [Image and tag] values.*

2. **Enable multiple revisions** -  One of the fundamental steps for Traffic Split is to enable multiple revisions of the app to exist *simultaneously*.

   Select the - _Revision Management_ - link in the left navigation menu as shown below  

   and then select -  _Multiple: Several revisions active  simultaneously_  and _Apply_

   <img width="510" alt="image" src="https://user-images.githubusercontent.com/25875242/198610282-24091690-01a4-4920-898b-d8dfcd3d7b32.png">

3. **Create a new revision** 

   <img width="898" alt="image" src="https://user-images.githubusercontent.com/25875242/198646595-03e04c5c-2c35-410d-8bc4-bfbe8f3ed72b.png">

5. Create traffic split.

4. Test traffic split.

 ***

**Challenges (optional)**
1. Implement a 30/30/40 split for same app.
2. Inactivate one of the versions and re-implement 50/50 split.

 ***

### Lab 2 – Create an Azure Container App - with az cli commands
**Objectives**  
1. Get faimiliar with the _az cli_ and the _az containerapp_ commands to create the Container App in Lab 1 in a command line driven manner.
2. Optionally, work through and complete the listed challenge(s).

**Steps**  

```

## Deploy with CLI

# Login to the CLI
az login

# Install the ACA extension for the CLI
az extension add --name containerapp --upgrade

# Register the Microsoft.App namespace
az provider register --namespace Microsoft.App

# Register the Microsoft.OperationalInsights provider for the Azure Monitor Log Analytics workspace if you have not used it before.
az provider register --namespace Microsoft.OperationalInsights

# Set the following environment variables

RESOURCE_GROUP="your-container-app-name"
LOCATION="eastus"
CONTAINERAPPS_ENVIRONMENT="your-environment"

# Create a resource group to organize the services related to your new container app

az group create \
  --name $RESOURCE_GROUP \
  --location $LOCATION
  
# Create the ACA Environment

az containerapp env create \
  --name $CONTAINERAPPS_ENVIRONMENT \
  --resource-group $RESOURCE_GROUP \
  --location $LOCATION
  
 # Create the Container App
 
 az containerapp create \
  --image "docker.io/dockerr10n/aca-lab1-image:green" \
  --name my-container-app \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT
  --target-port 80 \
  --query configuration.ingress.fqdn


```


**Challenges (optional)**
1. Convert the above deployment internal ingress using - _az cli_ .
2. Secure the above deployment with a VNet.



### Lab 3 –  Cross Container App integration and microservice communication

**Objectives**  
1. Create 3 Azure Container Apps - 2 back-end APIs and 1 UI front end - and inegrate them to demonstrate cross Container App integration.
2. Optionally, work through and complete the listed challenge(s).

**Steps**  
1. Create a Container App - for the _inventoryapi_ microservice.   
2. Test the _inventory_ microservice. 
3. Create a Container App - for the _productapi_ microservice.   
4. Test the _productapi_ microservice. 
5. Create a Container App - for the _store_ UI frontend. 
6. Create and configure Environment Variables
7. Test the integrated UI by navigating to the ingress of the _store_ UI frontend.

**Challenges (optional)**
1. Determine – if there are other ways to achieve the same objective - _cross microservice communication_ ? (Hint: Dapr)
2. Explore and implement the same cross-microservice integration scenario with the 3 Container Apps above with Dapr.



```
# Deploy the container-2-dotnet dotnet-app
az containerapp create \
  --name dotnet-app \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image 'ghcr.io/azure-samples/container-apps-connect-multiple-apps/dotnet:main' \
  --target-port 80 \
  --ingress 'internal'

DOTNET_FQDN=$(az containerapp show \
  --resource-group $RESOURCE_GROUP \
  --name dotnet-app \
  --query configuration.ingress.fqdn -o tsv)

# Deploy the container-1-node node-app
az containerapp create \
  --name node-app \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image 'ghcr.io/azure-samples/container-apps-connect-multiple-apps/node:main' \
  --target-port 3000 \
  --ingress 'external' \
  --environment-variables DOTNET_FQDN=$DOTNET_FQDN \
  --query configuration.ingress.fqdn
```



### Lab 4 – KEDA in action with Scale to Zero

**Objectives**  
1. Configure _inventoryapi_ for KEDA scaling with - httptrigger -  for  HTTP handler based scaling down to zero.
2. Optionally, work through and complete the listed challenge(s).


**Steps**  
1. Configure _inventoryapi_ for KEDA scaling with - httptrigger.
2. Observe that replicas are at zero
3. Generate/simulate concurrent user and http requests load using a load testing mechanism of your choice to the _inventoryapi_ ingress URI.
4. Observe that replicas are scaling up as the load test progresses.


**Challenges (optional)**
1. Explore other scalers in KEDA and create a custom scaler implementation of your choice based on KEDA scaled object chosen. 
   _You might need to deploy additional Azure resource based on choices made._

### Lab 5 – Monitoring an ACA app

**Objectives**  
1. Visualize the metrics of the deployed Azure Container Apps using Azure Managed Grafana.
2. Optionally, work through and complete the listed challenge(s).

**Steps**  
1. Deploy an Azure Managed Grafana instance.
2. Configure and Import a Azure Container App workbook.
3. Observe the Grafana dashboard for the metrics visualization. 

**Challenges (optional)**
1. Explore other ways to visualize metrics and implement an Azure native one without using Grafana.



 
