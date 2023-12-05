# Exercise 3: Azure Boards and Test Plans

Duration: 60 minutes

In this exercise, you'll explore Azure boards and Azure test plans. Azure Boards provides software development teams with the interactive and customizable tools they need to manage their software projects. Azure Test Plans provide rich and powerful tools everyone in the team can use to drive quality and collaboration throughout the development process. The easy-to-use, browser-based test management solution provides all the capabilities required for planned manual testing.

### Task 1: Connect Azure Board with GitHub

In this task, you will connect your Azure DevOps project's board to your GitHub repository using the Azure Boards app for GitHub to support the integration between Azure Boards and GitHub. This app is free for both public and private repositories. You'll also explore work items.

1. In your browser, open Azure DevOps by navigating to the below URL:

    ``` 
    https://dev.azure.com/aiw-devops/
    ```

1. In the Azure DevOps page, click on the **User settings** **(1)** from the top right corner of the page and click on **Preview features** **(2)**.

   ![](media/preview-features.png)

   > **Note:** If you get a sign-in error, then click on the **Sign out and sign with a different account** link and log in with your ODL user's Azure credentials. On the next page, leave the details to default and proceed. You should be logged in to the Azure DevOps organization.

1. In the **Preview features** pop-up, ensure to set the toggle button to **off** for **New Boards Hubs** **(1)** and close the preview features by clicking on **X** **(2)**.
   
   ![](media/new-boards-hubs1.png)

1. In your browser, open GitHub Marketplace by navigating to the below URL:

    ``` 
    https://github.com/marketplace/azure-boards
    ```

    ![The Azure Boards Integration App on GitHub Marketplace that will provide a link between Azure DevOps Boards and GitHub issues.](media/hol-ex1-task1-step1.png "Azure Boards Integration App on GitHub Marketplace")

1. Scroll to the bottom of the page and select `Install it for Free.`

   ![](media/2dg50.png)

**> Note:** If the **Install it for free** button is greyed out, please proceed to the next step.
   
1. On the next page, select **Complete order and begin installation**.

1. Select the lab files repository `aiw-devops-with-github-lab-files` that you created earlier and click on **Install & Authorize**.

   ![](media/ex4-kc-install&auth.png)
    
   >**Note**: If you see the message **You’ve already purchased this on all of your GitHub accounts**, this indicates Azure Boards integration is already used in your account. Follow the below steps.
   
   - Scroll to the top of the Azure Boards Marketplace page and select **grant this app access to your GitHub account**.
   
      ![](media/2dg51.png)
   
   - Select the lab file repository `aiw-devops-with-github-lab-files` that you created earlier and click on **Install & Authorize**.

      ![](media/ex4-kc-install&auth.png)

   - Select the cloudlabs **Email** <inject key="AzureAdUserEmail"></inject>
     
   - Now enter the password and **click** on **Sign in**.

      ![](media/img10.png).
    
1. Select the **aiw-devops (1)** Azure DevOps organization and select the **Contosotraders-<inject key="DeploymentID" enableCopy="false" /> (2)** project, then click on **Continue (3)**

   ![](media/azuredevops.png)

1. When the integration succeeds, you will be taken to the Azure DevOps Board. In the onboarding tutorial, click on **Create** to create an initial issue in the `To Do` column.
   
    >**Note**: Make sure to reduce the screen resolution in your browser window if you are not able to view the **Create** and **Create and link a pull request** options on the onboarding tutorial page.

   ![](media/2dg55.png)
    
1. Now click on **Create and link a pull request** to create a pull request associated with your issue.

   ![After completion of the onboarding tutorial. Two todo confirmation messages displayed.](media/image15.png "Get started and quick tip")

1. Click on **View work item**.

   ![](media/viewworkitem.png)
   
1. Open the new issue that the onboarding tutorial creates and observe the GitHub pull request and comments that are linked to the Azure DevOps board issue.

   ![Linked GitHub items in an Azure DevOps issue in Boards.](media/ex3-t1-8.png "GitHub Pull Request and Comment")

1. In GitHub, browse to the `Pull Requests` tab of the lab files repository created in [Task 1 of the Before the HOL Instructions] and open the pull request that was created in the onboarding tutorial for the Azure Boards Integration App. Note the `AB#1` annotation in the pull request comments - this annotation signals to Azure DevOps that this pull request comment should be linked to Issue #1 in Azure Boards.

   ![Pull request detail in GitHub created by onboarding tutorial in previous steps.](media/ex4-kc-merge.png "Pull Request detail")

1. Select the `Files changed` tab within the pull request detail and observe the change to the README.md associated with this pull request. After reviewing the changes, go back to the `Conversation` tab, select the `Merge pull request` button, and confirm the following prompt to merge the pull request into the `main` branch.

   ![The file changes associated with the pull request.](media/upd-ex4-kc-reviewchanges.png "Pull Request Files Changed tab")

1. In Azure DevOps Boards, find the work item and observe that the issue has been moved to the `Done` column on completion of the pull request.

   ![A work item with a linked GitHub commit illustrating the link between Azure DevOps Boards and GitHub issues.](media/ex4-kc-devops-todo.png "Work Item with a Linked GitHub Commit")   

1. You have successfully linked the GitHub account.
   
### Task 2: Link GitHub Pull requests to Boards items

In this task, you'll make changes in GitHub link a PR to Azure boards using syntax, and monitor the work item.

1. In the Azure Boards tab, click on **New Item** ***(1)***, provide **Update carts** **(2)** as a description and create a new work item by hitting **enter**.

   ![](media/ex4-task2-step1.png)
   
1. After creating a work item, Please note down the Work item ID which will be used in the further steps.

   ![](media/ex4-kc-todo-new1.png)
   
1. Select the **Code** ***(1)*** tab in your GitHub repository, navigate to **aiw-devops-with-github-lab-files/.github/workflows/** ***(2)*** and select **contoso-traders-provisioning-deployment.yml** ***(3)*** file.

   ![](media/2dgn140.png)
   
1. Copy the `#test azure boards` code and paste it into line number 1 of the file. Make sure there are no indentation errors.

   ![](media/2dgn166.png)
   
1. Click on **Commit Changes** ***(1)***, provide the details mentioned below and click on **Propose changes** ***(5)***.

   - Provide `workitem ID Updated` ***(2)*** as title. Make sure to provide the same **Work item ID** that was created in the earlier step in Azure DevOps.
   - Select **Create a new branch for this commit and start a pull request** ***(3)***  and name the new branch as **update carts** ***(4)***.

      ![](media/E3T2S5.png)
   
1. On Open a pull request tab, Click on **Create pull request**.

   ![](media/ex4-create-pr.png)
   
1. Navigate to **Azure Boards**. Open the **work item** ***(1)*** created in the earlier step.

   ![](media/ex4-open-wi.png)

1. Observe that the **Pull request** has been linked to the work item.

   ![](media/ex4-observe-pr.png)
   
1. Navigate back to the GitHub browser tab and select the **Pull requests** tab.

   ![](media/ex4-github-pr.png)
   
1. Open the PR created from **updated carts** branch and select **Merge pull request**.

   ![](media/ex4-mergepr.png)
   
1. Update the description as **fixed AB#{workitemID} updated** and select **confirm merge**.

   ![](media/ex4-confirm-merge.png)
   
1. Navigate back Azure Boards tab and notice that the **work item** has been marked as **done**.

   ![](media/2dgn142.png)
   
## Task 3: Configure Azure Test plan

In this task, you'll set up an Azure test plan and perform manual testing for the application.

1. From the Azure DevOps tab, select **Test plans** from the side blade.

   ![](media/2dg71.png)
   
1. From the Test Plans tab, click on **+ New Test Plan**

   ![](media/2dg72.png)
   
1. In the New Test Plan tab, provide the following details and click on **Create** ***(4)***.

   - Name: **TestPlan-<inject key="DeploymentID" enableCopy="false" />** ***(1)***
   - Area Path: **contosotraders-<inject key="DeploymentID" enableCopy="false" />** ***(2)***
   - Iteration: Leave it to **default** ***(3)***
   
      ![](media/2dgn144.png)   
   
1. From contosotraders-<inject key="DeploymentID" enableCopy="false" /> test plan tab, select **more options** ***(1)*** button, hover over **New Suite** ***(2)***, and select **Static suite** ***(3)***.

   ![](media/2dg109.png)   

1. Create a new suite as **TestSuite-<inject key="DeploymentID" enableCopy="false" />**.

   ![](media/2dg75.png)  
   
1. From the Test plans tab, click on **New Test case**.

   ![](media/2dg76.png)    
   
1. In the New Test Case pop-up, provide the following details and click on **Save & Close** ***(10)***

   - Name: **Validate the web app** ***(1)***
   - Steps:
     - Actions: **Access the Contoso Traders app** ***(2)*** Expected result: **Succeeded** ***(3)***          
     - Actions: **Access the Laptop page** ***(4)*** Expected result: **Succeeded** ***(5)***  
     - Actions: **Access the Controllers page** ***(6)*** Expected result: **Succeeded** ***(7)***
     - Actions: **Access the Desktop page** ***(8)*** Expected result: **Succeeded** ***(9)***

         ![](media/ex4-validate-webapp.png) 

1. From the Test plans tab, navigate to **Execute** ***(1)*** tab, select the **validate the web app** ***(2)*** test point and click on **Run for web app** ***(3)***.

   ![](media/2dg78.png)
   
1. A web-based runner will be opened. Manual testing of the web app can be performed. Keep this page open, we will use the runner in upcoming steps.

   ![](media/ex4-view-webapp.png)
   
1. Navigate to Azure Portal, and click on Resource groups from the Navigate panel to see the resource groups.

   ![](media/2dgn9.png) 
   
1. Select **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** resource group from the list.

   ![](media/2dgn126.png)   
   
1. Select **contoso-traders-ui2<inject key="DeploymentID" enableCopy="false" />** endpoint from the list of resources.

   ![](media/2dgn138.png)   
   
1. Click on **Endpoint hostname**. It'll open a browser tab where you will be visual that the Contoso trader's app has been hosted successfully.

   ![](media/2dgn128.png)   

1. Verify the availability of the web app, Laptop page, Controllers page, and desktop page. Simultaneously using the runner page, perform the testing by marking the steps according to the availability of the web pages and click on **Save & close** ***(1)***.

   ![](media/2dgn167.png)
   
   ![](media/ex4-save&close.png)   
   
1. From the execute tab, Verify the **outcome** of the manual testing. The outcome will be in a passed state if the web app works as expected and vice versa.

   ![](media/ex4-testsuite.png)
   
1. Navigate to **chart** ***(1)***, click on **+ New** ***(2)*** and select **+ New test case chart** ***(3)***.

   ![](media/2dg87.png)
   
1. In the Configure chart pop up, select **Bar** ***(1)*** as chart type, **Activated By** ***(2)*** for Group by option, and click on **OK** ***(3)***.

   ![](media/2dg88.png)              
   
1. You'll be able to visualize the chart. You can explore more by making changes in the chart, and by running multiple test cycles.

   ![](media/ex4-testsuite1.png)      

1. Click on the **Next** button present in the bottom-right corner of this lab guide.

## Summary

In this exercise, you explored the features of Azure boards and configured Azure Test plans for the application.
