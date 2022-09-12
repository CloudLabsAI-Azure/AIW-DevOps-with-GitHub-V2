## Exercise 3: Create Azure DevOps build pipeline

Duration: 15 Minutes

**Azure DevOps Pipelines**

 Implementing CI and CD pipelines helps to ensure a consistent, repeatable process is used to build, test, and release code.   This results in higher quality code that's readily available to users.  Azure DevOps Pipelines provides an easy and extensible way to provide consistency when building and releasing your projects, while also making the configuration available to authorized users on your team.   Let's take a high-level look at the major components that make up an Azure DevOps Pipeline:  

**Stages** 

In essence, Azure Pipelines are made of one or more *stages* representing a given CI/CD process and are the major divisions of action in a pipeline.  Actions such as: "build this app", "run these tests", and "deploy to this environment" are good examples of stages.  Stages themselves, decompose to of one or more *Jobs*.  

**Jobs**

Jobs consist of a linear series of steps within a stage, where each step can be tasks, scripts, or references to external YAML templates that represent the tactical aspects of an action.  It is important to note that both stages and jobs can run in a simple linear fashion, or may be arranged into more complex *dependency graphs*, e.g. "run this stage before that one" or "this job depends on the output of that job".   

From here you can see that this simple relationship can embody both simple and complex staged build and release processes through a defined execution hierarchy. For Azure DevOps, this hierarchy is defined in the structure of a YAML (Yet Another Markup Language) file, which is a structured markup file that can be managed like any other source file.

**Configuration As Code**

This entire concept is based on a *Configuration As Code* methodology.   This means declaratively defining the pipeline, and pipeline components such as stages, tasks, and conditions in detail.   Using YAML provides more visibility into pipeline structure and condition in once concise place, and also provides integration and automation opportunities as well.  In Azure DevOps, YAML defines both "Build" or "Continuous Integration" pipelines as well as "Release" or "Continuous Delivery" pipelines in one shot, and this is what is meant by the term *"Unified YAML Pipeline"*.    

While teams can use the **Azure DevOps Pipeline visual designer** to create multistage build and release pipelines to support a wide array of CI/CD scenarios, many teams prefer to define their build and release pipelines by editing the YAML configuration directly. A YAML build definition can be added to a project by including the YAML source file at the repository root. Azure DevOps will reference this configuration, evaluate it, and execute the configuration during build runs.  

Azure DevOps also provides default templates within the editing workflow, for popular project types, integration points, and common tasks, and this works alongside a simple YAML designer to streamline the process of defining build and release tasks.

In this lab, you will build up a pipeline YAML definition - *"azure-pipelines.yml"* - representing a simple multi-stage pipeline with a custom trigger and a Pull Request Policy configuration.   In the following exercise you will use the Azure DevOps Pipelines UI to create a build definition for the current project, but in subsequent exercises, you will be editing the YAML directly using the *Unified YAML* workflow. 
  
### Task 1: Create a build pipeline
You will start with creating a basic build pipeline, tie it to the existing repository for to lay the groundwork for a basic CI scenario.   Then, you will expand the capability of the pipeline to include stages - transforming it into a multi-stage pipeline - representing basic CD characteristics within the same pipeline.  

build the web application with every commit of source code. This will lay the groundwork for us to then create a release pipeline for publishing the code to our Azure environments.


1. In your Azure DevOps project, select the **Pipelines** menu option from the left-hand navigation.

    ![In the Azure DevOps window, Pipelines is highlighted in the ribbon.](images/stepbystep/media/image68.png "Azure DevOps Left Nav - Files")

2. Select the **Create pipeline** button to create a new build pipeline.

    ![In Builds, Create pipeline is highlighted.](images/stepbystep/media/image69.png "Create a new pipeline")

3. This starts a wizard where you'll first need to select where your current code is located. In a previous step, you pushed code up to Azure Repos. Select the **Azure Repos Git** option.

    ![A screen that shows choosing the Azure Repos option for the TailspinToys project.](images/stepbystep/media/image70.png "Where is your code?")

4. Next, you'll need to select the specific repository where your code was pushed. In a previous step, you pushed it to the **TailspinToys** repository. Select the **TailspinToys** git repository.

    ![A screen that shows choosing the TailspinToys repository.](images/stepbystep/media/image71.png "Select a repository")

5. Then, you'll need to select the type of pipeline to configure. Although this pipeline contains a mix of technologies, select **ASP.NET Core** from the list of options.

    ![A screen that shows choosing ASP.NET Core pipeline.](images/stepbystep/media/image72.png "Configure your pipeline")

6. As a final step in the creation of a build pipeline, you are presented with a configured pipeline in the form of an azure-pipelines.yml file.   Azure DevOps has placed this file at the repository root and will reference the file as configuration during pipeline runs.  
   
7. The YAML file contains a few lines of instructions (shown below) for the pipeline. Let's begin by updating the YAML with more specific instructions to build our application. 

    ![A screen that shows the starter pipeline YAML.](images/stepbystep/media/image72a.png "Review your pipeline YAML")

The *pool* section specifies which pool to use for a job of the pipeline. It also holds information about the job's strategy for running.

8. Select and replace the *pool* section with the following code:

    ```yml
    pool:
      vmImage: 'windows-latest'
      demands:
      - msbuild
      - visualstudio
      - vstest
    ```

    Steps are a linear sequence of operations that make up a job. Each step runs in its own process on an agent and has access to the pipeline workspace on disk. This means environment variables are not preserved between steps but, file system changes are.

9. Select and replace the *steps* section with the following code:
    
    ```yml
    steps:
    # Nuget Tool Installer Task
    - task: NuGetToolInstaller@1
      displayName: 'Use NuGet 5.5.1'
      inputs:
        versionSpec: 5.5.1      
    ```

    Tasks are the building blocks of a pipeline. They describe the actions that are performed in sequence during an execution of the pipeline.

10. Add additional tasks to your azure-pipelines.yml file by selecting and copying the following code. This should be pasted right after the NuGetToolInstaller@0 task which you pasted previously:
    
    >**Note**: The YAML below creates individual tasks for performing all the necessary steps to build and test our application along with publishing the artifacts inside Azure DevOps so they can be retrieved during the upcoming release pipeline process.

    ```yml
    # Nuget Restore Task
    - task: NuGetCommand@2
      displayName: 'NuGet restore'
      inputs:
        restoreSolution: '**/tailspintoysweb.csproj'

    # Node.js Tool Installer Task
    # Finds or downloads and caches the specified version spec of Node.js and adds it to the PATH
    - task: NodeTool@0
      inputs:
        versionSpec: '12.x' 

    # Build Task  
    - task: DotNetCoreCLI@2
      displayName: 'Build solution'
      inputs:
        command: publish
        publishWebProjects: True
        arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'  
        zipAfterPublish: true

    # Publish Task
    - task: PublishBuildArtifacts@1
      displayName: 'Publish Artifact'
      inputs:
        PathtoPublish: '$(build.artifactstagingdirectory)'
        ArtifactName: 'drop'
      condition: succeededOrFailed()
    ```

11. The final result should look like the following:

    ```yml
    trigger:
      - master

    pool:
      vmImage: 'windows-latest'
      demands:
      - msbuild
      - visualstudio
      - vstest

    variables:
      buildConfiguration: 'Release'

    steps:
    # Nuget Tool Installer Task
    - task: NuGetToolInstaller@1
      displayName: 'Use NuGet 5.5.1'
      inputs:
        versionSpec: 5.5.1

    # Node.js Tool Installer Task
    # Finds or downloads and caches the specified version spec of Node.js and adds it to the PATH
    - task: NodeTool@0
      inputs:
        versionSpec: '12.x' 
    
    # Nuget Restore Task
    - task: NuGetCommand@2
      displayName: 'NuGet restore'
      inputs:
        restoreSolution: '**/tailspintoysweb.csproj'

    # Build Task  
    - task: DotNetCoreCLI@2
      displayName: 'Build solution'
      inputs:
        command: publish
        publishWebProjects: True
        arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'  
        zipAfterPublish: true

    # Publish Task
    - task: PublishBuildArtifacts@1
      displayName: 'Publish Artifact'
      inputs:
        PathtoPublish: '$(build.artifactstagingdirectory)'
        ArtifactName: 'drop'
      condition: succeededOrFailed()
    ```
    At this point you have defined a simple, single stage pipeline, that will perform the following tasks:
    - execute on change commits to the master branch
    - install key tools required to build
    - build the code project, producing build artifacts
    - publish build artifacts to a known artifact location within Azure DevOps Pipelines.   

12. Choose the **Save and run** button to save our new pipeline and also kick off the first build.  

    ![A screen showing the contents of the YAML editor. The Save and run button is highlighted.](images/stepbystep/media/image73.png "Reivew your pipeline YAML - save highlighted")    

13. When the editor process saves your YAML, Azure DevOps Pipelines creates a new source file called *azure-pipelines.yml* to the root of your TailspinToys repository. This is done through a git commit that Azure DevOps facilitates as part of the save process which also prompts you to enter a commit message.  

    ![A screen that shows the commit of azure-pipelines.yml. The Save and run button is highlighted.](images/stepbystep/media/image74.png "Save and run")  
    
    By default, **Commit Message** will be populated for you, but you may change this. Select the **Save and run** button at the bottom of the screen to commit the pipeline changes to your master branch.  

14. The build process will immediately begin and run through the steps defined in your new *azure-pipelines.yml* definition file, and the screen will refresh to show you the build process executing, in real-time.  

    ![A screen that shows the real-time output of the build process.](images/stepbystep/media/image76.png "Real-time output")  

15. After the build process completes, you should see a green check mark next to each of the build pipeline steps.  

    ![A screen that shows a successfully completed build pipeline.](images/stepbystep/media/image77.png "Success")  
    
    **Congratulations**, you have just created your first build pipeline! In the next exercise, we will create a release pipeline that deploys your successful builds.  

