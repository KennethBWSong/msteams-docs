---
title: Provision in the cloud
author: Rajeshwari-v
description:  Describes how to provision in the cloud.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
---

# Provision in the cloud 

TeamsFx provides seamless integration with Azure and M365 cloud so that you can easily put your application in a secure cloud environment. Provision is the first step to deploy an application to cloud. In this step, necessary cloud resources are created in Azure and M365 for your application, but there is no code (HTML, CSS, JavaScript, etc.) is copied to the resources. 
 
## Prerequisites

Before you can provision cloud resources in Azure and M365, you must have the following: 

* A M365 organizational account. 
* An Azure Account with a valid subscription. 
 
> [!NOTE]
> Read account and permission page (link to account page) to learn why these accounts are needed. 
 
## Provision resources

Teams Toolkit provisions cloud resources based on the [Teams application capabilities](add-capabilities.md) and [Azure services](add-resources.md) that you have included in your application. 
 
### M365 Cloud Resources 

For any kind of Teams application, these M365 resources are created in your M365 tenant: 

* Register an application in Teams. (Commonly referred as Teams App ID). 
* Register an application in Azure Active Directory (Commonly referred as AAD App ID). 
 
The following table describes the necessity of mentioned resources:

|Resources | Why my application needs it? |
|----------|--------------------------------|
|Teams application | This is an application **registered in Teams platform** with the information in manifest and identified by a unique GUID.| 
|Azure Active Directory application| This is an application **registered in Azure Active Directory** to represent your Teams Application. This application is used to manage digital identity and permissions for your application so you could achieve features like single sign on and ask for user consent when your application requires additional permission to access user’s data in M365. |
 
### Azure cloud resources by project type 

Teams application can include different capabilities, and Teams Toolkit provides a most appropriate default Azure service that hosts your application workloads. If you project includes multiple capabilities, all necessary Azure services are provisioned. 
(Details Needed)
 
|Teams application capabilities| Azure services| Purposes|
|------------------------------|---------------|----------| 
|Tab <br> To be hosted on Azure |	Azure Storage Account </br> Azure Web App </br> Azure App Service |	Host frontend static content of your tab application. </br> Host a server side workload to handle authentication logic. </br> Defines a set of compute resources for the web app to run, which are analogous to the [server farm](https://en.wikipedia.org/wiki/Server_farm) in conventional web hosting. |
| Tab </br> To be hosted on SharePoint |There is a Teams application registered with Teams Platform but **no Azure services are provisioned.**|   
|Bot (and/or Messaging Extension) | Azure Web App </br> Azure App Service </br> Azure Bot Service | Host server logic for your bot application. </br> Defines a set of compute resources for the web app to run, which are analogous to the [server farm](https://en.wikipedia.org/wiki/Server_farm) in conventional web hosting. </br> Handles communication between your bot application and Teams client. |
 		
> [!NOTE]  
> Azure services incur costs in your subscription, you can refer to [pricing calculator](https://azure.microsoft.com/pricing/calculator/) to understand an estimate. 
 
You can optionally include additional Azure services that serves your application development needs, including: 
* Azure Functions 
* Azure API Management 
* Azure SQL Database 
 
For more information on how to add cloud resources, see [Add cloud resources](add-cloud-resources.md). 
 
### Configuration changes

In addition to creating Azure service instance, Teams Toolkit has also made configuration changes of these services. 
 
(Details Needed) 
|Resources |Configurations|	Reason |
|-----------|-------------|----------|
|Azure Active Directory Application |Includes a delegated Microsoft Graph Permission `User.Read`|With this permission specified in the AAD app, the hello world application created by Teams Toolkit can retrieve user profile from Microsoft Graph.| 
|Azure Storage Account|	Enables Static Content|	This allows static content like HTML, CSS, JavaScript and image files serving from a container.| 
|Bot Channel Registration|AAD app id and client secret |The AAD app id and client secret is configured to handle authentication between your bot and Teams.| 
 
## Find provisioned resources 

Teams Toolkit can provision M365 and Azure resources. 
* For M365 resources, it is created under your tenant. You can learn [how to find your M365 tenant ID](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant). 
* For Azure resources, it iscreated under a new resource group in your subscriptions. 
 
|Resources|	Where to find them|
|---------|-------------------| 
|Teams App ID|	You can find the Teams App ID in your project’s manifest file after you packaged your application. Read about App Package (Link to publish section) </br> You can also find your Teams App ID in [Teams Developer Portal](https://dev.teams.microsoft.com/apps). 
|Azure Active Directory Application|Go to [Azure Portal](https://portal.azure.com/) </br> Navigate to Azure Active Directory section. </br> Navigate to App registrations blade under manage section. 
You canfind your Azure Active Directory application with display name same as your project name. |
|Azure services |Go to [Azure Portal](https://portal.azure.com/) </br> Navigate to Resource groups section.</br> Find a resource group with name of ${yourProjectName}-rg 
You can find all Azure services provisioned in this resource group. |
 
## Perform provision 
 
Note that it’s the same if your project contains multiple capabilities. 
 
### Provision from Teams Toolkit in Visual Studio Code 

1. Activate Teams Toolkit from left side.

    ![Activate Teams Toolkit ](~/assets/images/tools-and-sdks/teams-toolkit.png)

1. In the Teams Toolkit side bar panel, select `Provision in the cloud` option. 

    ![Provision in the cloud ](~/assets/images/tools-and-sdks/provision-in-cloud.png)

1. Select `Provision` if you are ready to create cloud resources, or you can refer to pricing calculator for cost estimation.     

    ![Select provision](~/assets/images/tools-and-sdks/select-provision.png)

    Alternatively, you can open command palette and enter **Teams: Provision in the cloud** .

    ![Alternate provision](~/assets/images/tools-and-sdks/alternate-provision.png)

### Provision from TeamsFx CLI in Command Window 

1. Change directory to your project directory.   
1. Execute command `teamsfx provision`. 

    ![Execute command](~/assets/images/tools-and-sdks/execute-command.png)
   
## Advanced use cases 

There are few common advanced scenarios during cloud resources provision. 
 
### Switch a subscription and re-do provision 
1. Sign-in to [Azure Portal](https://portal.azure.com/) and delete the resource group that was created by Teams Toolkit. 
1. Switch subscription in current account or log out and select a new subscription. 
1. In your project directory, navigate to `.fx/env.default.json` file, change `provisionSucceeded` flag to false. 
1. Go through provision flow again. 
 
### Use an existing Azure Active Directory application 

In certain cases where you don’t have permission to create an Azure Active Directory application, you can use an existing one with following step: 
1. Go to [Azure Portal](https://portal.azure.com/). 
1. Find Azure Active Directory section. 
1. In overview blade, obtain Object ID and Application (client) ID for your AAD application. 

     ![Obtain ID](~/assets/images/tools-and-sdks/obtain-id.png)

1. In Certificates & secrets blade, obtain Client secret by creating a new one. 

    ![Client secret](~/assets/images/tools-and-sdks/client-secret.png)

1. In Manifest blade, find “id” under “oauth2Permissions” and obtain the value of it. 
1. In your project directory, navigate to `.fx/env.default.json ` and update the following value in the `fx-resource-aad-app-for-teams` section. 

    ![Update value](~/assets/images/tools-and-sdks/update-value.png)

1. In your project directory, navigate to `.fx/default.userdata` and update the client secret to `x-resource-aad-app-for-teams.clientSecret=’your-secret’` 
1. Go through provision flow. 
 
### Change default resource group and resource suffix name

To use an existing resource group, change default resource group name, or change the resource suffix name after a provision. 

**To change default resource group and resource suffix name** 

1. Sign-in to [Azure Portal](https://portal.azure.com/) and delete the resource group that was created by Teams Toolkit. 
1. In your project directory, navigate to `.fx/env.default.json` file, change `resourceGroupName`, `resourceNameSuffix` and `resource_base_name`. 
1. In the same file, change `provisionSucceeded` flag to false. 
1. Go through provision flow again. 
 
## See also

* Add additional cloud resources 
* Add additional Teams app capabilities 
* Provision resources with CI/CD pipelines 
* Deploy your project to cloud 