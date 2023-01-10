
# Azure Container Apps Hands-on-Labs

## Overview 
Martha, the CTO of the boutique cloud-native technologies consulting firm - StartUps & More Inc. (SUM Inc.), requires  her consultants to be conversant with emergent technologies and methodologies at a consistent yet fast pace. One of the key decisions she makes with the advent of every new technology, is to determine - it's fit-to-purpose and efficacy - before having her consultants delve deeper themselves and subsequently having them help their clients.

Azure Container Apps (ACA) is the newest offering from Microsoft providing a serverless platform for running containerized microservices, this is on the top of Martha's emerging tech list for a few  important reasons that she has heard so far -
1. ACA can empower developers to build cloud-native solutions focusing on their apps rather than cloud infrastructure. 

   *Something that resonated even more - considering startup teams would rather focus on product differentiation, speedy go-to-market as compared to foundational infrastructure setup, security and Day-2 operations.*

2. ACA is built on the foundation of open-source  Cloud Native Computing Foundation (CNCF) projects like - Kubernetes Event Driven Autoscaling (KEDA) and Distributed Application Runtime (Dapr) which are gaining adoption amongst cloud native developers and ACA inherently utilizing the CNCF Graduated project - Envoy - for its service-proxy functionality.

   *Serverless PaaS powered by CNCF projects to enable developers - sounded like an attractive proposition*

Martha has looped in and tasked two of her top engineers Alice and Bob to conduct a timeboxed hands-on evaluation of ACA. Such a time-boxed evaluation methodology has proven to be a strategic advantage to Martha's firm for many years.

Alice is a Kubernetes expert having worked with several of SUM Inc.'s clients on anything ranging from - large DIY Kubernetes clusters - to - vendor managed Kubernetes offerings including the Azure Kubernetes Service (AKS) from Microsoft. She has recently passed the Certified Kubernetes Administrator & Certified Kubernetes Application Developer exams from the Linux Foundation.

Bob is a polyglot developer - addressing the full-stack of cloud native application development. He is familiar with containerization and orchestration but would rather spend his time building high-performant microservices and applying the needed development rigor driven by well-adopted software development patterns. He is relatively new to Azure.

Alice and Bob proceed on the quest set forth by Martha.

## The First Take

Apart from looking into the official Azure Container Apps [documentation](https://learn.microsoft.com/en-us/azure/container-apps/) and the  studying the [comparison](https://learn.microsoft.com/en-us/azure/container-apps/compare-options#azure-container-apps) of Azure Containers Apps with other Azure Container options --- Alice and  Bob  --- read the following articles by members of the Azure Container Apps Product Group at Microsoft.   

1. Go Cloud Native with Container Apps [link](https://techcommunity.microsoft.com/t5/apps-on-azure-blog/go-cloud-native-with-azure-container-apps/ba-p/3616407)  
2. Journey to the cloud with Azure Container Apps [link](https://techcommunity.microsoft.com/t5/apps-on-azure-blog/journey-to-the-cloud-with-azure-container-apps/ba-p/3622609)  
3. Observability with Azure Container Apps [link](https://techcommunity.microsoft.com/t5/apps-on-azure-blog/observability-with-azure-container-apps/ba-p/3627909)

Having digested the optimal information on Azure Container Apps in a timeboxed manner, both Alice and Bob concur on the prospect this option offer and prepare an executive summary for Martha. The highlight of the summary being a crisp slide as depicted in one of the Microsoft Product Group articles  -  

<img width="746" alt="image" src="https://user-images.githubusercontent.com/25875242/203236769-d9abcbfc-386c-4215-81d6-2f91a345904f.png">



Based on the reassurance of Alice and Bob's presentation, Martha introduces them to a prospective customer of the firm  - **Marketblitz** 
This customer, Martha believes, could be an ideal pilot customer for ACA and could benefit from a set of hands-on-labs for their development team.  

Alice and Bob are tasked with creating the labs with one overarching instruction from Martha - "Keep it simple but not simplistic :)" 

## The Customer - Marketblitz  

Markeblitz is a rapidly growing market research firm which has recently **acquired 2 different startups** and their respective product lines. 

One of the acquisition is a  market analytics firm that develops mostly on the **Microsoft web tech stack** – Dotnet Core , ASP.Net Web API et.al. The other acquisition is a marketing UX firm focusing mostly on **different UI libraries.**

Marketblitz – is at a juncture where they want to consolidate ALL their offerings as a single API suite while ensuring their top talent is retained  and continues to work on their respective areas of expertise. They hope to structure some of the existing **core APIs for internal usage only** – parts of which could be used by the **new API suite which would be customer facing.** After the first phase of consolidation, they expect to beta test – at which point they **foresee some challenges with A/B testing** and are also concerned as to how they will meet **scaling needs** if/when the pilot becomes successful with increasing demand from end-users.  
The Dev team is a mix of developers who are conversant with Azure and the ones who are just getting started on Azure.     
Apart from core concerns, the lean Ops team at Marketblitz would require **insights and visualization of the performance** of the API suite too without them having to spin up and manage any new instrumentation or dashboards.



## The Labs

### Table of Contents
[Prerequisites](#prerequisites)  
[Structure](#structure)         
[Lab 1](#lab-1--create-an-azure-container-app-using-the-azure-portal-and-implement-traffic-split-functionality)   
[Lab 2](#lab-2--create-an-azure-container-app---with-az-cli-commands)  
[Lab 3](#lab-3---cross-container-app-integration-and-microservice-communication)  
[Lab 4](#lab-4--keda-in-action-with-scale-to-zero)  
[Lab 5](#lab-5--monitoring-an-azure-container-app)  

***

### Prerequisites   
1. Access to an Azure subscription with privileges to create Azure resources.   
   -  _If you do not have an entire Azure subscription , access to a Azure resource group with privileges to create Azure resources is required. The labs assume you have a subscription; you would need to skip the resource group creation steps in the relevant labs if you already have the resource group._  
2. [Azure Cloud Shell](https://learn.microsoft.com/en-us/azure/cloud-shell/overview) configured and ready to use. Bash commands/instructions provided in relevant labs.  
    - _Usage of Cloud Shell is favored for users who do not have typical Azure development tools like Azure  CLI installed. Feel free to use your Azure development setup / tooling  if you have one._   
3. Access to pull container images from a public DockerHub container image registry. 
   - _If you cannot or do not want to use the lab specific container images from the public DockerHub repo, source code is provided in the relevant labs with it's Dockerfile - for you to build and push to container registry of your choice.Your container registry and image details would need to be substituted accordingly in the relevant steps of the lab._   
4. Tooling of your choice to test API endpoints. 
   -  _Postman App is utilized here in the relevant labs._   
5. Tooling of your choice to load test API endpoints.  
   -  _[Artillery](https://www.artillery.io/) is utilized here in the relevant labs._
5. Basic understanding of APIs, Containers and Azure Portal UI and UX.
***
### Structure  

Each lab has the following structure -  

**Objectives** - Listing of the key objectives of the lab.  

**Why is it relevant to the customer ?** - This section describes the relevance and reasoning behind why Alice and Bob chose the objectives for the customer - **Marketblitz**  

**Steps** -   A set of detailed steps to follow in an hands-on manner to achieve the objectives.  

**Challenges(optional)** -  While the Objectives and the Steps to achieve them are considered mandatory, every lab has a set of optional Challenges that could be completed with some additional effort on the candidate's part. Highly Recommended.  


***

[<sub><sup>go back to TOC ^</sup></sub>](#table-of-contents)
### Lab 1 – Create an Azure Container App using the Azure Portal and implement traffic-split functionality

**Objectives**

1. Create the environment and test a sample container app using the Azure Portal.   
2. Utilize multiple revisions and test Traffic Split functionality with 2 different versions of the same app.  
As part of the Azure Container App environment creation and deployment,  get familiar with the Azure Portal UI and learn the Azure Container App specific terminologies & features.
3. Optionally, work through and complete the listed challenges.
  ***
**Why is it relevant to the customer ?**   

a. Alice and Bob have crafted this lab to be an easy initiation via the Azure Portal to create Azure resources for the developers in the Marketblitz team just getting started on their Azure journey.  
b. After the creation of the first app, this lab then addresses one of the key  customer requirements - **A/B Testing** -   and how its foundation could be laid via the multiple revisions and the traffic split functionality that is readily available with ACA.

***

**Steps**
1. **Create the sample app** - Download & follow instructions in the 
   [Create the sample app PDF](https://github.com/shankar-r10n/spt-aca-hol/blob/main/Lab1/Lab%201%20-%20Create%20Azure%20Container%20App%20-%20Azure%20Portal.pdf) 
    to create the sample app. Preferably, open this PDF in a PDF viewer or a separate browser window.

   _The  [Lab 1 - Create Azure Container App - Azure Portal.pdf] is inside the [Lab 1] folder in this repo._

   Note 1: Complete all instructions in the PDF and then return to this README.md again - for the next steps of this Lab 1.  
           The PDF is **_only_** for the _Create the sample app_ step.  
  
   Note 2: Please note that the container image for this sample app is pulled from a public Docker repository.    
   If you choose to utilize your own container image repository, utilize the [Lab1\src] folder and the associated Dockerfile to build and push the image to your          container registry of choice / repository  and substitute the values in the Container App creation step for the [Registry login server] and [Image and tag] values.

2. **Enable multiple revisions** -  One of the fundamental steps for Traffic Split is to enable multiple revisions of the app to exist *simultaneously*.

   a. Go to the Container App resource created in Step 1 by clicking on it's resource name in your resource group.  
   b. Select the - _Revision Management_ - link in the left navigation menu as shown below.  
 
   c. Click on the - _Choose revision mode_  - option as depicted in the image below -   
   <img width="1106" alt="image" src="https://user-images.githubusercontent.com/25875242/198933706-5defd2f9-0c9f-41d0-bbdc-857535bd7576.png">
   
   
   d. Then select -  _Multiple: Several revisions active  simultaneously_  and click  _Apply_ 
   <img width="1118" alt="image" src="https://user-images.githubusercontent.com/25875242/198933866-a1d6c8ce-5835-4de7-86d2-3c2883d6e24c.png">

   e. Refresh the page you are on _within_ the Azure Portal and navigate back to same Container App resource and the _Revision Management_ link in the left navigation menu, 
   same as Step 2.b. above.

3. **Create a new revision**   
   a. Click on  **_Create new revision_** as shown below   
 
   <img width="1151" alt="image" src="https://user-images.githubusercontent.com/25875242/198934487-fab429a2-9986-40b9-a785-942b44c63dc0.png">
   
   b. Click on the previously created container image's **_Name_** as shown below in the **_Container Image_** section    
 
   <img width="700" alt="image" src="https://user-images.githubusercontent.com/25875242/198934754-83e0c84d-9fad-4013-9ad0-d5aff1b9d80e.png">
    
   c. In the **_Edit a container_** tab that opens up - Enter the new value for the **_Image and tag_** field as  - dockerr10n/aca-lab1-image:blue - as shown in the         image below and then click **_Save_**   
 
    <img width="1144" alt="image" src="https://user-images.githubusercontent.com/25875242/198935239-7297a15c-d092-4c35-b025-021b06436b61.png">

   d. Now click **_Create_** as shown below 
      
   <img width="676" alt="image" src="https://user-images.githubusercontent.com/25875242/198935953-97198e35-37b0-4eae-be5e-615b50d0d00f.png">

   e. You should now see the new revision appear as shown below -  with **_Traffic_** at 0 % and **_Active_** enabled.   
       
      <img width="1153" alt="image" src="https://user-images.githubusercontent.com/25875242/198936241-bfd83e29-319c-4a1a-bd95-2173a3f60e96.png">

**NOTE:** 2 key aspects to note - (a.) you did not have to create another Container App Environment and  (b.) when a _revision-scope_ change was made by making container configuration and image changes a new revision was automatically created for you.
Read more about Container App Environments [here](https://learn.microsoft.com/en-us/azure/container-apps/environment) and about Revisions [here](https://learn.microsoft.com/en-us/azure/container-apps/revisions)    


     
4. **Create traffic split**  
   a. Now let us create a traffic split of 50 % each to these 2 revisions by editing and entering the values as shown below and then click on **_Save_**
      
      <img width="1153" alt="image" src="https://user-images.githubusercontent.com/25875242/198936732-26b2926b-f65b-4075-bacb-209caf97cebb.png">
  
   b. After the revisions of successfully updated, traffic split is successfully created with the percentage weight we assigned  
   
   <img width="1169" alt="image" src="https://user-images.githubusercontent.com/25875242/198937104-c251d724-d553-415e-b9b9-6fc8d01ab7aa.png">


5. **Test traffic split.**

     a. Navigate to the [Overview] link as shown and click on the [Application Url]   

     <img width="1157" alt="image" src="https://user-images.githubusercontent.com/25875242/198939711-84b5869c-d045-411a-9caf-850dbbd3c664.png">


        
     
    
    b. You should either see a blue or green back ground - and for every _n_ page refreshes you would see that approximately _n/2_ times the page back ground would be 
       blue and then green for the other instances - effectively proving that we have created a traffic split for 2 different revisions of the same Container App that 
       are active simultaneously.   
       You should see one of the 2 following depictions when you refresh the [Application Url] of the [Container App]  
      
      <img width="868" alt="image" src="https://user-images.githubusercontent.com/25875242/198939822-a53d60f4-fc37-4cf9-8069-256ce76e38e7.png">   

      
      **OR** 
      
      
       
      <img width="868" alt="image" src="https://user-images.githubusercontent.com/25875242/198939912-1c43cecd-3f80-422e-a990-b3d0932e509d.png">
 

       
     
   
      
 ***

**Challenges (optional)**
1. Implement a 30/30/40 split for same app - so that traffic split amongst the green, blue and pink revisions.    
   _(Hint: The - dockerr10n/aca-lab1-image:pink - image results in a html page with pink colored background.)_  

2. Inactivate one of the revisions and re-implement 50/50 split so that traffic is split between the green and pink revisions.

 ***
[<sub><sup>go back to TOC ^</sup></sub>](#table-of-contents)
### Lab 2 – Create an Azure Container App - with az cli commands
**Objectives**  
1. Get familiar with the _az cli_ and the _az containerapp_ commands to create the Container App in Lab 1 in a command line driven manner.
2. Optionally, work through and complete the listed challenge(s). 

***
**Why is it relevant to the customer ?**    
a. Nudge Marketblitz's developer team further to get familiar with the Azure command line and scripting options.  
b. Addresses the customer's need for segmenting their API suite - with few APIs for internal only use and others for external use.

***


**Steps**   
**1. Add the needed extensions and register the necessary providers** - required for creating an Azure Container App using the CLI.  
```

# Login to the account if you are using Azure CLI command-line tool that is locally installed 
# Skip this step if you are using Azure Cloud shell. 
az login

# Install the ACA extension for the CLI
az extension add --name containerapp --upgrade

# Register the Microsoft.App namespace
az provider register --namespace Microsoft.App

# Register the Microsoft.OperationalInsights provider for the Azure Monitor Log Analytics workspace if you have not used it before.
az provider register --namespace Microsoft.OperationalInsights

```
**2. Create the sample app using CLI** 
```
# Set the following environment variables

RESOURCE_GROUP="rg-spt-aca-hol1" # your new resource group name 
LOCATION="eastus"
CONTAINERAPPS_ENVIRONMENT="aca-hol-env1" # your new Conatiner Apps environment name 

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
  --name aca-hol-demo1 \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT
  
  
```
After executing the above commands, if you navigate to the resource group you created in the Azure Portal  and click on the newly created Container App you will observe the following as depicted in the image below:
a. Container App is created  
b. Application Url has the value - Ingress Disabled.  

<img width="1150" alt="image" src="https://user-images.githubusercontent.com/25875242/199140106-50274c47-d166-4681-b32c-a871d3d1b918.png"> 

This is to demonstrate the Container App can be created without any ingress. The Container App can later be updated to accept (Ingress) traffic from the Internet.This will be performed during the next step.  

**3. Update the Container App to enable ingress**  

Note: Update the values in the following command to reflect the name of your container app and resource group. 

``` 
az containerapp ingress enable -n aca-hol-demo1 -g rg-spt-aca-hol1 \
    --type external --allow-insecure --target-port 80 --transport auto 
```

After you execute this command, you will get a Application Url in the resultant output in the CLI; you will  have the Url in the *fqdn* value too.   

<img width="696" alt="image" src="https://user-images.githubusercontent.com/25875242/199143610-f0224da6-cab6-4301-ae44-e423e5a55e70.png">
 

Navigate to the above  Url. (Or) 
You could also - Navigate back to the Application URL field (Within overview) in the portal and click on the now populated URL field and you should see the browser result as depicted below.     
  
<img width="1153" alt="image" src="https://user-images.githubusercontent.com/25875242/199144171-23cc193b-6dff-4892-b08a-562dbf6fddd1.png">



**NOTE:** We could have created an ingress enabled Container App as part of the previous step itself by passing in  the _--ingress external_ and _target-port 80_ in the earlier command in Step 2. We did it in 2 parts to demonstrate that it can be enabled after the creation of the Container App.  

**4. Set the revision to Multiple** - enabling multiple revisions of the Container App to exist simultaneously 

```
az containerapp revision set-mode --mode multiple \
                                  --name aca-hol-demo1 \
                                  --resource-group rg-spt-aca-hol1
```

Ensure that you get the output - **"Mutliple"** - which means the revision mode was set successfully  

**5. Create a new revision** - based on the existing revision and using the image -  _docker.io/dockerr10n/aca-lab1-image:blue_   

```
az containerapp revision copy -n aca-hol-demo1 -g rg-spt-aca-hol1 --image "docker.io/dockerr10n/aca-lab1-image:blue"
```
Navigate to the Revision Management configuration page for the Container App within the Azure Portal.  You will see that two revisions exist simultaneously and that the revision we recently created is configured to receive 100 % of the traffic.   

<img width="1151" alt="image" src="https://user-images.githubusercontent.com/25875242/199154522-defc2380-b198-43d6-8335-44428ea91279.png">

And if we navigate to the _Application Url_ - we observe the change with the loading of the blue background page.

<img width="896" alt="image" src="https://user-images.githubusercontent.com/25875242/199154714-417d7087-4b28-466e-aceb-ebe6ecb06bb0.png">


**NOTE:** 2 key aspects to note - (a.) you did not have to create another Container App Environment and  (b.) when a _revision-scope_ change was made by making container configuration and image changes a new revision was automatically created for you.
Read more about Container App Environments [here](https://learn.microsoft.com/en-us/azure/container-apps/environment) and about Revisions [here](https://learn.microsoft.com/en-us/azure/container-apps/revisions)    


**6. Create a traffic split** - of 50-50 each for both these revisions.   

You can list the revisions using the following command ; observe and note down the full revision name of the most 2 revisions that exist.  

```

az containerapp revision list --name aca-hol-demo1 -g rg-spt-aca-hol1

````


The latest revision is now getting 100 % of the ingress traffic; so let us split the ingress traffic between the latest and the revision name of the first revision we created. 
```
az containerapp ingress traffic set -n aca-hol-demo1 \
                -g rg-spt-aca-hol1 \
  --revision-weight latest=50 aca-hol-demo1--d9ggleh=50  
```

After this command is executed, you get the following output depicting that the traffic split has been configured  

<img width="320" alt="image" src="https://user-images.githubusercontent.com/25875242/199157466-85ace811-55d2-4fe5-8a8c-74c5faeabcd7.png">


**7. Test the traffic split** - navigate to the Application Url and refresh the page a few times and you would see 50-50 weighted split between pages with green and blue colored backgrounds. 



**Challenges (optional)**
1. Using the CLI - Implement a 30/30/40 split for same app - so that traffic split amongst the green, blue and pink revisions.     
   _(Hint: The - dockerr10n/aca-lab1-image:pink - image results in a html page with pink colored background.)_ 
2. Using the CLI - Inactivate one of the revisions and re-implement 50/50 split so that traffic is split between the green and pink revisions.
3. Convert the above deployment to an internal only ingress using - _az cli_ .
4. Discuss and explore options you have securing the Container App with a VNet.
   If you are up to it - secure the Container App based on the options and choices you make. (Hint: You may need to create a new Container Apps Environment based on choices you make and then redeploy the app.)

***

[<sub><sup>go back to TOC ^</sup></sub>](#table-of-contents)
### Lab 3 –  Cross Container App integration and microservice communication

**Objectives**  
1. Create 3 Azure Container Apps - 2 back-end APIs and 1 UI front end - and integrate them to demonstrate cross Container App integration.  

 <img width="679" alt="image" src="https://user-images.githubusercontent.com/25875242/203225991-b987933a-b0f7-4128-935d-696bc7b13950.png">


2. Optionally, work through and complete the listed challenge(s).  

**NOTE:**  -  
a. Please note that the container images for the 2 APIs and 1 UI - are pulled from a public Docker repository in this lab.    
   If you choose to utilize your own container image repository, utilize the [Lab3\src] folder and the associated Dockerfiles to build and push the images to your          container registry of choice / repository and substitute the values in the relevant steps.  

b. The source code for the 3 container apps used in the lab to follow is taken from the following sample: - https://github.com/Azure-Samples/dotNET-FrontEnd-to-BackEnd-on-Azure-Container-Apps  
***
**Why is it relevant to the customer ?**   

Applies to the customer scenario  where different teams own their set of core APIs but there is a need for API integration and cross-service usage - arising from Marketblitz's acquisition of 2 different companies.  

***

**Steps**  
**1. Create a Container App - for the _inventoryapi_ microservice.**  

 
```
# Assuming the  Resource Group and Container App environment are already created as part of Lab 2 
# if not create them.
# Set the following environment variables

 RESOURCE_GROUP="rg-spt-aca-hol1"  
 CONTAINERAPPS_ENVIRONMENT="aca-hol-env1"  

# Deploy the Container App for the inventoryapi microservice
az containerapp create \
  --name inventoryapi \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image 'docker.io/dockerr10n/storeinventoryapi:latest' \
  --target-port 80 \
  --ingress 'external' \
  --query configuration.ingress.fqdn
  
 ```
  After the command is executed successfully, make a note of the App Url that is emitted in output.  

**2. Test the _inventoryapi_ Container App**  

  In the Postman Client, enter the URI as depicted below for the HTTP GET call and the expected a result of a random number denoting the inventory count of the           productId passed as part of the URI is returned in response.  

  HTTP GET URI : **https://**_< yourInventoryAPIAppURL >_**/inventory/**_< any-alphanumeric-string-representative-of-productId >_

<img width="1159" alt="image" src="https://user-images.githubusercontent.com/25875242/199887734-8fc71b6a-ed5d-4b68-add2-f532f45b5d53.png">


**3. Create a Container App - for the _productsapi_ microservice**  
 ```   
# Deploy the Container App for the productsapi microservice
az containerapp create \
  --name productsapi \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image 'docker.io/dockerr10n/storeproductapi:latest' \
  --target-port 80 \
  --ingress 'external'
  
 ```
  After the command is executed successfully, make a note of the App Url that is emitted in output.   

**4. Test the _productsapi_  Container App**  
  In the Postman Client, enter the URI as depicted below for the HTTP GET call and the expected a result of a randomized collection of 10 product names with their       productId.  

  HTTP GET URI : **https://**_< yourProductsAPIAppURL >_**/products**     
  
  <img width="1139" alt="image" src="https://user-images.githubusercontent.com/25875242/199889135-b5dc5328-ffd3-4daa-a04c-a2164f634294.png">


**5. Create a Container App - for the _store_ UI frontend**  

```
az containerapp create \
  --name store \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image 'docker.io/dockerr10n/store:latest' \
  --target-port 80 \
  --ingress 'external'  
  
 ```
  After the command is executed successfully, make a note of the App Url that is emitted in output. 

**6. Create and configure Environment Variables** 

In order for the UI store front Container App - to utilize the data obtained from the 2 backend API Container Apps - inventoryapi and productsapi -- we must create and set the  environment variables expected within the **store** Container App.  

```
# Create the value needed for the  - InventoryApi - environment variable
INVENTORY_FQDN=$(az containerapp show \
  --resource-group $RESOURCE_GROUP \
  --name inventoryapi \
  --query properties.configuration.ingress.fqdn -o tsv)

# Set the - InventoryApi - environment variable
az containerapp update -n store -g $RESOURCE_GROUP  --set-env-var  "InventoryApi=https://$INVENTORY_FQDN"

# Create the value needed for the  - ProductsApi - environment variable
PRODUCT_FQDN=$(az containerapp show \
  --resource-group $RESOURCE_GROUP \
  --name productsapi \
  --query properties.configuration.ingress.fqdn -o tsv)

# Set the - ProductsApi - environment variable
az containerapp update -n store -g $RESOURCE_GROUP  --set-env-var  "ProductsApi=https://$PRODUCT_FQDN"

```

**7. Test the integrated UI by navigating to the App Url of the _store_ Container App - our UI frontend** 

Navigate to the App Url of the _store_ Container App.  
You should see the following page render with the _Campaign Product_ data being obtained from the _productsapi_ Container App and the _Inventory_ column data being obtained from the _inventoryapi_ Container App. 

<img width="902" alt="image" src="https://user-images.githubusercontent.com/25875242/199593495-e1a5af7c-84f7-4530-aa87-f6a3fc2d5208.png">


**Challenges (optional)** 

1. Determine – if there are other ways to achieve the same objective - _cross microservice communication_ ? (Hint: Dapr)
2. Explore and implement the same cross-microservice integration scenario with the 3 Container Apps above with Dapr.



[<sub><sup>go back to TOC ^</sup></sub>](#table-of-contents)
### Lab 4 – KEDA in action with Scale to Zero

**Objectives**  
1. Configure _inventoryapi_ for KEDA scaling with - httptrigger -  for  HTTP handler based scaling down to zero.
2. Optionally, work through and complete the listed challenge(s).
***
**Why is it relevant to the customer ?**  

Marketblitz customer demand to increase during the beta testing phase and would like to be in a position to adapt to the demand without sunken costs. 

***


**Steps**  
1. Configure _inventoryapi_ for KEDA scaling with - httptrigger   
a.   
<img width="907" alt="image" src="https://user-images.githubusercontent.com/25875242/199890528-58f5a68d-08d6-472f-8ea8-4b53ae22cc0b.png">

b.  
<img width="782" alt="image" src="https://user-images.githubusercontent.com/25875242/199890642-fbbfeb3b-fd81-49a8-a8b2-96dd92152c45.png">

c.  
<img width="1153" alt="image" src="https://user-images.githubusercontent.com/25875242/199891196-acd2a1f9-28d9-41dd-955a-9d3dac961db6.png">


d.  
<img width="811" alt="image" src="https://user-images.githubusercontent.com/25875242/199891301-403766ff-a538-4e82-8f45-5805068445c0.png">

e. After you click _Create_ a new revision is deployed for the Container App and the scale rule is configured successfully. 

<img width="1152" alt="image" src="https://user-images.githubusercontent.com/25875242/199891577-3fe86640-cad1-42de-a315-5b3005e7dd20.png">



2. Observe that replicas are at zero  

<img width="929" alt="image" src="https://user-images.githubusercontent.com/25875242/199892941-d8d35706-1ee4-44dd-b0d2-345f226de8b4.png">

3. Generate/simulate concurrent user and http requests load using a load testing mechanism of your choice to the _inventoryapi_ App Url   

<img width="1192" alt="image" src="https://user-images.githubusercontent.com/25875242/199894281-e5a7b5f0-4d71-40bd-989e-e5deb58238a1.png">


4. Observe that replicas are scaling up as the load test progresses  
<img width="908" alt="image" src="https://user-images.githubusercontent.com/25875242/199895078-4cb35374-19ac-4f49-8a6f-99ddfd23b92d.png">


**Challenges (optional)**
1. Utilize the az cli (as containerapp) to achieve the same objectives of Lab 4.
2. Explore other scalers in KEDA and create a custom scaler implementation of your choice based on KEDA scaled object chosen. 
   _You might need to deploy additional Azure resource(s) based on choices made._

[<sub><sup>go back to TOC ^</sup></sub>](#table-of-contents)
### Lab 5 – Monitoring an Azure Container App

**Objectives**  
1. Visualize the metrics of the deployed Azure Container Apps using Azure Managed Grafana.
2. Optionally, work through and complete the listed challenge(s).
***
**Why is it relevant to the customer ?**   

Marketblitz's lean Ops team requires dashboards and insights into performance / operational metrics of the API suite but without them having to spin up and manage dashboards.  


***

**Steps**  
1. Deploy an Azure Managed Grafana instance 

   a.   
   <img width="1119" alt="image" src="https://user-images.githubusercontent.com/25875242/199895909-31cce470-abab-4e0a-97a1-d19a786f8887.png">

   b.   
   <img width="692" alt="image" src="https://user-images.githubusercontent.com/25875242/199896009-5d29ec8a-44af-4b50-88a8-e10290a341dd.png">

  c.   
  <img width="617" alt="image" src="https://user-images.githubusercontent.com/25875242/199896250-0471ca51-b131-4c12-8a15-6d8e5d6b4f6d.png">



2. Configure and Import a Azure Container App workbook 
   
   a. Navigate to the _Endpoint_ of the Azure Managed Grafana resource you created in Step 1 of Lab 5. 
   
   <img width="1081" alt="image" src="https://user-images.githubusercontent.com/25875242/199998463-8f03ef62-d49d-445e-a2a1-cd4bd3bbbb17.png">

   b. Click on _Import_ as shown below  
   
   <img width="674" alt="image" src="https://user-images.githubusercontent.com/25875242/199999434-311e2b2f-c629-4ac1-a367-606c11528ff9.png">
   
   c. We will now import the [Grafana Dashboard](https://grafana.com/grafana/dashboards/16592-azure-container-apps-container-app-view/)  -   
      So, navigate to the above link and click on _Copy ID to clipboard_ (the ID is currently 16592) and  _Load_ it as shown below -  
      
      <img width="953" alt="image" src="https://user-images.githubusercontent.com/25875242/200004813-b3c1718b-c86a-457c-bc8d-69bb2e68f297.png">

       
      
             
    e. Proceed to _Import_ it after selecting _Azure Monitor_ as the source as shown below   
    
    <img width="697" alt="image" src="https://user-images.githubusercontent.com/25875242/200005101-b0dd8397-f8f5-49fd-8aa3-c564914cfed5.png">

       
      



3. Observe the Grafana dashboard for the metrics visualization. 

   a. Observe the dashboard after selecting the appropriate - Subscription, Resource Group and then choose the _inventoryapi_ Container App we created previously. 
      You will observe the resource  allocations for CPU and Memory. With no recent activity / load testing - the _Max Request Count_ and _Max Replica Count_ should         also show 0.
      
      <img width="1157" alt="image" src="https://user-images.githubusercontent.com/25875242/200002233-0f15fd5a-1467-4a90-8885-86be725dbeb9.png">


   b. Generate/simulate concurrent user and http requests load using a load testing mechanism of your choice to the _inventoryapi_ App Url   

      <img width="1192" alt="image" src="https://user-images.githubusercontent.com/25875242/199894281-e5a7b5f0-4d71-40bd-989e-e5deb58238a1.png">
      
   c. Now observe the dashboard for changes in values. Scroll down the dashboard to the various sections to observe what this pre-built dashboard provides for               visualization.  
      
      <img width="1149" alt="image" src="https://user-images.githubusercontent.com/25875242/200003027-9ade1e6e-f28a-43f1-acf2-1ab6d21f3e1d.png">


**Challenges (optional)**
1. Explore other ways to visualize metrics and implement an Azure native one without using Grafana.



 
