# -Implement-Web-Apps-in-Azure
 Implement Web Apps in Azure Cloud 
--
## Lab introduction

In this lab, you learn about Azure web apps. You learn to configure a web app to display a Hello World application in an external GitHub repository. You learn to create a staging slot and swap with the production slot. You also learn about autoscaling to accommodate demand changes.

This lab requires an Azure subscription. Your subscription type may affect the availability of features in this lab. You may change the region, but the steps are written using East US.


## Lab scenario

Your organization is interested in Azure Web apps for hosting your company websites. The websites are currently hosted in an on-premises data center. The websites are running on Windows servers using the PHP runtime stack. The hardware is nearing end-of-life and will soon need to be replaced. Your organization wants to avoid new hardware costs by using Azure to host the websites. 

## Interactive lab simulations

There are interactive lab simulations that you might find useful for this topic. The simulation lets you to click through a similar scenario at your own pace. There are differences between the interactive simulation and this lab, but many of the core concepts are the same. An Azure subscription is not required.

+ [Create a web app](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%202). Create a web app that runs a Docker container.
    
+ [Implement Azure web apps](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%2013). Create an Azure web app, manage the deployment, and scale the app. 

## Architecture diagram
<img width="661" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/bf88c6cd-c271-403d-9453-9d45bca79812">


## Job skills

+ Task 1: Create and configure an Azure web app.
+ Task 2: Create and configure a deployment slot.
+ Task 3: Configure web app deployment settings.
+ Task 4: Swap deployment slots.
+ Task 5: Configure and test autoscaling of the Azure web app.

## Task 1: Create and configure an Azure web app

In this task, you create an Azure web app. Azure App Services is a Platform As a Service (PAAS) solution for web, mobile, and other web-based applications. Azure web apps is part Azure App Services hosting most runtime environments, such as PHP, Java, and .NET. The app service plan that you select determines the web app compute, storage, and features. 

1. Sign in to the **Azure portal** - `https://portal.azure.com`.

1. Search for and select `App services`.

1. Select **+ Create**, from drop-down menu, **Web App**. Notice the other choices. 

1. On the **Basics** tab of the **Create Web App** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- | ---|
    | Subscription | your Azure subscription |
    | Resource group | `az104-rg9` (If necessary, select **Create new**) |
    | Web app name | any globally unique name |
    | Publish | **Code** |
    | Runtime stack | **PHP 8.2** |
    | Operating system | **Linux** |
    | Region | **East US** |
    | Pricing plans | accept the defaults |
    | Zone redundancy | accept the defaults |

<img width="677" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/f718f66c-13eb-46fe-9abe-5f37a67fb8c2">


 1. Click **Review + create**, and then **Create**.

<img width="538" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/309d782f-9aa3-44a0-ae62-77a9147ddea4">


    >**Note**: Wait until the Web App is created before you proceed to the next task. This should take about a minute.

1. After the deployment, select **Go to resource**.

<img width="604" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/690cdd8c-0fde-4b36-accb-f7586bae688d">


## Task 2: Create and configure a deployment slot

In this task, you will create a staging deployment slot. Deployment slots enable you to perform testing prior to making your app available to the public (or your end users). After you have performed testing, you can swap the slot from development or staging to production. Many organizations use slots to perform pre-production testing. Additionally, many organizations run multiple slots for every application (for example, development, QA, test, and production).

1. On the blade of the newly deployed Web App, click the **Default domain** link to display the default web page in a new browser tab.

<img width="806" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/4af64714-0293-4979-9343-f53a840c3ae0">

<img width="739" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/5dc6f33f-0eda-4e14-8446-1065c4beca49">


1. Close the new browser tab and, back in the Azure portal, in the **Deployment** section of the Web App blade, click **Deployment slots**.

<img width="670" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/6e32bf23-0105-4f8b-8770-f0f5ef03bd0b">


    >**Note**: The Web App, at this point, has a single deployment slot labeled **PRODUCTION**.

1. Click **Add slot**, and add a new slot with the following settings:

    | Setting | Value |
    | --- | ---|
    | Name | `staging` |
    | Clone settings from | **Do not clone settings**|

<img width="860" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/fcc1374b-d3aa-41e5-9300-4153fe221910">


1. Select **Add**.

1. Back on the **Deployment slots** blade of the Web App, click the entry representing the newly created staging slot.

    >**Note**: This will open the blade displaying the properties of the staging slot.

1. Review the staging slot blade and note that its URL differs from the one assigned to the production slot.

## Task 3: Configure Web App deployment settings

In this task, you will configure Web App deployment settings. Deployment settings allow for continuous deployment. This ensures that the app service has the latest version of the application.

1. In the staging slot, select **Deployment Center** and then select **Settings**.

    >**Note:** Make sure you are on the staging slot blade (instead than the production slot).
    
1. In the **Source** drop-down list, select **External Git**. Notice the other choices. 

1. In the repository field, enter `https://github.com/Azure-Samples/php-docs-hello-world`

1. In the branch field, enter `master`.

1. Select **Save**.

<img width="810" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/f88e229a-abff-4108-8ed9-458000516716">


1. From the staging slot, select **Overview**.

1. Select the **Default domain** link, and open the URL in a new tab. 

1. Verify that the staging slot displays **Hello World**.

<img width="621" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/b3acc0b8-c356-4437-bf51-8d86b7089367">

>**Note:** The deployment may take a minute. Be sure to **Refresh** the application page.

## Task 4: Swap deployment slots

In this task, you will swap the staging slot with the production slot. Swapping a slot allows you to use the code that you have tested in your staging slot, and move it to production. The Azure portal will also prompt you if you need to move other application settings that you have customized for the slot. Swapping slots is a common task for application teams and application support teams, especially those deploying routine app updates and bug fixes.

1. Navigate back to the **Deployment slots** blade, and then select **Swap**.

1. Review the default settings and click **Swap**.

<img width="773" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/e7a0a3b0-7bee-4f97-a6c4-f0af62bb4cf3">

<img width="917" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/9a60f59e-db9b-4906-989f-2b480b8c5765">


1. On the **Overview** blade of the Web App select the **Default domain** link to display the website home page.

1. Verify the production web page displays the **Hello World!** page.

<img width="780" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/32859944-d3d5-48c3-ab51-dc68ea13b2d8">


    >**Note:** Copy the Default domain **URL** you will need it for load testing in the next task. 

## Task 5: Configure and test autoscaling of the Azure Web App

In this task, you will configure autoscaling of Azure Web App. Autoscaling enables you to maintain optimal performance for your web app when traffic to the web app increases. To determine when the app should scale you can monitor metrics like CPU usage, memory, or bandwidth.

1. In the **Settings** section, select **Scale out (App Service plan)**.

<img width="713" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/018935bf-a862-4eb7-b376-dbcaef680c21">


    >**Note:** Ensure you are working on the production slot not the staging slot.  

1. From the **Scaling** section, select **Automatic**. Notice the **Rules Based** option. Rules based scaling can be configured for different app metrics. 

1. In the **Maximum burst** field, select **2**.

<img width="797" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/4d6faf13-ef29-4de3-9951-77567cfe4652">


1. Select **Save**.

1. Select **Diagnose and solve problems** (left pane).

1. In the **Load Test your App** box, select **Create Load Test**.
<img width="832" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/9de659da-cf32-4f6c-901f-98d599089a7a">

    + Select **+ Create** and give your load test a **name**.  The name must be unique.
    + Select **Review + create** and then **Create**.
<img width="642" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/0155603e-0a5a-48f7-bbdc-dd645378f337">

1. Wait for the load test to create, and then select **Go to resource**.

1. From the **Overview** | **Add HTTP requests**, select **Create**.

<img width="892" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/0f66f0eb-0ad8-467d-9c56-e5d751ed071c">


1. For the **Test URL**, paste in your **Default domain** URL. Ensure this is properly formatted and begins with **https://**.

1. Select **Review + create** and **Create**.
<img width="601" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/02c2b383-cc38-42e5-b292-d46dad0aec33">

    >**Note:** It may take a couple of minutes to create the test. 

1. Review the test results including **Virtual users**, **Response time**, and **Requests/sec**.
<img width="872" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/53135957-25f4-4401-9ff1-f7bb96b90ec8">
<img width="614" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/2b115489-0b59-4671-8425-ec11c219890d">

1. Select **Stop** to complete the test run.

## Cleanup your resources

If you are working with **your own subscription** take a minute to delete the lab resources. This will ensure resources are freed up and cost is minimized. The easiest way to delete the lab resources is to delete the lab resource group. 

+ In the Azure portal, select the resource group, select **Delete the resource group**, **Enter resource group name**, and then click **Delete**.
+ Using Azure PowerShell, `Remove-AzResourceGroup -Name resourceGroupName`.
+ Using the CLI, `az group delete --name resourceGroupName`.
<img width="704" alt="image" src="https://github.com/Arinze008/-Implement-Web-Apps-in-Azure/assets/139396868/29b6619f-a351-44ca-a8cc-9e9b45c87ccc">

## Extend your learning with Copilot
Copilot can assist you in learning how to use the Azure scripting tools. Copilot can also assist in areas not covered in the lab or where you need more information. Open an Edge browser and choose Copilot (top right) or navigate to *copilot.microsoft.com*. Take a few minutes to try these prompts.

+ Summarize the steps to create and configure an Azure web app.
+ What are ways I can scale an Azure Web App?.

## Key takeaways

Congratulations on completing the lab. Here are the main takeaways for this lab. 

+ Azure App Services lets you quickly build, deploy, and scale web apps.
+ App Service includes support for many developer environments including ASP.NET, Java, PHP, and Python.
+ Deployment slots allow you to create separate environments for deploying and testing your web app.
+ You can manually or automatically scale a web app to handle additional demand.
+ A wide variety of diagnostics and testing tools are available. 
