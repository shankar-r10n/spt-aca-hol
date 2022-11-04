# Azure Container Apps Hands-on-Labs

## Overview 
Martha, the CTO of the boutique cloud-native technologies consulting firm - StartUps & More Inc. (SUM Inc.), requires  her consultants to be conversant with emergent technologies and methodologies at a consistent yet fast pace. One of the key decisions she makes with the advent of every new technology, is to determine - it's fit-to-purpose and efficacy - before having her consultants delve deeper themselves and subsequently having them help their clients.

Azure Container Apps (ACA) is the newest offering from Microsoft providing a serverless platform for running containerized microservices, this is on the top of Martha's emerging tech list for a few  important reasons that she has heard so far -
1. ACA can empower developers to build cloud-native solutions focusing on their apps rather than cloud infrastructure. 

   *Something that resonated even more - considering startup teams would rather focus on product differentiation, speedy go-to-market as compared to foundational infrastructure setup, security and Day-2 operations.*

2. ACA is built on the foundation of open-source  Cloud Native Computing Foundation (CNCF) projects like - Kubernetes Event Driven Autoscaling (KEDA) and Distributed Application Runime (Dapr) which are gaining adoption amongst cloud nativedevelopers and ACA inherently utilizing the CNCF Graduated prooject - Envoy - for its service-proxy functionality.

   *Serverless PaaS powered by CNCF projects to enable developers - sounded like an attractive proposition*

Martha has looped in and tasked two of her top engineers Alice and Bob to conduct a timeboxed, hands-on evaluation, such a time-boxed evaluation methodology has proven to be a strategic advantage to Martha's firm for many years.

Alice is a Kubernetes expert having worked with several of SUM Inc.'s clients on anything ranging from - large DIY Kubernetes clusters - to - vendor managed Kubernetes offerings including the Azure Kubernetes Service (AKS) from Microsoft. She has recently passed the Certified Kubernetes Administrator & Certified Kuberneted Application Developer exams from the Linux Foundation.

Bob is a polyglot developer - addressing the full-stack of cloud native application development. He is familiar with containerization and orchestration but would rather spend his time building high-performant microservices and applying the needed development rigor driven by well-adopted software development patterns.

Alice and Bob proceed on the quest set forth by Martha.

## The First Take and next steps

*Alice and Bob - read up on the following documentation and announcements from Microsoft Engineering*


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
1. **Create the sample app** - Download & follow instructions in the 
   [Create the sample app PDF](https://github.com/shankar-r10n/spt-aca-hol/blob/main/Lab1/Lab%201%20-%20Create%20Azure%20Container%20App%20-%20Azure%20Portal.pdf) 
    to create the sample app.  

   _The  [Lab 1 - Create Azure Container App - Azure Portal.pdf] is inside the [Lab 1] folder in this repo._

   Note 1: Complete all instructions in the PDF and then return to this README.md again - for the next steps of this Lab 1.  
           The PDF is **_only_** for the _Create the sample app_ step.  
  
   Note 2: Please note that the container image for this sample app is pulled from a public Docker repository.    
   If you choose to utilize your own container image repository, utilize the [Lab1\src] folder and the associated Dockerfile to build and push the image to your          repository and substitute the values in the Container App creation step for the [Registry login server] and [Image and tag] values.

2. **Enable multiple revisions** -  One of the fundamental steps for Traffic Split is to enable multiple revisions of the app to exist *simultaneously*.

   a. Go to the Container App resource created in Step 1 by clicking on it's resource name in your resource group.  
   b. Select the - _Revision Management_ - link in the left navigation menu as shown below.  
 
   c. Click on the - _Choose revision mode_  - option as depicted in the image below -   
   <img width="1106" alt="image" src="https://user-images.githubusercontent.com/25875242/198933706-5defd2f9-0c9f-41d0-bbdc-857535bd7576.png">
   
   
   d. Then select -  _Multiple: Several revisions active  simultaneously_  and click  _Apply_ 
   <img width="1118" alt="image" src="https://user-images.githubusercontent.com/25875242/198933866-a1d6c8ce-5835-4de7-86d2-3c2883d6e24c.png">

   e. Refresh the page you are on the Azure Portal and navigate back to same Container App resource and the _Revision Management_ link in the left navigation menu, 
   same as Step 2.b. above.

3. **Create a new revision**   
   a. Click on  **_Create new revision_** as shown below   
 
   <img width="1151" alt="image" src="https://user-images.githubusercontent.com/25875242/198934487-fab429a2-9986-40b9-a785-942b44c63dc0.png">
   
   b. Click on the **_Name_** as shown below in the **_Container Image_** section    
 
   <img width="700" alt="image" src="https://user-images.githubusercontent.com/25875242/198934754-83e0c84d-9fad-4013-9ad0-d5aff1b9d80e.png">
    
   c. In the **_Edit a container_** tab that opens up - Enter the new value for the **_Image and tag_** field as  - dockerr10n/aca-lab1-image:blue - as shown in the         image below and then click **_Save_**   
 
    <img width="1144" alt="image" src="https://user-images.githubusercontent.com/25875242/198935239-7297a15c-d092-4c35-b025-021b06436b61.png">

   d. Now click **_Create_** as shown below 
      
   <img width="676" alt="image" src="https://user-images.githubusercontent.com/25875242/198935953-97198e35-37b0-4eae-be5e-615b50d0d00f.png">

   e. You should now see the new revision appear as shown below -  with **_Traffic_** at 0 % and **_Active_** enabled.   
       
      <img width="1153" alt="image" src="https://user-images.githubusercontent.com/25875242/198936241-bfd83e29-319c-4a1a-bd95-2173a3f60e96.png">

     
4. **Create traffic split**  
   a. Now let us create a traffic split of 50 % each to these 2 revisions by editing and entering the values as shown below and then click on **_Save_**
      
      <img width="1153" alt="image" src="https://user-images.githubusercontent.com/25875242/198936732-26b2926b-f65b-4075-bacb-209caf97cebb.png">
  
   b. After the revisions of successfully updated, traffic split is successully created with the percent weigthage we assigned  
   
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

### Lab 2 – Create an Azure Container App - with az cli commands
**Objectives**  
1. Get familiar with the _az cli_ and the _az containerapp_ commands to create the Container App in Lab 1 in a command line driven manner.
2. Optionally, work through and complete the listed challenge(s).

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

This is to demonstrate the Container App can be created without any ingress. And that it can be updated to have the Ingress accepting traffic from anywhere in the internet as we are going to show in the next step.  

**3. Update the Container App to enable ingress**  

``` 
az containerapp ingress enable -n aca-hol-demo1 -g rg-spt-aca-hol1 \
    --type external --allow-insecure --target-port 80 --transport auto 
```

After you execute this command, you will get a Application Url in the resultant output in the CLI; you will  have the Url in the *fqdn* value too.   

<img width="696" alt="image" src="https://user-images.githubusercontent.com/25875242/199143610-f0224da6-cab6-4301-ae44-e423e5a55e70.png">
 

Navigate to this Url and you should see the browser result as depicted below   
  
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
Now, if you navigate to the  _Revision Management_ link in the left navigation you will observe that 2 revisions exist simultaneously and that the revision we recently created is configure to get 100 % of the traffic.  

<img width="1151" alt="image" src="https://user-images.githubusercontent.com/25875242/199154522-defc2380-b198-43d6-8335-44428ea91279.png">

And if we navigate to the _Application Url_ - we observe the change with the loading of the blue background page.

<img width="896" alt="image" src="https://user-images.githubusercontent.com/25875242/199154714-417d7087-4b28-466e-aceb-ebe6ecb06bb0.png">

**6. Create a traffic split** - of 50-50 each for both these revisions. 

The latest revision is now getting 100 % of the ingress traffic; so let us split the ingress traffic between the latest and the revison name of the first revision we created. 
```
az containerapp ingress traffic set -n aca-hol-demo1 \
                -g rg-spt-aca-hol1 \
  --revision-weight latest=50 aca-hol-demo1--d9ggleh=50  
```

After this command is executed, you get the following output depicting that the traffic split has been configured  

<img width="320" alt="image" src="https://user-images.githubusercontent.com/25875242/199157466-85ace811-55d2-4fe5-8a8c-74c5faeabcd7.png">


**7. Test the traffic split** - navigate to the Application Url and refresh the page a few times and you would see 50-50 weighted split between pages with green and blue collored backgrounds. 



**Challenges (optional)**
1. Using the CLI - Implement a 30/30/40 split for same app - so that traffic split amongst the green, blue and pink revisions.     
   _(Hint: The - dockerr10n/aca-lab1-image:pink - image results in a html page with pink colored background.)_ 
2. Using the CLI - Inactivate one of the revisions and re-implement 50/50 split so that traffic is split between the green and pink revisions.
3. Convert the above deployment to an internal only ingress using - _az cli_ .
4. Secure the above deployment with a VNet.

***


### Lab 3 –  Cross Container App integration and microservice communication

**Objectives**  
1. Create 3 Azure Container Apps - 2 back-end APIs and 1 UI front end - and inegrate them to demonstrate cross Container App integration.
2. Optionally, work through and complete the listed challenge(s).

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
  After the command is executed successfuly, make a note of the App Url that is emitted in output.  

**2. Test the _inventoryapi_ Container App**  

  In the Postman Client, enter the URI as depicted below for the HTTP GET call and the expected a result of a random number denoting the inventory count of the           productId passed as part of the URI is returned in response.  

  HTTP GET URI : _https://<yourInventoryAPIAppURL>/inventory/<any-alphanumeric-string-representative-of-productId>_  

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
  After the command is executed successfuly, make a note of the App Url that is emitted in output.   

**4. Test the _productsapi_  Container App**  
  In the Postman Client, enter the URI as depicted below for the HTTP GET call and the expected a result of a randomized collection of 10 product names with their       productId.  

  HTTP GET URI : _https://<yourProdcutsAPIAppURL>/product/   
  
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
  After the command is executed successfuly, make a note of the App Url that is emitted in output. 

**6. Create and configure Environment Variables** 

In order for the UI store front Contaniner App - store to utilize the data obatined from the 2 backend API Container Apps - inventoryapi and productsapi -- let us create and configure the needed environment variables utilized by the **store** Container App.  

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

You should see the following page render with the _Campaign Product_ data being obtained from the _productsapi_ Container App and the _Inventory_ column data being obtained from the _inventoryapi_ Container App. 

<img width="902" alt="image" src="https://user-images.githubusercontent.com/25875242/199593495-e1a5af7c-84f7-4530-aa87-f6a3fc2d5208.png">


**Challenges (optional)** 

1. Determine – if there are other ways to achieve the same objective - _cross microservice communication_ ? (Hint: Dapr)
2. Explore and implement the same cross-microservice integration scenario with the 3 Container Apps above with Dapr.




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

### Lab 5 – Monitoring an Azure Container App

**Objectives**  
1. Visualize the metrics of the deployed Azure Container Apps using Azure Managed Grafana.
2. Optionally, work through and complete the listed challenge(s).

**Steps**  
1. Deploy an Azure Managed Grafana instance.
2. Configure and Import a Azure Container App workbook.
3. Observe the Grafana dashboard for the metrics visualization. 

**Challenges (optional)**
1. Explore other ways to visualize metrics and implement an Azure native one without using Grafana.



 
