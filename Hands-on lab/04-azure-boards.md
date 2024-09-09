# Exercise 3: Azure Boards and Test Plans

Duration: 60 minutes

In this exercise, you'll explore Azure boards and Azure test plans. Azure Boards provides software development teams with the interactive and customizable tools they need to manage their software projects. Azure Test Plans provides rich and powerful tools everyone in the team can use to drive quality and collaboration throughout the development process. The easy-to-use, browser-based test management solution provides all the capabilities required for planned manual testing.

### Task 1: Connect Azure Board with GitHub

In this task, you will connect your Azure DevOps project's board to your GitHub repository using the Azure Boards app for GitHub to support the integration between Azure Boards and GitHub. This app is free for both public and private repositories. You'll also explore work items.

1. In your browser open Azure DevOps by navigating to the below URL:

   ```
   https://dev.azure.com/aiw-devops/
   ```

2. In the Azure DevOps page click on the **User settings** **(1)** from the top right corner of the page and click on **Preview features** **(2)**.

   ![](media/preview-features.png)

   > **Note:** If you get a sign-in error, then click on **Sign out and sign with a different account** link and login with your ODL user's Azure credentials. In the next page, leave the details to default and proceed. You should be logged in to the Azure DevOps organization.

3. In the **Preview features** pop-up, ensure to set the toggle button to **off** for **New Boards Hubs** **(1)** and close the preview features by clicking on **X** 
   **(2)**.

   ![](media/new-boards-hubs1.png)

4. In your browser open GitHub Marketplace by navigating to the below URL:

   ```
   https://github.com/marketplace/azure-boards
   ```

   ![The Azure Boards Integration App on GitHub Marketplace that will provide a link between Azure DevOps Boards and GitHub issues.](media/hol-ex1-task1-step1.png "Azure Boards Integration App on GitHub Marketplace")

5. Scroll to the bottom of the page and select `Install it for Free.`

   ![](media/2dg50.png)

6. In review your order page enter the billing information and click on **save**

   > **Note:** If the **Install it for free** button is greyed out  with the message **You’ve already purchased this on all of your GitHub accounts** this indicates Azure Boards integration is already used in your account follow the below steps and please proceed from step number 8.

     - Scroll to the top of the Azure Boards Marketplace page and click on the elipsis and choose configure account access.

       ![](media/l1.png)

   - In the next page, click on **Configure**.

     ![](media/l2.png)

   - Scroll down and select the lab files repository `aiw-devops-with-github-lab-files`which you created earlier from the dropdown  and click on **Save**.

      ![](media/l3.png)

   - Select the cloudlabs **Email** <inject key="AzureAdUserEmail"></inject>
   - Now enter the password and **click** on **Sign in**.

   ![](media/img10.png).

7. On the next page, select **Complete order and begin installation**.

8. Select the lab files repository `aiw-devops-with-github-lab-files` which you created earlier and click on **Install & Authorize**.

   ![](media/ex4-kc-install&auth.png)


9. Select the **aiw-devops (1)** Azure DevOps organization and select the **Contosotraders-<inject key="DeploymentID" enableCopy="false" /> (2)** project then click 
   on **Continue (3)**

   ![](media/azuredevops.png)

10. When the integration succeeds, you will be taken to the Azure DevOps Board. In the onboarding tutorial click on **Create** to create an initial Issue in the `To 
   Do` Column.

   > **Note**: Make sure to reduce the screen resolution in your browser window if you are not able to view the **Create** and **Create and link a pull request** 
    options in the onboarding tutorial page.

   ![](media/2dg55.png)

11. Now click on **Create and link a pull request** to create a pull request associated with your Issue.

   ![After completion of the onboarding tutorial. Two todo confirmation messages displayed.](media/image15.png "Get started and quick tip")

12. Click on **View work item**.

   ![](media/viewworkitem.png)

13. Open the new Issue that the onboarding tutorial creates and observe the GitHub pull request and comments that are linked to the Azure DevOps board Issue.

   ![Linked GitHub items in an Azure DevOps issue in Boards.](media/ex3-t1-8.png "GitHub Pull Request and Comment")

14. In GitHub, browse to the `Pull Requests` tab of the lab files repository created in [Task 1 of the Before the HOL Instructions] and open the pull request that 
    was created in the onboarding tutorial for the Azure Boards Integration App. Note the `AB#1` annotation in the pull request comments - this annotation signals to 
    Azure DevOps that this pull request comment should be linked to Issue #1 in Azure Boards.

   ![Pull request detail in GitHub created by onboarding tutorial in previous steps.](media/ex4-kc-merge.png "Pull Request detail")

15. Select the `Files changed` tab within the pull request detail and observe the change to the README.md associated with this pull request. After reviewing the 
    changes, go back to the `Conversation` tab, select the `Merge pull request` button, and confirm the following prompt to merge the pull request into the `main` 
    branch.

   ![The file changes associated with the pull request.](media/upd-ex4-kc-reviewchanges.png "Pull Request Files Changed tab")

16. In Azure DevOps Boards, find the work item and observe that the issue has been moved to the `Done` column on completion of the pull request.

   ![A work item with a linked GitHub commit illustrating the link between Azure DevOps Boards and GitHub issues.](media/ex4-kc-devops-todo.png "Work Item with a Linked GitHub Commit")

17. You have successfully linked the GitHub account.

### Task 2: Link GitHub Pull requests to Boards items

In this task, you'll make changes in GitHub link a PR to Azure boards using syntax, and monitor the work item.

1. In the Azure Boards tab, click on **New Item** **_(1)_**, provide **Update carts** **(2)** as a description and create a new work item by hitting **enter**.

   ![](media/ex4-task2-step1.png)

1. After creating a work item, Please note down the Work item ID which will be used in the further steps.

   ![](media/ex4-kc-todo-new1.png)

1. Select the **Code** **_(1)_** tab in your GitHub repository, navigate to **aiw-devops-with-github-lab-files/.github/workflows/** **_(2)_** and select **contoso-traders-provisioning-deployment.yml** **_(3)_** file.

   ![](media/2dgn140.png)

1. Copy `#test azure boards` code and paste it into line number 1 of the file. Make sure there are no indentation errors.

   ![](media/2dgn166.png)

1. Click on **Commit Changes** **_(1)_**, provide the details mentioned below and click on **Propose changes** **_(5)_**.

   - Provide `workitem ID Updated` **_(2)_** as title. Make sure to provide the same **Work item ID** that was created in the earlier step in Azure DevOps.
   - Select **Create a new branch for this commit and start a pull request** **_(3)_** and name the new branch as **update carts** **_(4)_**.

   ![](media/E3T2S5.png)

1. On Open a pull request tab, Click on **Create pull request**

   ![](media/ex4-create-pr.png)

1. Navigate to **Azure Boards**. Open the **work item** **_(1)_** created in the earlier step.

   ![](media/ex4-open-wi.png)

1. Observe that the **Pull request** has been linked to the work item.

   ![](media/ex4-observe-pr.png)

1. Navigate back to the GitHub browser tab and select **Pull requests** tab.

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

1. From the Test plans tab, click on **+ New Test Plan**

   ![](media/2dg72.png)

1. In the New Test Plan tab, provide the following details and click on **Create** **_(4)_**.

   - Name: **TestPlan-<inject key="DeploymentID" enableCopy="false" />** **_(1)_**
   - Area Path: **contosotraders-<inject key="DeploymentID" enableCopy="false" />** **_(2)_**
   - Iteration: Leave it to **default** **_(3)_**

   ![](media/2dgn144.png)

1. From contosotraders-<inject key="DeploymentID" enableCopy="false" /> test plan tab, select **more options** **_(1)_** button, hover over **New Suite** **_(2)_**, and select **Static suite** **_(3)_**.

   ![](media/2dg109.png)

1. Create a new suite as **TestSuite-<inject key="DeploymentID" enableCopy="false" />**.

   ![](media/2dg75.png)

1. From the Test plans tab, click on **New Test case**.

   ![](media/2dg76.png)

1. In the New Test Case pop-up, provide the following details and click on **Save & Close** **_(10)_**

   - Name: **Validate the web app** **_(1)_**
   - Steps:
     - 1. Actions: **Access the Contoso Traders app** **_(2)_** Expected result: **Succeeded** **_(3)_**
     - 2. Actions: **Access the Laptop page** **_(4)_** Expected result: **Succeeded** **_(5)_**
     - 3. Actions: **Access the Controllers page** **_(6)_** Expected result: **Succeeded** **_(7)_**
     - 4. Actions: **Access the Desktop page** **_(8)_** Expected result: **Succeeded** **_(9)_**

   ![](media/ex4-validate-webapp.png)

1. From the Test plans tab, navigate to **Execute** **_(1)_** tab, select the **validate the web app** **_(2)_** test point and click on **Run for web application** **_(3)_**.

   ![](media/2dg78.png)

1. A web-based runner will be opened. Manual testing of the web app can be performed. Keep this page open, we will use the runner in upcoming steps.

   ![](media/ex4-view-webapp.png)

1. Navigate to Azure Portal, and click on Resource groups from the Navigate panel to see the resource groups.

   ![](media/2dgn9.png)

1. Select **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** resource group from the list.

   ![](media/2dgn126.png)

1. Select **contoso-traders-ui2<inject key="DeploymentID" enableCopy="false" />** endpoint from the list of resources.

   ![](media/2dgn138.png)

1. Click on **Endpoint hostname**. It'll open a browser tab where you will be visual that the contoso traders app has been hosted successfully.

   ![](media/2dgn128.png)

1. Verify the availability of the web app, Laptops page, Controllers page, and Desktops page. Simultaneously using the runner page, perform the testing by marking the steps according to the availability of the web pages and click on **Save & close** **_(1)_**.

   ![](media/2dgn167.png)

   ![](media/ex4-save&close.png)

1. From the execute tab, Verify the **outcome** of the manual testing. The outcome will be in a passed state if the web app worked as expected and vice versa.

   ![](media/ex4-testsuite.png)

1. Navigate to **chart** **_(1)_**, click on **+ New** **_(2)_** and select **+ New test case chart** **_(3)_**.

   ![](media/2dg87.png)

1. In the Configure chart pop up, select **Bar** **_(1)_** as chart type, **Activated By** **_(2)_** for Group by option, and click on **OK** **_(3)_**.

   ![](media/2dg88.png)

1. You'll be able to visualize the chart. You can explore more by making changes in the chart, and by running multiple test cycles.

   ![](media/ex4-testsuite1.png)

1. Click on the **Next** button present in the bottom-right corner of this lab guide.

  <validation step="33638c78-3fac-4987-accd-3df1a2e578f2" />

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
 
> - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at labs-support@spektrasystems.com.



## Summary

In this exercise, you explored the features of Azure boards and configured Azure Test plans for the application.
