# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*

### Assess app changes that would change your decision.

## Costs

### General Overview

The cost of a cloud infrastructure deployment depends largely on the resources of the deployed machines.  
Among these are processing power, ram, storage space, online time, software licenses.  

This will depend on the requirements of our application.  
Normally conditioned by the number of users / requests it will have to face, and the corresponding SLU.  

Azure's pricing calculator is a great help to estimate possible costs before deploying and save us from unpleasant surprises for our budget.  

https://azure.microsoft.com/en-us/pricing/calculator/  

We will also have to take into account the cost of other services that our app may requiere, as we have already mentioned.  

Among these costs we can enumerate:  

- Azure Storage  
- Azure SQL Database  
- Azure VM  
- Software Licenses (Windows, SQL)  
- Domain name / hosting  
- SSL Certificates  

We can compare prices of a WM and Azure App Service:  

### Azure App Services  

Azure App Services has several tiers, with different instances in each tier.  
For the most basic tier a B1 instance is at the time of writing a virtual machine capable of running with the following resources:  

- 1 Core
- 1.75GB RAM
- 10GB storage
- Linux OS
- Would cost USD 0.018 / hour (West US)

### Virtual Machine

At the time of writing a virtual machine capable of running with the most similar resources of the previous AAS, is a A1 instance, with following resources:  

- 1 Core  
- 1.75GB RAM  
- 40GB storage
- Linux OS
- Would cost USD 0.06 / hour (West US)

### Comparison

Using 730h per month. Azure App Services cost $13.14 againts $43.85 of a Azure VM A1. 3 Times more.  

## Availabilty  

Azure Virtual Machine  

Having control of a virtual machine gives us much more control of the actions to be performed, but as we have seen in the course, this control implies an effort in the configuration of the machine and its security.

Just like with real machines, we can configure the VM to be available only when needed, for example during office hours, and not on weekends.
This would help to reduce the running costs of our application.

Azure App Services  

An application in Azure has fewer options, it is a service that is available until we cancel it.

https://azure.microsoft.com/en-us/services/app-service/

## Scalability  

**Azure Virtual Machine**  

Azure Virtual Machines has a maximum limit of:  

- 416 Cores
- 5700GB RAM
- 8192GB Storage

That M416s instance would cost $46,051 per month ($64.454 per hour). So its not a problems. Even we can use several clusters.  

We have to be aware that whether we scale vertically or horizontally, our application has to be designed to take advantage of it. Otherwise we are burning money.  
There is no point in multiple cores if the application does not run multiple threads and compute operations in parallel.  
An application in Azure has fewer options, it is a service that is available until we cancel it.  

Azure App Services
Azure App Services has a maximum limit of:  

- 8 Cores
- 32GB RAM
- 250 GB Storage  

Storage can be added using other Azure services. That is plenty for an instance of an app.  In this case is more used the horizontal scaling.  

## Workflow  

Azure Virtual Machine  

A Virtual Machine is a PaaS. So we must handle installation, upgrades, and security of the machine. Even many of this operations can be automatizated, you need more expertice, and be always on track. Patch a system without messing with incompatibilities of other apps or services is an art.  "With great power there must also come great responsibility".  

Azure App Services  
App Services is a SaaS, so we don't need to get worried about system issues. So is easier for the client side.
One the CI/CD approach to releasing new versions is learned, is a lot simpler to deploy on Azure App Services.
In the course we have learned how to do it with Github Actions. When a new commit is released in the repository, the app is deployed again. We can also use automated testing to avoid problems before updating the app.  

## Recommendation  

As we just want to run a web service. Is recommended the use of Azure App Services.  
THat is also the workflow that we learned along the course. And that allowed people achieved without knowing system administration, that will requiere a virtual machine.  
Also our requeriments for the app are not so big that can¡t be handle easily with a basic instance of a Azure App Services.  

One advantage of Azure is that we can latter move to a VM.  