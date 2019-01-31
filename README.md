[![Build Status](https://dev.azure.com/MSREADY19Sandbox/devsecopsbiz-session/_apis/build/status/technical-lab?branchName=master)](https://dev.azure.com/MSREADY19Sandbox/devsecopsbiz-session/_build/latest?definitionId=4&branchName=master)

# Microsoft Ready, Feb 2019
## AI-APP-ST300: Hands on Dev*Ops (Dev-Sec-Ops-Biz) 

**Welcome to Technical Lab for the AI-APP-ST300: Hands on Dev*Ops session!**

DevOps has been propagating throughout the world as the place to be in order to be Agile and successful. 
As maturity sets in, new challenges start to come up, namely the security role and the integration with the business teams. 
As such, buzz words like _DevSecOps_ and even _DevSecOpsBiz_ are becoming more popular in discussions. 

This lab session builds on top of _AI-APP-ST201: The new trends of Dev*Ops (DEV-SEC-OPS-BIZ)_, allowing you to experience first hand the construction of a real world scenario.

## Prerequisites 
Before we get started we need to ensure some prerequisites required for the lab.

* Azure Account [Azure Portal](https://portal.azure.com)
* Azure DevOps Services Organization [Azure DevOps](https://dev.azure.com/)

## Lab steps
* Start by [creating an Azure DevOps Project](#AzDevOps)
* Now let's [setup the build and release for the application](#CICD)
* Next, we'll want to [include Security into the pipeline](#Security)
* And to wrap up, let's [gather Business information](#Business)


> Optional: Connect Azure DevOps to Power BI
[Create an active bugs report in Power BI based on a custom Analytics view](https://docs.microsoft.com/en-us/azure/devops/report/powerbi/active-bugs-sample-report?view=vsts&tabs=new-nav)


*********

<a name="AzDevOps"></a>
# Lab: Create Azure DevOps Project 

This workshop will guide you through the initial setup of an Azure DevOps Project, providing a quicker, prebuilt setup ([option 1](#Option#1:-Azure-DevOps-Labs-++)), and a step by step setup ([option 2](#Option-#2:-Azure-DevOps-from-scratch)).

## Setup Azure DevOps Project

### Option #1: Azure DevOps Labs ++

>  Use Azure DevOps Labs to create a preconfigured project and enrich it for a quick start.

* Start by creating a new Project using a preselected [Lab](https://azuredevopsdemogenerator.azurewebsites.net/?name=WhiteSource-Bolt&templateid=77362)
    1. Navigate to the Azure DevOps Demo Generator and *Sign In* with the credentials you've used to create the Azure DevOps Organization:
    
        ![Azure DevOps Demo Generator - Sign In](img/AzureDevOpsLab-SignIn.png)

    2. Select your Organization from the dropdown, fill in the Project Name, and *Create Project*:

        ![Azure DevOps Demo Generator - Create Project](img/AzureDevOpsLab-CreateProject-01.png)

    3. Wait for a few seconds for the project to create and then *Navigate* to it:

        ![Azure DevOps Demo Generator - Create Project](img/AzureDevOpsLab-CreateProject-02.png)

* Import additional Git repos, required for the labs:

    1. Navigate to *Repos* and on the upper repositories drop down, select *Import repository*:

        ![Azure DevOps Demo Generator - Navigate to Project](img/AzureDevOpsLab-ImportRepo.png)

    2. Fill in the *Clone URL* with    `https://github.com/Microsoft/SmartHotel360-Website.git`
    and press *Import*:

        ![Azure DevOps Demo Generator - Navigate to Project](img/AzureDevOpsLab-CloneURL.png)

    3. Select *Import repository* again, now filling with     `https://github.com/Deliveron/owasp-zap-vsts-extension.git`
    and press *Import*:

        ![Azure DevOps Demo Generator - Navigate to Project](img/AzureDevOpsLab-CloneURL.png)


## Next step:  
[Setup the build and release for the application](#CICD)

*********

<a name="CICD"></a>
# Lab: Azure DevOps CI/CD

This lab will guide you through building Continuous Integration (CI) and Continuous Deployment (CD) pipelines with Azure DevOps. The build pipeline will make use of a Java application, built with Maven, but also a .NET Core and Azure Functions App.
For the release pipeline we'll be leveraging ARM templates and Azure App Services to host our application.

## Create Build Pipeline

* Wait a few seconds for the import process to finish and navigate to *Pipelines*, *Builds*:

    ![Navigate to Pipelines, Build](img/AzureDevOpsLab-Builds-01.png)

    ### WhiteSource Bolt Build
    1. Under *New*, select *Import a pipeline* to import a precooked pipeline to build the recently imported repo:

        ![Import a build pipeline](img/AzureDevOpsLab-Builds-02.png)

    2. Drag and drop the `SmartHotel_Petchecker-Web.json` file, or Browse for the same file. Then, press *Import* to start the import process:

        ![Start the build pipeline import process](img/AzureDevOpsLab-Builds-03.png)
    
    3. Select the `Hosted VS2017` Agent pool:

        ![Build pipeline agent pool](img/AzureDevOpsLab-Builds-04.png)

    4. Now select the Source Repo to the recently imported repository:

        ![Build pipeline Source repo](img/AzureDevOpsLab-Builds-05.png)

    5. To finish, enable the *Continuous integration* trigger, saving the build after it:

        ![Build pipeline trigger](img/AzureDevOpsLab-Builds-trigger.png)

    ### OWASP Build
    
    Now we'll be using an alternative way to setup our CI build, leveraging a YAML file.

    6. Navigate to the `owasp-zap-vsts` repo, and drag and drop the `azure-pipelines.yml` file, located on the Lab contents you've downloaded, under *~/files/OWASP*


## Create Release Pipeline

* Under *Pipelines*, navigate to *Releases* and press `New pipeline`

     ![Releases pipeline](img/AzureDevOpsLab-Releases-01.png)

    1. We first need to create a dummy, empty, Release pipeline in order for the *Import* to become available. 
    Let's do this by pressing `New pipeline`, `Empty job` and `Save`:

    ![Select empty process](img/AzureDevOpsLab-Releases-02.png)

    2. Navigate back to `All pipelines` and `Import a release pipeline`:

    ![All pipelines](img/AzureDevOpsLab-Releases-04.png)

    ![Import release pipeline](img/AzureDevOpsLab-Releases-05.png)

    3. Drag and drop, or navigate, to select the `SmartHotel360_Website-Deploy.json` file:

    ![Import release pipeline](img/AzureDevOpsLab-Releases-06.png)

    4. Press *OK* to start the import process. You should now have a release pipeline like this:

    ![Import release pipeline](img/AzureDevOpsLab-Releases-07.png)

    5. Navigate to the Stage tasks:

    ![Import release pipeline](img/AzureDevOpsLab-Releases-08.png)

    6. Select the first task and, under *Azure Subscription*, press `New`:

    ![Release pipeline CD trigger](img/AzureDevOpsLab-Releases-09.png)

    7. This opens a pop up where we'll have to fill in the details of our *Azure Subscription*, where we'll be deploying out solution:

    > Step in each one of the options with error, selecting and authorizing an Azure Subscription to use in the lab. 

    8. To finish, enable the Continuous Deployment trigger

    ![Import release pipeline](img/AzureDevOpsLab-Releases-trigger.png)
    

#### Run a test build

1. In Azure DevOps, click on Builds, select each build and click the "Queue" button on the right upper corner.

    ![Azure DevOps Build](img/AzureDevOpsLab-Builds-Run-01.png)

2. Monitor the builds and wait for the build to complete

    ![Azure DevOps Build](img/AzureDevOpsLab-Builds-Run-end.png)

# ADD INFO TO OPEN WEBSITE AND SEE IT WORKED

3. The release will automatically start when the build is complete (be patient, this can take some time). Review the results as it is complete. 

    ![Azure DevOps Release](img/AzureDevOpsLab-Releases-Run-executing.png)

4. Now kick-off the full CI/CD pipeline by making an edit to the  code in the Azure DevOps code repo.
Navigate back to *Repos*, *SmartHotel360-Website* repo, select `appsettings.Development.json` and press *Edit*

    ![Repo change to trigger CI CD](img/AzureDevOpsLab-Repo-edit.png)

5. Change the *Name* property value to something you want, and *Commit* the change after it

    ![Repo change to trigger CI CD](img/AzureDevOpsLab-Repo-commit.png)


## Next step:  
[Include Security into the pipeline](#Security)

*********

<a name="Security"></a>
# Lab: Security

This lab will guide you through adding some Security validations into our pipelines, detecting and fixing security vulnerabilities, but also problematic open source licenses.

## Review WhiteSource Bolt task configurations on Build
> TALK A LITTLE ABOUT EACH TASK AND IS THEIR PURPOSE 

1. In Azure DevOps, click on "Pipelines" on the left menu and then click "Builds"

2. Select each build pipeline, click the "Edit" button, and select the `WhiteSource Bolt` task

    ![WhiteSource Bolt task](img/AzureDevOpsLab-Builds-WhiteSourceBolt.png)

3. Now navigate to *Pipelines*, *WhiteSource Bolt* on the left and explore the generated reports

    ![WhiteSource Bolt report](img/AzureDevOpsLab-Builds-WhiteSourceBolt-report.png)


## Add OWASP ZAP penetration testing tool to the Release pipeline

1. Setup a Docker host
> Steps to run the commands in Cloud Shell
> create MD for this
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/dockerextension


2. Start by obtaining a personal access token (PAT) for later use.
> Save that PAT token, it can't be retrieved later!

![Navigate to User Security](img/PAT-token-security.png)
![Generate PAT Token](img/PAT-token-navigate.png)
![Generate PAT Token](img/PAT-token-create.png)
![Copy PAT Token](img/PAT-token.png)


Now let's add some `Command` tasks to our release pipeline, one for attaching the generated analysis report and another to be able to create bugs if necessary:

![Add OWASP task](img/Add-OWASP-tasks-navigate.png)
![Add OWASP task](img/Add-OWASP-tasks-search.png)

2. Paste this command on the *Script* text box, changing the values in bold*, as seen in the image.
`$(System.DefaultWorkingDirectory)/owasp-zap-vsts CI/drop/owasp-zap-vsts-tool/bin/Release/owasp-zap-vsts-tool.exe Arguments: attachreport collectionUri="https://myacct.visualstudio.com" teamProjectName="MsReadyLab" releaseUri=$(Release.ReleaseUri) releaseEnvironmentUri=$(Release.EnvironmentUri) filepath=$(System.DefaultWorkingDirectory)\OwaspZapReport.html personalAccessToken=abc123`

![Add OWASP task](img/Add-OWASP-tasks-Report.png)

3. Now paste this for the *Create bugs* task.
`$(System.DefaultWorkingDirectory)/owasp-zap-vsts CI/drop/owasp-zap-vsts-tool/bin/Release/owasp-zap-vsts-tool.exe arguments: createbugfrompentest collectionUri="https://myacct.visualstudio.com" teamProjectName="CLExtended" team=Demo releaseUri=$(Release.ReleaseUri) releaseEnvironmentUri=$(Release.EnvironmentUri) filepath=$(Agent.ReleaseDirectory)\OwaspZapAlerts.xml personalAccessToken=abc123`

![Add OWASP task](img/Add-OWASP-tasks.png)


## Next step:  
[Gather Business information](#Business)

*********

<a name="Business"></a>
# Lab: Azure DevOps Business

This workshop will guide you through the process of creating and configuring a set of specialized dashboards, each with a diferent scope that can be used by distinct team members and stakeholders. 

## Create Build Pipeline

1. Create [Queries, Dashboards, charts, & widgets](https://docs.microsoft.com/en-us/azure/devops/report/dashboards/overview?view=vsts)