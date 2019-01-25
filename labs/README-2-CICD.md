[![Build Status](https://dev.azure.com/MSREADY19Sandbox/devsecopsbiz-session/_apis/build/status/technical-lab?branchName=master)](https://dev.azure.com/MSREADY19Sandbox/devsecopsbiz-session/_build/latest?definitionId=4&branchName=master)


# Microsoft Ready, Feb 2019
## AI-APP-ST300: Hands on Dev*Ops (Dev-Sec-Ops-Biz) 

**Welcome to Technical Lab for the AI-APP-ST300: Hands on Dev*Ops session!**

DevOps has been propagating throughout the world as the place to be in order to be Agile and successful. 
As maturity sets in, new challenges start to come up, namely the security role and the integration with the business teams. 
As such, buzz words like _DevSecOps_ and even _DevSecOpsBiz_ are becoming more popular in discussions. 

This lab session builds on top of _AI-APP-ST201: The new trends of Dev*Ops (DEV-SEC-OPS-BIZ)_, allowing you to experience first hand the construction of a real world scenario.

# Lab: Azure DevOps CI/CD

This lab will guide you through building Continuous Integration (CI) and Continuous Deployment (CD) pipelines with Azure DevOps. The build pipeline will make use of a Java application, built with Maven, but also a .NET Core and Azure Functions App.
For the release pipeline we'll be leveraging ARM templates and Azure App Services to host our application.

## Create Build Pipeline

* Wait a few seconds for the import process to finish and navigate to *Pipelines*, *Builds*:

    ![Navigate to Pipelines, Build](../img/AzureDevOpsLab-Builds-01.png)

    ### WhiteSource Bolt Build
    1. Under *New*, select *Import a pipeline* to import a precooked pipeline to build the recently imported repo:

        ![Import a build pipeline](../img/AzureDevOpsLab-Builds-02.png)

    2. Drag and drop the `SmartHotel_Petchecker-Web.json` file, or Browse for the same file. Then, press *Import* to start the import process:

        ![Start the build pipeline import process](../img/AzureDevOpsLab-Builds-03.png)
    
    3. Select the `Hosted VS2017` Agent pool:

        ![Build pipeline agent pool](../img/AzureDevOpsLab-Builds-04.png)

    4. Now select the Source Repo to the recently imported repository:

        ![Build pipeline Source repo](../img/AzureDevOpsLab-Builds-05.png)

    5. To finish, enable the *Continuous integration* trigger, saving the build after it:

        ![Build pipeline trigger](../img/AzureDevOpsLab-Builds-trigger.png)

    ### OWASP Build
    
    Now we'll be using an alternative way to setup our CI build, leveraging a YAML file.

    6. Navigate to the `owasp-zap-vsts` repo, and drag and drop the `azure-pipelines.yml` file, located on the Lab contents you've downloaded, under *~/files/OWASP*


## Create Release Pipeline

* Under *Pipelines*, navigate to *Releases* and press `New pipeline`

     ![Releases pipeline](../img/AzureDevOpsLab-Releases-01.png)

    1. We first need to create a dummy, empty, Release pipeline in order for the *Import* to become available. 
    Let's do this by pressing `New pipeline`, `Empty job` and `Save`:

    ![Select empty process](../img/AzureDevOpsLab-Releases-02.png)

    2. Navigate back to `All pipelines` and `Import a release pipeline`:

    ![All pipelines](../img/AzureDevOpsLab-Releases-04.png)

    ![Import release pipeline](../img/AzureDevOpsLab-Releases-05.png)

    3. Drag and drop, or navigate, to select the `SmartHotel360_Website-Deploy.json` file:

    ![Import release pipeline](../img/AzureDevOpsLab-Releases-06.png)

    4. Press *OK* to start the import process. You should now have a release pipeline like this:

    ![Import release pipeline](../img/AzureDevOpsLab-Releases-07.png)

    5. Navigate to the Stage tasks:

    ![Import release pipeline](../img/AzureDevOpsLab-Releases-08.png)

    6. Select the first task and, under *Azure Subscription*, press `New`:

    ![Release pipeline CD trigger](../img/AzureDevOpsLab-Releases-09.png)

    7. This opens a pop up where we'll have to fill in the details of our *Azure Subscription*, where we'll be deploying out solution:

    > Step in each one of the options with error, selecting and authorizing an Azure Subscription to use in the lab. 

    8. To finish, enable the Continuous Deployment trigger

    ![Import release pipeline](../img/AzureDevOpsLab-Releases-trigger.png)
    

#### Run a test build

1. In Azure DevOps, click on Builds, select each build and click the "Queue" button on the right upper corner.

    ![Azure DevOps Build](../img/AzureDevOpsLab-Builds-Run-01.png)

2. Monitor the builds and wait for the build to complete

    ![Azure DevOps Build](../img/AzureDevOpsLab-Builds-Run-end.png)

# ADD INFO TO OPEN WEBSITE AND SEE IT WORKED

3. The release will automatically start when the build is complete (be patient, this can take some time). Review the results as it is complete. 

    ![Azure DevOps Release](../img/AzureDevOpsLab-Releases-Run-executing.png)

4. Now kick-off the full CI/CD pipeline by making an edit to the  code in the Azure DevOps code repo.
Navigate back to *Repos*, *SmartHotel360-Website* repo, select `appsettings.Development.json` and press *Edit*

    ![Repo change to trigger CI CD](../img/AzureDevOpsLab-Repo-edit.png)

5. Change the *Name* property value to something you want, and *Commit* the change after it

    ![Repo change to trigger CI CD](../img/AzureDevOpsLab-Repo-commit.png)


## Next step:  
[Include Security into the pipeline](README-3-Security.md)