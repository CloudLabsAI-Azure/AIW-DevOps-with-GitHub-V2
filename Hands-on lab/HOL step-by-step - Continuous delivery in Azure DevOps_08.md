## Exercise 4: Create Azure DevOps Multi Stage Release Pipeline  

Duration: 30 Minutes

In this exercise, you will modify the existing pipeline to include a basic release stage that performs the following tasks:
- Automated deployment of build artifacts to Azure Pipeline storage. 
- Deploy to the three stages created earlier (dev, test, and production).

### Task 1: Modify YAML definition to create a multistage pipeline  

1. Now that we have a great build working, we can modify the YAML file to include stages.  At first, we will add one stage for Build and then run that so we can see the difference in output.  

    From left navigation, select **Pipelines** to view configured Pipelines.   From here, highlight your new pipeline definition and select Edit from the ellipses to the right:  

    ![A screen showing pipeline instance edit menu.](images/stepbystep/media/image1000.png "Pipeline runs")  

    This action shows the **Azure Pipelines YAML Editor** that you viewed after building your initial pipeline.  You will be using this editor to make changes to your azure-pipelines.yml definition in the next steps.  

    ![A screen showing pipeline YAML Editor.](images/stepbystep/media/Image1001.png "Pipeline YAML Editor with Task Panel")  
    
    On the left, is the YAML editor containing the pipeline definition and the Tasks panel to the right, has common components that can be added to the pipeline.   Selecting from the task panel to add a component first shows a property panel supporting custom configuration for your pipeline, allowing fast configuration, and the result is additional formatted YAML added directly to the pipeline definition with the configuration customization you provided.  

2. Let's transform this pipeline to a multi-stage configuration by adding the following configuration right below the *trigger* section to define a **Build Stage** in your YAML pipeline.  

    ```yml  
        stages:
        - stage: Build
          displayName: 'Build Stage'
          jobs:
          - job: Build
    ```  
   This is the first step to a multi-stage pipeline!  
   
   You can define whatever stages you want to reflect the true nature of your CI/CD process, and as an added benefit, users get better visibility to entire pipeline process.  
   
   >**Note**: YAML is whitespace sensitive!  Indentation matters in a similar fashion as Python, so pay particular attention to formatting within this file.  The editor will highlight most formatting issues.  If you are off on your spacing at all, the file will likely contain errors, such as `Unexpected value 'steps'`.
   
   After adding this structure, your result should look like this:  

    ![A screen showing adding YAML stage code.](images/stepbystep/media/image1002.png "Build Stage YAML")  

3. Next, simply **highlight the remainder of the YAML file** that defines your build jobs and indent it four spaces (two tabs), thus making this definition a child of the build stage *jobs* node.   Your YAML should look like this now:

    ![A screen showing highlight of build code under stage definition.](images/stepbystep/media/Image1003.png "Formatting Build Stage YAML")

    **Take a moment now to triple-check your indentation is correct**:  

    * trigger is not indented
    * stages is not indented
    * Pool is indented four spaces and lines up with the 'j' in 'job' above it.
    * Everything else is also appropriately indented (you should be able to collapse the file at this point, so that all that shows is the stage)  Note that your line numbers may differ slightly from what is shown. 

    ![An image showing the yaml collapsed to prove indentation is correct.](images/stepbystep/media/image1003a.png "Collapsed Build Stage YAML")

4. You now have a very simple multi-stage pipeline with exactly one stage - a **Build Stage**.   
   
   Running the pipeline now would execute the pipeline as a single stage, and it would build exactly like it did before.  For now, be aware that using simple stage definitions like this means the stages execute in the order they are defined in the file.  More advanced pipeline definitions can support conditionals for dependency graphs that govern more complex stage execution.

   Now, let's add a **Deployment Stage** by adding the YAML below to the bottom of the pipeline definition:


    ```yml
    - stage: DevDeploy  
      displayName: 'Dev Deploy Stage'
      jobs:
      - job: Deploy
        pool:
          name: Hosted VS2017
        steps:
    ```

    This is a simple definition for a Deployment Stage that by definition, will execute after the Build Stage because it is defined after the build stage. 
    
    Your YAML definition should now look like this:

    ![A screen showing simple Deploy Stage scaffolding.](images/stepbystep/media/image1004.png "Deploy Stage YAML")

5. Now your pipeline definition file contains a *build stage and a deploy stage*.  For now, let's configure the deploy stage to deploy to the dev environment using deployment slots.   Then we can repeat this configuration to support test and production in a similar manner. perform the same action.  

    Set your cursor on a new line at the end of your YAML definition, and note this will be the location where new YAML is added in the next step:

    ![A screen showing preferred cursor location to add tasks using the YAML Editor Task panel.](images/stepbystep/media/Image1005.png "YAML Editor Cursor EOF")


6. Using the Tasks panel, select the *Azure App Service Deploy* Task:  

    ![On the Pipeline Tasks panel, Azure App Service Deploy Task is highlighted.](images/stepbystep/media/image1006.png "Select Task")
    
    This will show a configuration panel to configure this deployment task with some fields containing default values:

    ![A screen showing the App Service Deploy Task configuration options.](images/stepbystep/media/image1007.png "Default Task Configuration Panel")

    Leave the **Connection type** as default, but in Azure Subscription, select the service connection you used earlier in the lab.   
    
    For **App Service type**, leave as default, and for **App Service name**, select the development appnamedropdown list, select **TailspinToys**.    
    
    Check **Deploy to Slot or App Service Environment**, and you should see additional configuration settings appear.   
    
    Set **Resource group** to the resource group you have been using, and select "Staging" for the **Slot**.   Leave all other fields as default, as we will configure those later.  

    At this point, the panel should look like this:

    ![On the Task Configuration, the image shows the Azure App Service deploy with reqwured values .](images/stepbystep/media/image1008.png "Task Configuration Panel")

    If the service connection is not authorized, you may be asked to authorize the service connection like this:

    ![In the Pipeline Task Configuration, the image shows Authorization panel.](images/stepbystep/media/image1009.png "Azure DevOps Authorization Prompt")
     > **Note**: You may not be able to authorize with Subscription, in that case Select your Azure subscription from the Azure subscription dropdown list and then click the dropdown option next to Authorize button and select Advanced options. You will be navigated to Add an Azure Resource Manager service connection prompt, Now verify the Connection name, Scope level and Subscription and enter the value for Resource Group from the drop down list (i.e. TailSpinToysRG) and click OK

    In this scenario, select Authorize to enable the integration with Azure DevOps. 
    
    Select **Add** to add this task as configured to your pipeline definition file, and on completion, you can see that the following YAML has been added in the YAML editor:

    ![In the Pipeline YAML editor, the image shows the YAML result from adding the Azure App Service deploy Task.](images/stepbystep/media/image1010.png "Pipeline YAML Editor")  

    > **Note:** Pay close attention to the final line `packageForLinux`.  It is highly likely you will need to update this line to match the image above to use the correct drop location:    

    ```  
    '$(Build.ArtifactStagingDirectory)/drop/*.zip'
    ```  
    
7. At this point you now have a **Build Stage** that builds your project and publishes an artifact to a known location in Azure Pipelines.   You also have a **Deploy Stage** that will deploy the artifact to your dev environment, however, you need to make some additional adjustments to this stage to tie everything together. 

    Looking at the last task of your build stage you can see that the publish task places the build artifacts in a specific location: 

    ![In the code editor, the Publish Build Artifacts Tasks definition is highlighted.](images/stepbystep/media/image1011.png "Pipeline YAML Properties")

    Your deploy stage needs to download the artifacts from the Build Stage published location in order to install them in the dev environment, and Azure Pipelines has a task template for that.   
    
    In the YAML editor, place your cursor at this position, right before the AzureRmWebAppDeployment task you just added:

    ![Screen showing preferred cursor position in the YAML Editor.](images/stepbystep/media/image1012.png "Cursor Position in YAML Editor")
    
    Search Tasks for *"download build"* and select the **Download Build Artifacts** task.   
    
    ![Screen showing YAML Editor Task panel Search for download build.  The Download Build Artifacts Template and Add button are highlighted.](images/stepbystep/media/image1013.png "Download Task Selected")
    
    As before, a configuration panel is shown so you can configure the task before adding:
    
    ![Screen showing close up of the Download Build Artifacts template with Current build, Specific artifact, and Add button highlighted.](images/stepbystep/media/image1014.png "Download Task Configuration Panel")
    
    For now, let's use the default values, and select **Add**.   
    
    This will add the task as configured to your YAML.  As an alternative, you can select tasks and add them, and then edit their properties directly in the YAML editor.  
    
    Finally, be sure to check task indenting:

    ![Screen showing YAML code highlighted for indent check in YAML Editor.](images/stepbystep/media/image1015.png "YAML formatting in Editor")
    
    
8.  The task you just added needs one additional property added in order to be able to execute properly.  We could have added this property using the UI, but let's modify the task by editing the YAML directly.  
    
    In the editor, modify the following:
    - Change the **downloadPath** property to *'$(Build.ArtifactStagingDirectory)'*.
    - Add a property *artifactName* to the task you just added, just under *downloadPath*, and set this new property to *"drop"*.   
    
    Your Download Task now matches the artifact staging directory that the Publish task above uses during the build stage.   
    
    Your YAML should now look like this:

    ![Screen showing YAML code highlighted on artifactName property for value edit in the YAML Editor.](images/stepbystep/media/image1016.png "Download Path YAML Property Configuration")

    
9.  At this point, the deployment stage can find and download the build artifacts during execution. However, the deployments and downloads will publish the files with successful build or commit regardless of what branch it comes from. You can add the following conditions to your tasks to ensure the environment matches only the ones you are expecting to ensure pull requests that are coming in do not trigger deployments:

    ```yml
    condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/master'))
    ```

    Note that the "refs/heads/**master**" is the reference to the branch name.  Move your cursor to a line after the `job: Deploy` and paste the line above.

    ![Screen showing YAML code highlighted on conditions property for value edit in the YAML Editor](images/stepbystep/media/image1052.png "Conditional processing YAML Property Configuration")

10.  The deployment should now happen only to builds within the master branch of your deployment even if they're the validation of a pull request.  Review your YAML file for proper indentation and then select **Save** to commit changes to the pipeline.
    ![Screen showing highlighted Save button on the pipeline YAML Editor.](images/stepbystep/media/image1017.png "Save Pipeline")

11. Azure DevOps will prompt for the commit message and the commit goes directly to the master branch: 

    ![Screen showing a commit panel with Save button highlighted.](images/stepbystep/media/image1018.png "Commit Confirmation")
    
12. Since this changes the master branch, and your pipeline is configured to trigger on master, the pipeline will immediately run.   Using the left menu, navigate to **Pipelines** select the new build:

    ![Screen showing left navigation options with Pipelines highlighted.](images/stepbystep/media/image1019.png "Azure DevOps LeftNav - Pipelines")
    
    From here you can see the multiple stages you've just added in the **Stages** column.  
    
    ![Screen showing recent pipeline run from the previous commit task with the Runs tab, build name and the Tasks item is highlighted.](images/stepbystep/media/image1020.png "Pipeline Run")


13. When the **Build** stage completes, select the **Deploy** stage to follow each task:

    ![Screen showing the Build and Deploy Stage recently added.](images/stepbystep/media/image1021.png "Deploy Stage Pipeline Run Detail!")

    Expand the **AzureRmWebAppDeployment** task to review the steps performed during the Azure deployment. Once the task completes, your app is live on Azure.

    ![Screen showing stage execution log view with AzureRmWebAppDeployment highlighted.](images/stepbystep/media/image1022.png "Deployment Task Detail")

    
14. **Congratulations!** You have just created your first multistage pipeline!  Now, let's verify your deployment.   

    Using **Azure Portal**, navigate to the resource group you created earlier to view your app services in this resource group .   Sort by **Type** Select the development app service staging slot:

    ![Screen showing Azure Portal provisioned assets in lab resource group , the dev Web App Service and sorted type column header are highlighted.](images/stepbystep/media/image1023.png "Azure Portal Resources")  

    On the App Service Overview, select **Browse**.

    ![Screen showing Azure Portal detail view of provisioned development web app service with Browse highlighted.](images/stepbystep/media/image1024.png "Azure Portal - App Service Detail")  

    This will launch your default browser navigating to your development site:  

    ![Screen showing Microsoft Edge browser showing development application.](images/stepbystep/media/image1025.png "Application Home Page")  

    A successful deployment!  In the next task we will add stages for deploying to Test and Production.   Once you deploy, you can use this step to verify those sites too.  

### Task 2: Add Test and Production Environments as stages in the pipeline  

You could repeat the process in **Task 1** to add stages for Test and Production by using the Tasks panel.  However, the beauty of the unified YAML pipeline definition is the speed at which you can "copy-paste" the Development Deploy Stage within the YAML editor, and then just change the particular values for your Test and Production environments.   Let's add a Test deployment stage now.  

1. Return to Azure DevOps Pipeline view and select your new multistage pipeline and select **Edit** for the YAML editor.   

    Scroll down to the Development Deploy Stage and highlight and copy the script for that entire stage:  

    ![Screen showing YAML Editor and Development Deployment Stage is highlighted for copy-paste operation.](images/stepbystep/media/image1026.png "Pipeline YAML Editor")  

2. Move your cursor to the very end of the YAML definition file and paste the copied development environment deployment stage code.  Now you can look though the newly pasted stage and change certain properties to match your Test environment.  Begin by changing the **stage:** string name property to *TestDeploy* and then, change the **DisplayName** property to *Test Deploy Stage*.  

3. Move to the nested Deployment Task, and change **WebAppName** to match the Web App Name for your test environment, in this case *tailspintoys-test-\<randomstring>*  

4. Leave every other property the same.  Your YAML should now look like this:  

    ![Screen showing YAML Editor with added Test Deployment Stage.](images/stepbystep/media/image1027.png "Pipeline YAML Test Deployment Stage")  

    Select **Save**.   
    
    ![Screen showing Commit panel with.](images/stepbystep/media/image1028.png "Commit Confirmation")  

    As before, add your commit message, and select **Save**.  This will save the YAML definition file contents, commit to the master branch and which will trigger a pipeline run.  

5. Let's go take a look at the pipeline run. Navigate to Pipeline view to view recently run pipelines.  You can see the run triggered from your committed change here.  
    
    ![Screen showing Pipeline run with run details highlighted.](images/stepbystep/media/image1029.png "Pipeline Run")  

    Select this newest run and let's dig deeper.  

    ![Screen showing pipeline run details with multiple stages now added.](images/stepbystep/media/image1030.png "Pipeline Run Detail")  

    In this view, you can see that your multistage pipeline now has 3 stages:  Build, Dev, Test.    
    
    Selecting the **Test Deploy Stage** flow box shows you the Jobs detail view with access to all the tasks that executed.   Note that on the **AzureRmWebAppDeployment** task, you can see navigable links for deployment history and the application URL:  

    ![Screen showing Pipeline Job Detail View with AzureRmWebAppDeployment task selected.  Hightlighted are the deployment log and app URL.](images/stepbystep/media/image1031.png "Deployement Taks Detail")  

6. At this point you have configured a working multistage pipeline that builds, publishes and deploy to two of your provisioned environments (Dev and Test).  Repeat the steps 1-5 above, to add a Test deployment stage to create a **Production Deployment Stage**.  Take careful note of the properties you changed above to edit them for the production environment, and save the pipeline configuration.  

7. If your configuration was successful, this should have triggered a pipeline run that looks like this:

    ![Screen showing Pipeline run.](images/stepbystep/media/image1032.png "Pipeline Runs")

Congratulations! You have completed the creation of a release pipeline with four stages.   In the screen shot above you can see your progression in including new functionality by added each modification to your Unified YAML Pipeline.

