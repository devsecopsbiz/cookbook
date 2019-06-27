[![Build Status](https://dev.azure.com/MSREADY19Sandbox/devsecopsbiz-session/_apis/build/status/GitHub_LabMDBuild?branchName=master)](https://dev.azure.com/MSREADY19Sandbox/devsecopsbiz-session/_build/latest?definitionId=12&branchName=master)

# Microsoft Ready, July 2019
## R-AIST307-P1: Dev*Ops: Hands on DevSecOps and DevOpsBiz cookbook 

**Welcome to Dev*Ops: Hands on DevSecOps and DevOpsBiz cookbook!**

DevOps has been propagating throughout the world as the place to be in order to be Agile and successful. 
As maturity sets in, new challenges start to come up, namely the security role and the integration with the business teams. 
As such, buzz words like _DevSecOps_ and even _DevSecOpsBiz_ are becoming more popular in discussions. 

This lab session builds on top of _R-AIST216 Dev*Ops: Digging into the trends of DevSecOps and DevOpsBiz_, allowing you to experience first hand the construction of a real world scenario.

## Lab steps
* Start by setting up an [Azure DevOps Organization](#AzDevOpsOrg)
* Then, [create an Azure DevOps Project](#AzDevOps) for us to work in
* Now let's [setup the build and release for the application](#CICD)
* Next, we'll want to [include Security into the pipeline](#Security)
* To wrap up, let's [gather Business information](#Business)
* And share it with a broader team and stakeholders using [Power BI](#PBI) and [Microsoft Teams](#Teams) 


<a name="AzDevOpsOrg"></a>
# Lab: Create Azure DevOps Organization 

The first step is to create a brand new *Azure DevOps* Organization.
Start by opening your favorite browser and navigate to:

```
https://dev.azure.com
```

Press **Start free**.

![](img/AzDevOpsOrgStart.png)

And sign in with the supplied credentials for the lab.

![](img/AzDevOpsOrgSignIn.png)

And then press `Continue`.

![](img/AzDevOpsOrgContinue.png)

You will end up with an empty Azure DevOps Organization. 
It's not necessary to create any *Project* at this time, you can proceed to next step.

![](img/EmptyDevOpsOrg.png)


*********

<a name="AzDevOps"></a>
# Lab: Create Azure DevOps Project 

This lab will guide you through the initial setup of an Azure DevOps Project, providing a quicker, prebuilt setup.

The first required step is to clone the public GitHub repository where the Lab is hosted.
This will allow you to have access to several pre-prepared assets, necessary for the different Lab modules we'll be implementing.

On the lab windows, press the *Windows* start menu and search for *x64_x86 Cross Tools Prompt for VS 2017*, launching it in *Administrator mode*.

![](img/CommandLine.png)

Navigate to the root folder, by typing `cd\` and pressing *enter*. Then execute the following command:

```
git clone https://github.com/devsecopsbiz/technical-lab.git
```

And you will get all the content on the *C:\technical-lab* folder, as shown in the image:

![](img/CloneRepo.png)

## Setup Azure DevOps Project

>  Use Azure DevOps Labs to create a preconfigured project and enrich it for a quick start.

* Start by creating a new Project using a preselected Lab.
For that, on your browser navigate to the following URL:

    ```
    https://azuredevopsdemogenerator.azurewebsites.net/?name=WhiteSource-Bolt&templateid=77362
    ```

    1. Navigate to the Azure DevOps Demo Generator and *Sign In* with the credentials you've used to create the Azure DevOps Organization, and then press the **Accept** button to proceed.
    
        ![Azure DevOps Lab Sign In](img/AzureDevOpsLab-SignIn.png)

    2. Select your Organization from the dropdown, fill in the *Project Name* with a name of your choice.
    
        Check the check-box allowing *WhiteSource Bolt* to be installed and then press *Create Project*:

        ![](img/AzureDevOpsLab-CreateProject-01.png)
    
    3. Wait for a few seconds for the project to create and then *Navigate* to it:

        ![](img/AzureDevOpsLab-CreateProject-02.png)

* Install additional extensions from the Marketplace:

    1. Navigate to `https://marketplace.visualstudio.com/items?itemName=keesschollaart.arm-outputs`, selecting the *Get it free* button.

        ![](img/ARMOutputs-navigate.png)

    2. Now, select the recently created Azure DevOps Organization on the dropdown, and press *Install*.

        ![](img/ARMOutputs-install.png)

    3. After a few seconds you should see a success message. Now, select the *Proceed to organization*.

        ![](img/ARMOutputs-success.png) 

    4. Navigate to `https://marketplace.visualstudio.com/items?itemName=keesschollaart.AzureCostInsights`, selecting the *Get it free* button.

        ![](img/AzureCostInsightsMarketplace.png)

    5. As for the previous extension, select the recently created Azure DevOps Organization on the dropdown, and press *Install*.

    6. After a few seconds you should see a success message. Select the *Proceed to organization*.

    7. Now, select the project you've just created, by pressing its name.


* Create a free account for *WhiteSource Bolt* 

    1. Navigate to *WhiteSource Bolt* under *Pipelines -> WhiteSource Bolt*.

    2. Fill in your details to create a free account.

        ![](img/WhiteSourceBolt-freeaccount.png)

    3. After a few seconds, we're good to go!

        ![](img/WhiteSourceBolt-success.png)

* Import additional Git repositories, required for the labs:

    1. Navigate to *Repos* and on the upper repositories drop down, select *Import repository*:

        ![](img/AzureDevOpsLab-ImportRepo.png)

    2. Fill in the *Clone URL* with `https://github.com/devsecopsbiz/SmartHotel360-Website`
    and press *Import*:

        ![](img/AzureDevOpsLab-ImportRepo-CloneURL.png)

        Wait for a couple of seconds for it to finish.

    3. Select *Import repository* again, now filling with     `https://github.com/Deliveron/owasp-zap-vsts-extension.git`
    and press *Import*.

        TROCAR POR UM REPOSITÓRIO NOSSO POR CAUSA DOS TESTES E OUTRAS SITUAÇÕES QUE POSSAM ACONTECER

        ![](FALTA)

    4. You should now see the complete list of repositories available has shown in the following image:

        ![](FALTA)


## Next step:  
[Setup the build and release for the application](#CICD)

*********

<a name="CICD"></a>
# Lab: Azure DevOps CI/CD

This lab will guide you through building Continuous Integration (CI) and Continuous Deployment (CD) pipelines with Azure DevOps. The build pipeline will make use of a Java application, built with Maven, but also a .NET Core and Azure Functions App.
For the release pipeline we'll be leveraging ARM templates and Azure App Services to host our application.

## Create Build Pipeline

* Navigate to *Pipelines*, *Builds*.

    ![](img/AzureDevOpsLab-Builds-01.png)

    ### WhiteSource Bolt Build
    1. Here you should see an existing build definition name *WhiteSourceBolt*.
    Under *New*, select *Import a pipeline* to import a precooked pipeline to build the recently imported SmartHotel repository:

        ![](img/AzureDevOpsLab-Builds-02.png)
        
    2. Drag and drop the `SmartHotel_Petchecker-Web.json` file, located on the Lab repository under *~/files/SmartHotel/*, or Browse for the same file. Then, press *Import* to start the import process:

        ![](img/AzureDevOpsLab-Builds-03.png)

        ```
        Change the Name, removing the "-import" portion of it.
        The final name should be "SmartHotel_Petchecker-Web", as shown in the image:
        ``` 

        ![](img/AzureDevOpsLab-Builds-031.png)
    
    3. Select the **Hosted VS2017** Agent pool:

        ![](img/AzureDevOpsLab-Builds-04.png)
  
    4. Now select the *Source Repository* `SmartHotel360-Website`, by pressing *Get sources*, *Azure Repos Git* and selecting the correct repository on the *Repository* dropdown:

        ![](img/AzureDevOpsLab-Builds-05.png)

    5. To finish, enable the *Continuous integration* trigger by navigating to *Triggers* and selecting *Enable continuous integration*:

        ![](img/AzureDevOpsLab-Builds-trigger.png)

        Save by pressing the **Save** button, confirming the save on the popup (no neeed to change anything on the *Select folder* or add a Comment):

        ![](img/Save.png)

    ### OWASP Build
    
    Now we'll be using an alternative way to setup our CI build, leveraging a YAML file.

    Navigate to the *owasp-zap-vsts-extension* repository, and drag and drop the **azure-pipelines.yml** file, located on the Lab contents you've downloaded, under *~/files/OWASP*, into the repository.
    Click on the **Commit** button to confirm.

    You should end up with the following contents:

    ![](img/OWASP-pipeline.png)

    This will generate an additional build pipeline, now available together with the remaining ones.
    Navigate back to *Pipelines*, *Builds* to double check:

    ![](img/OWASP-build.png)


## Create Release Pipeline

* Under *Pipelines*, navigate to *Releases* and press **New pipeline**

    ![](img/AzureDevOpsLab-Releases-01.png)

    1. We first need to create a dummy, empty, Release pipeline in order for the *Import* to become available. 
    Let's do this by pressing *New pipeline*, *Empty job* and **Save**:

        ![](img/AzureDevOpsLab-Releases-02.png)

        ![](img/AzureDevOpsLab-Releases-04.png)

    2. Navigate back to *All pipelines* and select **Import release pipeline**:

        ![](img/AzureDevOpsLab-Releases-05.png)

    3. Drag and drop, or navigate as before, to select the **SmartHotel360_Website-Deploy.json** file:

        ![](img/AzureDevOpsLab-Releases-06.png)

    4. Press *OK* to start the import process. You should now have a release pipeline like this:

        ![](img/AzureDevOpsLab-Releases-07.png)

    5. Navigate to the Stage tasks:

        ![](img/AzureDevOpsLab-Releases-08.png)

    6. Select the *Agent job*, and set the *Agent pool* to **Hosted**

        ![](img/ReleasePipeline_SetAgentPool.png)

    7. Select the first task and, under *Azure Subscription*, select the **Manage** button.
    It will redirect you to a page were we'll be configuring access to the Resource Group from our Azure Subscription.

        ![](img/AzureDevOpsLab-Releases-09.png)

        Under `New service connection`, select `Azure Resource Manager`:

        ![](img/ServiceConnections.png)

        Select the available *resource group* from the dropdown, give the service connection a name and press OK.

        > Important: Save the Resource Group name for later use (copy to notepad for example).

        ![](img/ServiceConnectionConfig.png)

        You should then see a new Service connection appear:

        ![](img/ServiceConnectionFinish.png)

 
    8. Going back to the *release pipeline* (should be on a previous tab on the browser), the dropdown should now show you the brand new *Service connection*.

        Select it.
        > If it hasn't loaded, press the refresh button on the right and then open the dropdown again.

        ![](img/AzureSubscriptionAvailable.png)


        Step in each one of the tasks with error, selecting and authorizing an Azure Subscription to use in the lab. 

        > For the *ARM Outputs* task in particular, it's also required to specify the *Azure Connection Type* as **Azure Resource Manager**

    9. Navigate to *Variables* and update the values.

        **location:** West US

        **ResourceGroup:** <paste the resource group we've saved earlier: e.g. ResourceGroupXXXXX>

        ![](img/VariablesUpdate.png)

    10. Remove the existing *Artifact* by navigating back to the *Pipeline* tab, selecting the Artifact, and pressing *Delete*.

        ![](img/RemoveArtifact.png)

    11. Now, add the **SmartHotel_Petchecker-Web** build artifact. This will make sure we're using the artifact coming from the build we've created before.

        > Important: set the *Source alias* to `SmartHotel Petchecker Web`

        ![](img/AddArtifact.png)

    12. To finish, enable the Continuous Deployment trigger

        ![](img/AzureDevOpsLab-Releases-trigger.png)

    13. Press the **Save** button, confirming with the **OK** button.
    > Important: Set the release pipeline name to **SmartHotel360_Website-Deploy**


#### Run a test build

1. In Azure DevOps, click on Builds, navigate to **Folders** and, for each build, select it and press the "Queue" button on the right upper corner.

    ![](img/AzureDevOpsLab-Builds-Run-01.png)

2. Monitor the build logs, by double clicking the running build, and wait for it to complete

   ![](img/AzureDevOpsLab-Builds-Run-end.png)

3. The release will be triggered automatically when the build is complete (be patient, this can take some time). Review the results as it completes. 

   ![](img/AzureDevOpsLab-Releases-Run-executing.png)

4. Navigate to the release logs and check the details regarding the last step, **Echo Website Name**.

   ![](img/AzureDevOpsLab-Releases-CheckOutput-deploytask.png)

    Here you should see the website URL. Press <Ctrl> and click on the URL to navigate to it.

    ![](img/AzureDevOpsLab-Releases-CheckOutput-1.png)

    The website we've just deployed looks like :

    ![](img/AzureDevOpsLab-Releases-CheckOutput-site.png)


7. Now kick-off the full CI/CD pipeline by making an edit to the  code in the Azure DevOps code repository.
Navigate back to *Repos*, *SmartHotel360-Website* repository, select **appsettings.Development.json** and press *Edit*

    ![](img/AzureDevOpsLab-Repo-edit.png)

8. Change the *Name* property value to something you want, and *Commit* the change after it

    ![Repository change to trigger CI CD](img/AzureDevOpsLab-Repo-commit.png)


## Next step:  
[Include Security into the pipeline](#Security)

*********

<a name="Security"></a>
# Lab: Security

This lab will guide you through adding some Security validations into our pipelines, detecting and fixing security vulnerabilities, but also problematic open source licenses.

## Review WhiteSource Bolt task configurations on Build

*WhiteSource Bolt for Azure DevOps* is a free extension, which scans all your projects and detects open source components, their license and known vulnerabilities.

It covers over 200 programming languages support and continuous tracking of multiple open source vulnerabilities databases like the NVD, security advisories, peer-reviewed vulnerability databases, and popular open source projects issue trackers.

### Let's start adding it to our pipelines

1. In Azure DevOps, click on "Pipelines" on the left menu and then click "Builds"

2. Select the *SmartHotel_Petchecker-Web* and *WhiteSourceBolt* build pipelines, clicking the "Edit" button for each, and select the **WhiteSource Bolt** task. Review it.

    ![](img/AzureDevOpsLab-Builds-WhiteSourceBolt.png)

3. Now navigate to *Pipelines*, *WhiteSource Bolt* on the left and explore the generated reports

    ![](img/AzureDevOpsLab-Builds-WhiteSourceBolt-report.png)


## Add OWASP ZAP penetration testing tool to the Release pipeline

OWASP is a worldwide not-for-profit organization dedicated to helping improve the quality of software. ZAP is a free penetration testing tool for beginners to professionals. ZAP includes an API and a weekly docker container image that can be integrated into your deployment process

### Let's start adding it to our pipelines

1. Start by setting up a Docker host for later use:

    ## Deploy a template with the Azure Docker VM extension
    Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.

    You need to login onto the Azure Portal (`https://portal.azure.com`), and access the Cloud Shell, setting it up to *Bash*.

    ![](img/AzureCloudShell.png)

    Since we're using brand new Subscriptions, we need to create a storage to support Cloud Shell.

    Press **Show advanced settings** and fill in **Storage account** and **File share** before hitting the **Create storage** button.
    
    ![](img/CloudShellStorage.png)

    ![](img/CloudShellStorageAdvanced.png)

    After a few seconds you should see something like:

    ![](img/AzureCloudShellBash-ready.png)

    Cloud Shell already provides us the latest Azure CLI, allowing us to execute the following commands.

    First, grab the resource group name (*name* property) already created for the lab. Paste it on notepad for example.

    ```azurecli
    az group list
    ```

    ![](img/RGName.png)

    Next, deploy a VM with that includes the Azure Docker VM extension from an Azure Resource Manager template from GitHub. 

    On the bash cloud shell, run the following command providing, when prompted, your own unique values for *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*.

    > Replace the name of the resource group with the one you got previously.     
    > And *dnsNameForPublicIP* will be your public VM name and must be unique.

    Command to execute:

    ```azurecli
    az group deployment create --resource-group <REPLACE HERE> --template-uri https://raw.githubusercontent.com/devsecopsbiz/azure-quickstart-templates/f99d00825b32577a5321f4e91ca07e0f914c3aa6/docker-simple-on-ubuntu/azuredeploy.json
    ```

    
    It takes a few minutes for the deployment to finish.


    ## Deploy your first NGINX container
    To view details of your VM, including the DNS name, use *az vm show*:

    > Replace the name of the resource group with the one you got previously

    ```azurecli
    az vm show --resource-group <REPLACE HERE> --name myDockerVM --show-details --query [fqdns] --output tsv
    ```

    SSH to your new Docker host. **Provide your own** username and DNS name from the preceding steps:

    ```
    ssh <azureuser>@<mypublicdns.eastus.cloudapp.azure.com>
    ```

    Once logged in to the Docker host, let's run an NGINX container:

    ```
    sudo docker run -d -p 80:80 nginx
    ```

    The output is similar to the following example as the NGINX image is downloaded and a container started:

    ```
    Unable to find image 'nginx:latest' locally
    latest: Pulling from library/nginx
    efd26ecc9548: Pull complete
    a3ed95caeb02: Pull complete
    a48df1751a97: Pull complete
    8ddc2d7beb91: Pull complete
    Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
    Status: Downloaded newer image for nginx:latest
    b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
    ```

    Check the status of the containers running on your Docker host as follows:

    ```
    sudo docker ps
    ```

    The output is similar to the following example, showing that the NGINX container is running and TCP ports 80 and 443 and being forwarded:

    ```
    CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
    b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
    ```

    To see your container in action, open up a web browser and enter the DNS name of your Docker host:

    ![](img/nginx.png)


2. Before proceeding any further, let's run a OWASP ZED Attack Proxy against our published website.

    > Note: Replace the website URI with the one you've deployed earlier. e.g. *https://smarthotel360lcu4bmxi7kl4w.azurewebsites.net* 

    ```
    docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-weekly zap-baseline.py -t <REPLACE HERE> -g gen.conf -r testreport.html
    ```
    Docker image will be pulled and the container will be then executed.

    ![](img/OWASP-docker-pull.png)

    When if finishes you should see a summary like this

    ![](img/OWASP-finish.png)

    
3. Navigate back to your Azure DevOps Project and let's grab a personal access token (PAT) we'll be needing later on.
    > Save that PAT token, it can't be retrieved later

    3.1 Navigate to the user profile and select *Security*

    ![](img/PAT-token-security.png)

    3.2 Select *Personal access token*

    ![](img/PAT-token-navigate.png)

    3.3 Create a new personal access token

    ![](img/PAT-token-create.png)

    3.4 Copy the token, making sure you don't lose it.

    ![](img/PAT-token.png)

4. On your Azure DevOps project, navigate to *Pipelines*, *Releases* *SmartHotel360_Website-Deploy*, and press the **Edit** button.

    Then, under *Variables*, add a new variable setting:

    **Name:** PAT

    **Value:** <copied PAT token>

    **Secret:** press the locker button, making it a secret, hiding the contents

    You should get the following configuration:

    ![](img/PAT-token-variable.png)

    Save the release pipeline.


4. Let's get back to the Release pipeline and add some extra tasks to launch the ZAP test and grab the results.
Start by adding two **SSH** tasks, one for running the tests and another for publishing the test report to a public website. 

    Under `Pipeline`, add a new Artifact, from the *owasp-zap-vsts-extension* build, as shown in the following image:

    ![](img/Artifact-owasp-zap-vsts-extension.png)

    > Important: make sure your *Source alias* for this artifact is **_owasp-zap-vsts-extension**

    Now, *view stage tasks*: 

    ![](img/Add-OWASP-tasks-navigate.png)

    4.1. Before going further we need to configure the SSH service connection to the provisioned Docker machine.
    Press the *Manage* button, *New service connection*, *SSH*, and fill in the following details, replacing *Host name*, *User name* and *Password* with your own details, specified on the previous steps of this lab.

    ![](img/SSH-service-connection.png)

    Press *OK* and go back to the previous tab, on the release pipeline. Refresh the *SSH service connection* drop down and select the fresh new connection. 

    4.2. For the first `SSH` task, we need to specify the command to run and check the `Continue on error` option. This is required due to possible failing tests, that we don't want to prevent the deployment to proceed.

    ![](img/SSH-ZAP-test.png)

    > Tip: Rename `Display name` to make it clearer to understand what is going on here.

    Change the URI with the value of your own website, published on the previous Labs, and copy the updated command:

    ```
    docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-weekly zap-baseline.py -t $(SmartHotelWebsiteURL) -g gen.conf -r $(Release.DefinitionName)_$(Release.ReleaseName)_OwaspZapReport.html
    ```

    4.3. On the second `SSH` task insert the following command:

    ```
    docker stop $(docker ps -a -q)
    docker run -v $(pwd):/usr/share/nginx/html -d -p 80:80 nginx
    ```

    This will copy the generated test report to the NGINX container, making it publicly available.
    Rename the *Display name* as suggested before, making it clearer to understand in the future.

    4.4. Next we'll be adding a *Powershell* task to download the generated test report and pass into the release pipeline.

    Add the following command to download the file, changing the *URI* on both commands.

    ```
    Invoke-WebRequest -Uri "http://<msreadydockervm>.<eastus>.cloudapp.azure.com/$(Release.DefinitionName)_$(Release.ReleaseName)_OwaspZapReport.html" -OutFile "$(System.DefaultWorkingDirectory)\OwaspZapReport.html"
    ```

    ![](img/Powershell-Download.png)
   
   4.5. To finish, add a *Command Line* task, were we'll be executing the **owasp-zap-vsts-tool.exe** to attach the report into Azure DevOps.

    ![](img/Add-OWASP-tasks-search.png)

5. Paste this command on the *Script* text box as seen in the image, adapting the URI on the Echo command. 

    ```
    $(System.DefaultWorkingDirectory)/_owasp-zap-vsts-extension/drop/owasp-zap-vsts-tool/bin/Release/owasp-zap-vsts-tool.exe attachreport collectionUri="$(System.TeamFoundationCollectionUri)" teamProjectName="$(System.TeamProject)" releaseUri=$(Release.ReleaseUri) releaseEnvironmentUri=$(Release.EnvironmentUri) filepath=$(System.DefaultWorkingDirectory)\OwaspZapReport.html personalAccessToken=$(PAT)

    echo "http://<msreadydockervm>.<eastus>.cloudapp.azure.com/$(Release.DefinitionName)_$(Release.ReleaseName)_OwaspZapReport.html"
    ```

    ![](img/OWASP-Attach-Report.png)

6. To finish the Security Lab, run the release pipeline and, when it has finished, navigate to your website made available using NGINX.
You can check the URI by navigating to the *Attach Report* task log:

    ![](img/OWASP-Attach-Report-Navigate.png)

    You should see something like:

    ![](img/NGINX-ZAP-Report.png) 


## Next step:  
[Gather Business information](#Business)

*********

<a name="Business"></a>
# Lab: Azure DevOps Business

This workshop will guide you through the process of creating and configuring a set of specialized dashboards, each with a different scope that can be used by distinct team members and stakeholders. 

## Azure Cost Insights

It's easy to get your Azure Costs out of control. _Wouldn't it be great to get insights of your infrastructure spending in your daily routine?_

Costs are a concern of everyone, developers, product owners and operations.
They come together in Azure DevOps, so why not show these insights there?

*Azure Cost Insights* is a widget that you can add on your Azure DevOps Dashboard.

This widget is built with the belief that cost insights need to be scoped to your costs. 


### Getting started

You need to create an Azure Pipeline for the widget to work. This pipeline is going to download and host your cost-data, used by the widget.

![](img/flow.png)
 
1. **Create the build pipeline**<br/>

    Navigate to *Pipelines*, *Builds* and *Import a pipeline*.

    ![](img/CostInsights-Import-Build.png)

    Drag and drop the **Cost Insights.json** file, located on the Lab repository under *~/files/Business/*, or Browse for the same file. Then, press *Import* to start the import process:

    ![](img/CostInsights-Import.png)

    After importing, configure the missing settings as following:

    ![](img/CostInsights-configuration.png)

    **Pipeline** -> **Agent pool**: Hosted VS2017

    **Get sources** -> **Repository**: SmartHotel360-Website
    
    **Download cost data** -> **Azure RM Subscription**: `Azure subscription being used in the lab`

    When you're finished, your  pipeline will look like this:

    ![](img/CostInsights-Import-finish.png)

2. **Queue the build** and wait for it to finish<br/>

    ![](img/CostInsights-run.png)

3. **Add the Widget to your Dashboard**<br/>
    - Go to your teams' dashboard and add a 'Azure Cost Insights' widget.

        Navigate back to *Overview*, *Dashboards* and press the **Add a widget** button.

        ![](img/Dashboard-AddWidget.png)

        Then, search for the **Azure Cost Insights** widget and press the **Add** button.

        ![](img/Dashboard-SearchWidget.png)

        Configure it by selecting the build we've just created, grouping by *Resource Type* as shown in the image:

        ![](img/CostInsights-resourcetype.png) 

        Now add another 'Azure Cost Insights' and configure it as shown below:

        ![](img/CostInsights-subscription.png)
     
## Examples

![](img/screen2.png)

*********

<a name="PBI"></a>
# (Optional) Lab: Connect Azure DevOps to Power BI

In this lab, we'll show you how to create a custom Analytics view for active bugs and then generate a Power BI report based on that view. You'll learn how to filter the Analytics view, create a trend chart, as well as a card showing the current count of approved bugs. 

 Using Power BI connected to Analytics views, you can create reports on your work items. Reports can show your current work data and also historical revisions of the work items.  

Follow these steps to create a report in Power BI desktop that shows a **daily active trend of  bugs** based on a custom **Analytics view**:

1. From the web portal for Azure DevOps:   
	a. Open **Analytics views**  
	b. Create a custom Analytics view for your data.   
2. From the Power BI Desktop:  
	a. Get the data set defined by the Analytics view   
	b. Create a trend report  
	c. Apply filters to your trend report  
	d. Create a card and apply the Is Current=True filter to show current count.  

<a id="prerequisites">  </a>
## Prerequisites  

In order to create a Power BI report that references an Analytics view, you must meet the following criteria:  

- Have installed *Power BI Desktop* *February 2018 Update* or later version. You can download this client application from the official [Power BI Desktop download page](https://powerbi.microsoft.com/desktop).
- Have tracked bugs for some period of time on which to generate a trend report. 


## Create a view to only include Approved bugs

![](img/open-analytics-views-vert.png)

From the web portal, **Analytics view**, choose **New View** to create a custom view. Fill out the forms provided in each tab as shown in the steps below. 

Choose **Continue** to move to the next tab in the panel. If you need to revisit a tab, simply click the tab title. 

### 1. Name your view and set to Private  

1. Give your view a name, such as *Approved bugs*. Select **Private view** to save it under **My Views**. Otherwise, you can select **Shared view** to save it under **Shared Views**.  

    ![](img/active-bugs-general.png)

Choose **Continue** to move to the next tab. 

2. From the **Work items** tab, select the Project and Team that contain the data you want to report on.  
 
    Here we choose the *MsReadyLab* project and the *MsReadyLab Team*.
    
    ![](img/active-bugs-team.png)

	To add additional projects or teams, click *Add row icon* to add a new row and then select the project and team. 
    

3. Under **Backlogs and work items**, add a new row, and then select **Bug** from the list of work items types.

    ![](img/wi-type-picker-bugs.png)

4. Under **Field criteria**, choose the **State** field set to **Active**.

    ![](img/active-bugs-field-criteria.png)
    
	Choose **Continue** to move to the next tab. 

5. In the next tab, **Fields**, we'll keep the most common fields selection. This selection will also include any custom fields that have been added to your project.  
    
    ![](img/fields-common.png)

	Choose **Continue** to move to the next tab. 

6. In the **History** tab, select **Rolling period in days** and enter **60** days. Keep the **Granularity** set to **Daily**. These selections will generate 60 snapshot rows of data for each approved bug. Each day will include all the details of that work item as it was at the end of that day. 
    
    ![](img/active-bugs-history.png)

	Choose **Continue** to move to the next tab. 

7. On the last tab, **Verification**, click **Verify view**. The system will verify your view by running a test query against the data set it defines and validate all your filter criteria. 

    ![](img/active-bugs-verify.png)
  
	> Verification time will vary based on the amount of data defined in your view. Verify your view to make sure all the definitions are correct.  

	Once your view successfully verifies, choose **Save**. You can then start using it in Power BI. Verification also returns an estimate of the number of rows in the dataset and the time it will take to load in Power BI.

    ![](img/active-bugs-verify-success.png)
	
	If your view fails to verify successfully, you'll get an error explaining the issue and pointing to a possible fix. Try changing the options you selected in the **Work Items** and **History** tabs to include less data, and then verify the view again. 

## Open Power BI desktop and load your view 

1. Open Power BI Desktop.  
 
2. Choose (1) **Get Data**, choose (2) **Online Services**, then (3) **Azure DevOps (Beta)**, and then click (4) **Connect**. 

    ![](img/get-data-2.png)
    
3. Enter your organization name, the same Azure DevOps name you used to create the Active Bugs view, and the same project for which you defined the Active Bugs view. 

    ![](img/specify-account.png) 

4. Expand the **Private Views** folder, choose the **Approved Bugs** view you saved in the previous section, and then click **Load**. 

    ![](img/choose-view.png)

## Create a daily bug trend report 

1. In your report, (1) select the Line chart visual, (2) enter `work item id` in the search field, and then (3) check the box for **Work Item Id**. 

    ![](img/select-line-chart-work-id.png)

	This will change your chart to a single dot.  
  
2.	Click the context menu icon next to the **Work Item Id** field and change it from **Count** to **Count (Distinct)**.

    ![](img/choose-count-distinct.png)

3. Next, (1) select the **Date** field in the fields list as your axis. To see a daily trend, (2) click the context menu icon next to the field and change it from **Date Hierarchy** to **Date**.

    ![](img/select-date.png)

   To view trends over time, you want to use **Date** and not **Date Hierarchy**. The **Date Hierarchy** in Power BI rolls ups everything into a simple number for the period. The day level in the hierarchy rolls all days to a number between 1-31. For example, April 3 and May 3 both roll up into number 3. This is not the same as counting items per actual date.

## Filter your trend by Priority

1. To group your bugs by `Priority`, search for the field in the list (a). Drag the Priority field into the `Legend` of your trend chart (b)
    
    ![](img/filter-priority-legend.png)

2. The chart now shows a daily distinct count of bugs, grouped by Priority.

3. To just show only Priority 0 and 1 bugs, click the context menu icon next to the **Priority** field to set the filters.  

    ![](img/filter-priority-1-and-2.png)   
   
	The trend chart is now grouped and filtered by high priority bugs.

## Create a card for latest bug count

1. Add a new page by clicking the plus sign (+) at the bottom of the page. 

2. Select the card visual, add the **Work Item Id** field, add the **Work Item Type** field, and click the context menu icon next to the field and change it from **Count** to **Count (Distinct)**.

	The card now shows the number of active bugs times the number of days they existed within the selected time period.  For this example, that number is 1066. 

    ![](img/card-active-bugs.png)   
    
3. To get the latest count, add **Is Current** as a page level filter, and select the True checkbox. The **Is Current** field is added automatically to all data sets, marking the rows that contain the latest revision of the work items.

    ![](img/iscurrent.png)   
   
	The value on this card should match the count on the last day of the trend chart, which you can obtain by returning to Page 1 and hovering over the last day as shown.  

    ![](img/check-of-is-current.png)

## Save your report, optionally share with others 

1. Choose **File > Save As** to save your report to your local workspace. 

2. To publish your report to Power BI, choose the **Publish** tab.

    ![](img/publish-powerbi.png)

## Continue to explore your data

Analytics views provide you with a great deal of power and flexibility to filter your data and generate useful reports quickly and easily using Power BI. Within a custom view, you can create data sets that span multiple teams or projects. 

*************

<a name="Teams"></a>
# (Optional) Lab: Connect Azure DevOps to Microsoft Teams

## Overview

**[Microsoft Teams](https://teams.microsoft.com/start)** is a hub for teamwork in Office 365. Keep all your team's chats, meetings, files, and apps together in one place. Software development teams get instant access to everything they need in a dedicated
hub for teamwork, that brings your teams, conversations, content and tools from across Office 365 and Azure DevOps together into one place.

## Prerequisites

1. You should have Office365 account in order to integrate **Azure DevOps Services** with **Microsoft Teams**.

1. Only Azure DevOps organizations in the same organization (AAD tenant) can be used to integrate with your Microsoft Teams account.

**You can start a free trial if you don't have Office365 account from [here](https://teams.microsoft.com/start)**

In this lab, you’ll learn about how **Azure DevOps** integrates with **Microsoft Teams** to provide a comprehensive chat and collaboration experience, across your Agile and development work.

## Getting started with Microsoft Teams

1. Launch **Microsoft Teams** - you can either open the web app or download the app to your desktop from [here](https://teams.microsoft.com/dl/launcher/launcher.html?url=/_%23/l/home/0/0&type=home)

   ![](img/launch_teams.png)

1. After launching the app, on the left side of **Teams**, click **Teams**, and then at the bottom of the teams list, click **Join or create a team**. A team is a collection of people who gather together around a common goal. 
    
    ![](img/create_team.png)

1. In the **Join or create team** window select **Create team**.
    
    ![](img/create_team2.png)

1. Give a name for your team and description if needed. Select the privacy settings and click on **Next**.

    ![](img/create_team3.png)

1. Add members for your team in order to get notified the events that occur and also start conversations with your team members.

   ![](img/add_members.png)

## Integrating Microsoft Teams with Azure DevOps Services

**Azure DevOps Services** integration with Microsoft Teams provides a comprehensive chat and collaborative experience across the development cycle. Teams can easily stay informed of important activities in your Azure DevOps team projects with notifications and alerts on work items, pull requests, code commits, build and release.

1. Select **Tailwind Traders** team that was created.  Click the ellipsis or **'...'** at the top nav of your team channel, and then select **Connectors**.
   
    ![](img/connectors.png)

1. Select **Azure DevOps** connector from the list and click **Add**.

   ![](img/azuredevops_connector.png)

1. Click **Install** to add the connector for your team.
   
    ![](img/install_connector.png)

1. Select your organization (you may be prompted to sign in first), the project, and your team. Choose the type of activity you want to be notified about. Depending on the event, you may be given further fields to filter down the notifications so you can filter out notifications your team does not care about. For example, for work item events, you can filter by area path, work item type, and even particular field changes.

   ![](img/connector_configuration.png)

   When you are happy with the configuration, **Save** it.

1. Since Azure DevOps is configured now, activity from your Azure DevOps Services project will start appearing in your Teams channel.
   
   ![](img/azuredevops_activity.png)

1. If you want to make a change to an existing connector, navigate to the **Configured** tab on the **Connector** dialog, find the connector, and click **Manage**. 

   ![](img/manage_connector.png)

## Azure DevOps Kanban board & Dashboards in Teams 

Your Kanban board turns your backlog into an interactive signboard, providing a visual flow of work. As work progresses from idea to completion, you update the items on the board. Each column represents a work stage, and each card represents a user story (blue cards) or a bug (red cards) at that stage of work.

You can bring in your teams kanban board or favourite dashboard directly into Microsoft Teams.
These can be added using Tabs. **Tabs** allow team members to access your service on a dedicated canvas, within a channel or in user's personal app space. You can leverage your existing web app to create a great tab experience within Teams.

1. To bring your Kanban board or Dashboard into Microsoft Teams, click the **+** icon to add new tab. Find the Azure DevOps icon and select **Azure DevOps**

   ![](img/add_kanbanboard.png)

   ![](img/azuredevops_tab.png)

 
1. Select the Organization

   ![](img/kanban_selectorg.png)

   ![](img/kanban_selectorg2.png)

   The Kanban board and Dashboard integration has the following limitations:

    1. Only works for Azure DevOps Services (Team Foundation Server is not supported)

    2. Only Kanban boards and Dashboards within organizations in the same organization (Azure Active Directory tenant) as your Microsoft Teams account can be configured." %}
 
1. Once you have authenticated and selected your organization, you will be displayed a screen to select a **Kanban board** or **Dashboard**. 


   ![](img/select_kanbanboard.png)

   Select the **Kanban board** and select your project, team, backlog level. **Save** the configuration.

1. Now you can see the **Kanban Board** appearing in the tab.

   ![](img/kanbanboard_teams.png)

1. All the work can be monitored during the daily standup's and the updates are real when the work items states are changed. It also allows us to customize the Kanban Board from within the Teams and synced.


## Collaboration Experience

Messages are a good way to connect and keep a history of the conversation. It's even better to use emoji, stickers, and GIFs to make a great impression.

1. Start having conversations with your team members by selecting the **Conversations** tab.

   ![](img/conversations.png)

1. All the conversations could be retrieved at any time without losing the history which helps the entire team to have a collaborative experience

1. Teams can have a collaborative experience with the latest updates with respect to the **work items, build summary** etc so that it helps in better transparency

1. **Easily find and discuss work items from DevOps in Teams** : You can easily search, find and discuss work items from Azure DevOps in Teams, keeping the conversation and collaboration within your Teams app. For example if you would like to discuss about any User Story you can click on **Azure DevOps** icon. It will prompt a window where you can search your project workitems. Select the work item to discuss and enter your comments.

      ![](img/workitems.png)
      ![](img/workitems2.png)
      
For more information about using the Conversation tab in Microsoft Teams click [here](https://support.office.com/en-us/article/using-the-conversation-tab-in-microsoft-teams-53d1c530-3797-4a6f-9892-6760f8763df2)

## Working with Channels

**Channels** are dedicated sections within a team to keep conversations organized by specific topics, projects, disciplines—-whatever works for your team!

- Team channels are places where everyone on the team can openly have conversations. Private chats are only visible to those people in the chat.

- Channels are most valuable when extended with apps that include tabs, connectors, and bots that increase their value to the members of the team.

To learn more about best practices for creating teams and channels view this short [video](https://youtu.be/hjJWtoaRJeE).
1. Select the **Team** that was created earlier and click on **ellipsis (...)**

   ![](img/add_channel.png)

1. Give a name and description for your channel and click on **Add**

   ![](img/create_channel.png)

1. Once the channel is created, the conversations can be started among the team members.

   ![](img/channel_added.png)

## Sharing the Contents

As your team works together you'll undoubtedly have files that you'll want to share and collaborate on. Microsoft Teams makes it easy to share files within channels. If the files are Word, Excel. PowerPoint or Visio files your colleagues can even view, edit, and collaborate on the files right within Teams. For Word, Excel, and PowerPoint, they can see each others changes in almost real time.

1. Select **Files** and select **Upload** to share a document with the team. You can also use **Drag and drop** (Using your mouse, drag the file from where it's currently located and drop it on the Teams window among the files.) method to upload files.

   ![](img/upload_files.png)

1. Click on the document that was uploaded from the list to start editing and having a live conversation with your team members

   ![](img/conversation_files.png)

1. You can also share the related websites within the Teams as Tabs. As we use **Wiki** to explain project objectives, epics, specs, release notes, best practices or other content to ensure all your team members and stakeholders learn, you can also share your Team's **[Wiki](https://azure.microsoft.com/en-in/services/devops/wiki/)** content as website within teams as tab. 

1. Navigate to your Azure DevOps projects Wiki page. Copy the URL.
       
    ![](img/wikipage.png)

1. Now switch back to the **Teams**. Click on **+** and select **Website**

   ![](img/add_tab.png)

   ![](img/add_website.png)

1. Provide a name for the website, enter the wiki URL copied in previous step and click on **Save**. It appears on the channel where all of the team members can access to get quick information if there were any updates done

    ![](img/wikiasweb.png)

1. This is how the website/Wiki looks when added to the channel.

   ![](img/wikiasweb2.png)

Now that you have connected Microsoft Teams and Azure DevOps think about the other development team information that you can expose via Microsoft teams, for example: 

- [Add a OneNote notebook to Teams](https://support.office.com/en-us/article/Add-a-OneNote-notebook-to-Teams-0ec78cc3-ba3b-4279-a88e-aa40af9865c2) to keep meeting notes such as **Sprint Planning Meetings** and **Retrospective Meetings**. 
     
    ![](img/onenote.png)

- [Connect Azure DevOps to Power BI ](https://docs.microsoft.com/en-us/azure/devops/report/powerbi/?view=azure-devops) and [add a Power BI tab ](https://support.office.com/en-us/article/add-a-powerbi-tab-to-teams-708ce6fe-0318-40fa-80f5-e9174f841918) that displays advanced reports from Azure DevOps or other data related to your project.

   ![](img/powerbi.png)

