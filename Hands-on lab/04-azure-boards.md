## Exercise 4: Azure Boards and Test plans

### Task 1: Connect Azure Board with GitHub

We can automate our project tracking with the Azure Board integration for GitHub. In this task, you will connect your Azure DevOps project's board to your GitHub repository.

1. In your browser open GitHub Marketplace by navigating to the below URL:

    ``` 
    https://github.com/marketplace/azure-boards
    ```

    ![The Azure Boards Integration App on GitHub Marketplace that will provide a link between Azure DevOps Boards and GitHub issues.](media/hol-ex1-task1-step1.png "Azure Boards Integration App on GitHub Marketplace")

1. Scroll to the bottom of the page and select `Install it for Free`.

   ![](media/2dg50.png)
   
1. On the next page, select **Complete order and begin installation**.

1. Select the lab files repository `mcw-continuous-delivery-lab-files` which you created earlier and click on **Install & Authorize**.

   ![](media/2dg53.png)
    
   >**Note**: If you see the message **You’ve already purchased this on all of your GitHub accounts** this indicates Azure Boards integration is already used in your account, follow the below steps.
   
   - Scroll to the top of the Azure Boards Marketplace page and select **grant this app access to your GitHub account**.
   
   ![](media/2dg51.png)
   
   - Select the lab files repository `mcw-continuous-delivery-lab-files` which you created earlier and click on **Install & Authorize**.

   ![](media/2dg53.png)
    
1. Select the **aiw-devops** Azure DevOps organization and select the Fabrikam project then click on **Continue**

   ![](media/2dg54.png)

1. When the integration succeeds, you will be taken to the Azure DevOps Board. In the onboarding tutorial click on **Create** to create an initial Issue in the `To Do` Column.

   ![](media/2dg55.png)
    
1. Now click on **Create and link a pull request** to create a pull request associated with your Issue.

   ![After completion of the onboarding tutorial. Two todo confirmation messages displayed.](media/image15.png "Get started and quick tip")

1. Open the new Issue that the onboarding tutorial creates and observe the GitHub pull request and comments that are linked to the Azure DevOps board Issue.

   ![Linked GitHub items in an Azure DevOps issue in Boards.](media/hol-ex1-task1-step7-1.png "GitHub Pull Request and Comment")

1. In GitHub, browse to the `Pull Requests` tab of the lab files repository created in [Task 1 of the Before the HOL Instructions] and open the pull request that was created in the onboarding tutorial for the Azure Boards Integration App. Note the `AB#1` annotation in the pull request comments - this annotation signals to Azure DevOps that this pull request comment should be linked to Issue #1 in Azure Boards.

   ![Pull request detail in GitHub created by onboarding tutorial in previous steps.](media/hol-ex1-task1-step8-1.png "Pull Request detail")

1. Select the `Files changed` tab within the pull request detail and observe the change to the README.md associated with this pull request. After reviewing the changes, go back to the `Conversation` tab and select the `Merge pull request` button and confirm the following prompt to merge the pull request into the `main` branch.

   ![The file changes associated with the pull request.](media/hol-ex1-task1-step9-1.png "Pull Request Files Changed tab")

1. In Azure DevOps Boards, find the work item and observe that the issue has been moved to the `Done` column on completion of the pull request.

   ![A work item with a linked GitHub commit illustrating the link between Azure DevOps Boards and GitHub issues.](media/hol-ex1-task1-step10-1.png "Work Item with a Linked GitHub Commit")
   
### Task 2: Link GitHub Pull requests to Boards items   

1. In Azure Boards tab, Click on **New Item** ***(1)***, provide **Deploy WebApp** as description and create a new work item.

   ![](media/2dg57.png)
   
1. After creating a work item, Please note down the Work item ID which will be used in the further steps.

   ![](media/2dg58.png)
   
 1. Go to Environment details click on **Service principle Credentials** copy **Application id(clientId)** , **clientSecret(secretkey)** , **subscriptionId** and **tenantId** 
    
    ![spcreds](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/sp-creds-auth.png)
    
    Replace the values that you copied in the below Json.
    ```pwsh
    {
        "clientId": "...",
        "clientSecret": "...",
        "subscriptionId": "...",
        "tenantId": "...",
        "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
        "resourceManagerEndpointUrl": "https://management.azure.com/",
        "activeDirectoryGraphResourceId": "https://graph.windows.net/",
        "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
        "galleryEndpointUrl": "https://gallery.azure.com/",
        "managementEndpointUrl": "https://management.core.windows.net/"
    }
    ```
    
    Copy the complete JSON output to your clipboard.
   
1. In your GitHub lab files repository, select the **Settings** tab from the lab files repository.

   ![](media/2dg23.png)
   
1. Under **Security**, expand **Secrets** ***(1)*** by clicking the drop-down and select **Actions** ***(2)*** blade from the left navigation bar. Select the **New repository** ***(3)*** secret` button.

   ![](media/2dg24.png)
   
1. Under **Actions Secrets/New secret** page, enter the below mentioned details and Click on **Add secret** ***(3)***.  

1. Under **Actions Secrets/New secret** page, enter the below mentioned details and Click on **Add secret** ***(3)***.

   - **Name** : Enter **AZURE_CREDENTIALS** ***(1)***
   - **Value** : Paste the **JSON output** ***(2)*** copied in the previous step.

   ![](media/2dg59.png)
   
1. Select the **Code** ***(1)*** tab in your GitHub repository,  Navigate to **mcw-continuous-delivery-lab-files/.github/workflows/** ***(2)*** and select **docker-publish.yml** ***(3)*** file.

   ![](media/2dg60.png)
   
1. Copy the code from `https://raw.githubusercontent.com/CloudLabs-MCW/MCW-Continuous-delivery-in-Azure-DevOps/microsoft-devops-with-github-v2/Hands-on%20lab/docker-flow.yml` ***(1)*** link and paste it in the end of the file. Make sure there are no identation errors.

   ![](media/2dg61.png)
   
1. Click on **Start commit** ***(1)***, provide the details mentioned below and click on **Propose changes** ***(5)***.

   - Provide `workitem ID Updated` ***(2)*** as title. Make sure provide the same **Workitem ID** which was created in earlier step in Azure DevOps.
   - Select **Create a new branch for this commit and start a pull request** ***(3)***  and name new branch as **deploy webapp** ***(4)***.

   ![](media/2dg62.png)
   
1. On Open a pull request tab, Click on **Create pull request** 

   ![](media/2dg65.png)
   
1. Navigate to **Azure Boards**. Open the **workitem** ***(1)*** created in earlier step.

   ![](media/2dg63.png)

1. Observe that the **Pull request** has been linked to the workitem.

   ![](media/2dg64.png)
   
1. Navigate back to GitHub browser tab and select **Pull requests** tab.

   ![](media/2dg66.png)
   
1. Open the PR created from **deploy-webapp** branch and select **Merge pull request**.

   ![](media/2dg67.png)
   
1. Update the desciption as **fixed AB#{workitemID} updated** and select **confirm merge**.

   ![](media/2dg68.png)
   
1. Navigate back Azure Boards tab and notice that the **workitem** has been marked as **done**.

   ![](media/2dg69.png)
   
## Task 3: Configure Azure Test plan

1. From Azure DevOps tab, select **Test plans** from the side blade.

   ![](media/2dg71.png)
   
1. From thw Test plans tab, click on **+ New Test Plan**

   ![](media/2dg72.png)
   
1. In New Test Plan tab, provide the following details and click on **Create** ***(4)***.

   - Name: **TestPlan-<inject key="DeploymentID" enableCopy="false" />** ***(1)***
   - Area Path: **fabrikam-<inject key="DeploymentID" enableCopy="false" />** ***(2)**
   - Iteration: Leave it to **deafault** ***(3)***
   
   ![](media/2dg73.png)   
   
1. From fabrikam-<inject key="DeploymentID" enableCopy="false" /> test plan tab, select **more options** ***(1)*** button, hover over **New Suite** ***(2)***, and select **Static suite** ***(3)***.

   ![](media/2dg74.png)   

1. Create a new suite as **TestSuite-<inject key="DeploymentID" enableCopy="false" />**.

   ![](media/2dg75.png)  
   
1. From thw Test plans tab, click on **New Test case**.

   ![](media/2dg76.png)    
   
1. In the New Test Case pop up, provide the following details and click on **Save & Close** ***(8)***

   - Name: **Validate the web app** ***(1)***
   - Steps:
     - 1. Actions: **Access the Contoso web app** ***(2)*** Expected result: **Succeeded** ***(3)***          
     - 2. Actions: **Access Speakers page** ***(4)*** Expected result: **Succeeded** ***(5)***  
     - 3. Actions: **Access Sessions page** ***(6)*** Expected result: **Succeeded** ***(7)***

   ![](media/2dg77.png) 

1. From thw Test plans tab, navigate to **Execute** ***(1)*** tab, select the **validate the web app** ***(2)*** test point and click on **Run for web app** ***(3)***.

   ![](media/2dg78.png)
   
1. A web-based runner will be opened. Maunal testing of the web app can perfomed. Keep this page open, we'll will use the runner in upcoming steps.

   ![](media/2dg79.png)
   
1. On the Azure portal search for **Resource groups** in the search bar ***(1)*** and select **Resource groups** ***(2)*** from the suggestions. 

   ![](media/2dg80.png)   
   
1. In the resource group page, Select the **fabrikam-<inject key="DeploymentID" enableCopy="false" />** resource group fromthe list.

   ![](media/2dg81.png)  
   
1. Select the App service from the name, **fabrikam-web-<inject key="DeploymentID" enableCopy="false" />** from the list of resources. 

   ![](media/2dg82.png)
   
1. From the Overview page, access the web app using the **URL**.

   ![](media/2dg83.png)    

1. Verify the availability of the web app, speakers page, and sessions page. Simulatanously using the runner page, perform the mark the steps accordingly and click on **Save & close** ***(1)***.

   ![](media/2dg84.png)
   
   ![](media/2dg85.png)   
   
1. From the execute tab, Verify the **outcome** of the manual testing. Outcome will be in passed state if the web app worked as expected and vice versa.

   ![](media/2dg86.png)
   
1. Navigate to **chart** ***(1)***, click on **+ New** ***(2)*** and select **+ New test case chart** ***(3)***.

   ![](media/2dg87.png)
   
1. In the Configure chart pop up, select **Bar** ***(1)*** as chart type, **Activated By** ***(2)*** for Group by optiom, and click on **OK** ***(3)***.

   ![](media/2dg88.png)              
   
1. You'll be able to visualize the chart. You can explore more by making changes in the chart, by running multiple test cycles.

   ![](media/2dg89.png)      

1. Click on the **Next** button present in the bottom-right corner of this lab guide.
   
