# Azure Container Apps Hands-on-Labs

## Overview 
Martha, the CTO of the boutique cloud-native technologies consulting firm - StartUps & More Inc. (SUM Inc.), requires  her consultants to be conversant with emergent technologies & methodologies at a consistent yet fast pace. One of the key decisions she makes with the  advent of every new technology is to determine - it's fit-to-purpose & efficacy - before having her consultants delve deeper themselves & consequently having them help their firm's clients.

Azure Container Apps (ACA) - the newest offering from Microsoft providing a serverless platform for running containerized microservices  - is on the top of Martha's emerging tech list for a few  important reasons that she has heard so far -
1. ACA can empower developers to build cloud-native solutions focusing on their apps rather than cloud infrastructure. 

   *Something that resonated even more - considering startup teams would rather focus on product differentiation, speedy go-to-market as compared to foundational infrastructure setup, security & Day-2 operations.*

2. ACA is built on the foundation of open-source  Cloud Native Computing Foundation (CNCF) projects like - Kubernetes Event Driven Autoscaling (KEDA) and Distributed Application Runime (Dapr) which are gaining adoption amongst cloud nativedevelopers  & ACA inherently utilizing the CNCF Graduated prooject - Envoy - for its service-proxy functionality.

   *Serverless PaaS powered by CNCF projects to enable developers - sounded like an attractive proposition*

BUT all of this was *still* a surmise ; Martha has looped in and tasked two of her top engineers Alice and Bob to conduct a timeboxed evaluation resulting in key findings based on hands-on evaluation. 
This time-boxed evaluation methodology has proven to be a strategic advantage to Martha's firm for many years.

Alice is a Kubernetes expert having worked with several of SUM Inc.'s clients on anything ranging from - large DIY Kubernetes clusters - to - vendor managed Kubernetes offerings including the Azure Kubernetes Service (AKS) from Microsoft. She has recently aced the Certified Kubernetes Administrator & Certified Kuberneted Application Developer - exams from the Linux Foundation.

Bob is a polyglot developer - addressing  the full-stack of cloud native application development. He is familiar with containerization & orchestration but would rather spend his time building high-performant microservices and applying the needed development rigor driven by well-adopted software development patterns.

Alice and Bob - proceed on the quest set forth by Martha.

## The First Take & next steps

*Alice and Bob - readup on some key documentation, announcements from the Microsoft Product Group and some reference material to utilize as part of the ongoing assessment.*


*To be done*

## Executive summary

*Crisp tabulation of Alice and Bob's findings reported back to Martha before getting the approval to proceed on the hands-on-evaluation and labs*

*To be done*

## The Labs


### Lab 1 – Create an Azure Container Apps service using the Azure Portal.

**Objectives:**
a. Create the environment & test a simple container app using the Azure Portal.
b. Utiize multiple revisions and test Traffic Split functionality with 2 different versions of the same app.
As part of the environment creation & deployment  get familiar with the UI and learn the Azure Container App specific terminologies & features.

1.a. Create a Container App environment & test a simple app

In the Azure Portal, click on [+ Create a Resource] and type in "Container App"

<<Insert Image 1>>

<<Insert Image 2>>




[Create Container App - Basics] tab
<< Insert pre-filled Basics tab image>>


Project Details

Choose the [Subscription] you would like to use.
It is recommended that you create a new resource group so fill in a name & create a new resource group by clicking on the [Create New] hyperlink.
Provide a [Container app name] of your choice _e.g. aca-hol-demo_


Container Apps Environment

Choose the [Region] you want to deploy to from the drop-down of available regions.

As it is the first time, click on the [Create new] hyperlink to create a new [Container Apps Environment]

<<Insert image of Create Container Apps Environment - Basics>> tab
**[Create Container Apps Environment - Basics] tab**

Environment details

Provide an [Environment name] 

Zone Redundancy (ZR) - The decision to make this Container App Environment - zone redundant is to be made at deployment time. The Container App Environment cannot be made zone redundant If NOT deployed as zone redundant at the time of creation.
For Lab 1 - let us leave [Zone redundancy] as [Disabled]


[Create Container Apps Environment - Monitoring] tab

A [Log Analytics workspace] name is pre-populated for you. You can choose to [Create new] using the link.
<<Insert image of Create Container Apps Environment - MOnitoring tab>>

[Create Container Apps Environment - Networking] tab

Virtual Network

For Lab 1 - we are not going to choose a own virtual network (VNet). So choose [No]

But for future reference, choose [Yes]  just to make a note of this part for when you create an container app environment beyond this lab - that you get to choose an existing VNet or [Create new].
  
And then observe the menu to provide the [Infrastructure subnet] range.

The choice to have the Virtual IP as [Internal] only with the endpoint being an internal load balancer [OR] to expose the apps on an internet accessible IP address is also made here.

Now, revert to choosing [No] and click [Create]

<<Insert image of Create Container Apps Environment - Networking tab>>


  **[Create Container Apps Environment - App Settings] tab**

<<Insert image of Create Container Apps Environment - App Settings tab>>

Uncheck the [Use quickstart image] check-box as we want to deploy our own simple app; the container image of our app is in the public Docker Hub.

[Container details]
  
[Name] Provide a name for the container
[Image Source] Select [Docker Hub or other registries]
[Image type]   Select [Public]
  
 [Registry login server] can be retained as [docker.io]
 
 [Image and tag] Enter the value [ dockerr10n/aca-hol-image:A ] 
  
 [Container resource allocation] - FOr this lab retain the default first value but observe that there is a set of choices that can be made based on your container's  CPU and memory requirements.

Application ingress settings

[HTTP Ingress]    - Check/ enable the checkbox

[Ingress traffic] - Select the [Accepting traffic from anywhere] button.

[Target port]      - Enter 80
 
 







### Lab 2 – Create an ACA service – scripted mode

*Create/ utilize a shell script that enables az cli creation.* 

*In Progress* 

*Running parallel to Lab 1 - extracting the [az cli] commands to achieve everything in Lab 1 in cli-driven manner; makes notes on what can be done only in the portal*

*(Optional) Achieve the same objective as Lab 1 with Bicep. Start lab by Intro and hands-on simple sample of Bicep. *

*To be done*

### Lab 3 – Deploy and test a workload.

*A representative workload (using both UI and backend API)*

*To be done*


### Lab 4 – KEDA in action with Scale to Zero

*Introduce KEDA, hands-on sample with AKS (if needed) , then contrast with ACA ease of use and incorporate HTTP handler based scaling down to zero.*
*To be done*

### Lab 5 – Monitoring an ACA app

*Monitoring fundamentals driven by the Log Analytics workspace. Visualize the monitoring with an Azure native option*

*To be done*


### Lab 6 – ACA versioning using [Revisions]

*Exercise introducing multiple iterative changes including app scope changes and enabling audience to learn how Revisions in ACA help with versioning.*

*To be done*



 
