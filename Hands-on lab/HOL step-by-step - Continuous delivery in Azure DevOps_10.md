## Exercise 6: Setup a pull request policy, create a task branch and submit a pull request

Duration: 30 Minutes

In this exercise, you will first set up a pull request policy for the master branch, then create a short-lived task branch.  In this branch you will make a small code change, commit, push the code, and finally, submit a pull request with validation builds. 

Then, you will merge the pull request into the master branch, triggering an automated build and release of your application.  For this exercise, you will use Azure DevOps workflow to complete the tasks, but keep in mind this same process could be performed locally using the Azure Command Line Interface (CLI), or an IDE of your choice.

### Task 1: Set up a pull request policy

1.  Create a work item to associate to a pull request.

    For this task, you will be creating a new work item that simulates having a task for the developer to complete that will be eventually be associated to a pull request.  

    On the left navigation, select **Boards**, then use the green plus symbol in the `New` column to add a new work item.  Make sure to create the new work item as a `Product Backlog Item`.  

    >**Note**: Instead of `Product Backlog Item`, you may see `User Story` or `TODO`, depending on what methodology you chose when you setup your organization (such as Agile, Scrum, or CMMI).    

    ![Screen showing how to use the navigation to create a new work item in the Azure Boards.](images/stepbystep/media/image1036_01.png "Creating a new work item for tracking developer work")    

    In the dialog that appears, enter the following text:  

    ```  
    Fix the navigation on the main page home link.  Currently redirects to Privacy.
    ```  

    Save the work item so that it will be assigned a valid number and be ready to assign to the next pull request (created in a future exercise).   

    ![Screen showing the created work item.](images/stepbystep/media/image1036_02.png "Screen that shows the created work item")  

    >**Note**: Your number will almost certainly be different than mine.  

2.  On left navigation, select **Repos** and select **Branches** to view branches associated with your repo.  For now there is only the master branch.   Select the ellipsis for the master branch and select **Branch policies**.

    ![Screen showing the Azure DevOps Branches screen indicating the selection of the Branches link on the far left, followed by selecting the ellipsis next to the master branch and choosing branch policies from the menu.](images/stepbystep/media/image1036.png "Selecting Branch Policy")  

3.  Enable the policy by checking **Check for linked work items** (1) and **Check for comment resolution** (2).

    ![Screen showing the branch policies for master screen with Check for linked work items and check for comment resolution checked and the add button for branch policy highlighted.](images/stepbystep/media/image1037.png "Configuring Branch Policy")
    
    Let's unpack what these configurations do:

    The first check, *Check for linked work items* enables the build policy to require a work item to be included with a pull request.  The work item may be added with one of the commits, or added directly to the pull request.

    >**Note**: It is recommended to enable this setting.  If you *do* enable this then you also must add a work item in your process below with the code changes in this task set.  You can ignore this setting for the workshop if you don't want to add a work item.

    The second check. *Check for comment resolution* ensures comments applied to this pull request during the peer review phase require resolution.

4.  Now select **+** (3) to add the build policy.  This will enable the build to run when a pull request is created.  In the *Add build policy* panel, choose the correct **Build pipeline** and add a **Display name** and select **Save**.   

    ![Screen showing the Add Build Policy panel with the Build pipeline and Display Name values added, and Display Name and Save button highlighted.](images/stepbystep/media/image1038.png "Add Build Policy")

    You should see your new configured branch policy right below the Branch Policies section like this:

    ![Screen showing build validation detail.](images/stepbystep/media/image1039.png "Build Validation")

### Task 2: Create a new branch

1. From left navigation **Repos**, choose **Branches** to show the Branches view.  Select **New branch** in the upper right corner to create a new branch from master: 

    ![Screen showing configured branches with New branch button highlighted.](images/stepbystep/media/image1040.png "Branches View")

2. In the **Create a branch** panel, enter a name for the new branch (e.g. **new-heading**). In the *Based on* field, be sure **master** is selected.

    ![Screen showing, Name and Base highlighted along with the Create button.](images/stepbystep/media/image107.png "Create a Branch")

3. Select the **Create** button.

### Task 3: Make a code change to the task branch

1.  From the **Branches** view, select your newly created branch, this will navigate to a *Files* view showing all  files for this branch.

    ![Screen showing configured branches with the new-heading branch highlighted.](images/stepbystep/media/image1041.png "Branches View - New Branch")

2. You will use this view to make a change to a source file from the web application we have been deploying to your 3 environments in earlier steps.  

    ![Screen showing Azure DevOps Branch source explorer with file detail view.](images/stepbystep/media/image1042.png "Branch Source Explorer - File Details")
    
    Under the *tailspintoysweb* folder, select the **ClientApp** folder, and expand and select the **src** folder.  

3. Next expand the **app** folder then expand the **home** folder.  In this folder, select the **home.component.html** file.  The editor to the right displays the contents of this file.   Now, select **Edit** button on the top right of the screen to begin editing the page.

    ![Screen showing Azure DevOps Branch source explorer with target file highlighted and code editor view enabled.](images/stepbystep/media/image1043.png "Source File Detail")
    
4. Replace the text ```<h1>Welcome to Tailspin Toys v1!</h1>``` on *line 1* with the following:

    ```
    <h1>Welcome to Tailspin Toys v2!</h1>
    ```
    
5.  Now that you've completed the code change, select the **Commit** button on the top right side of the screen.

    ![Screen showing editor with line 1 code change and Commit button highlighted.](images/stepbystep/media/image110.png "Repo Code Editor")

    This will present the Commit panel where you can enter a comment; one will automatically be filled in for you. Select the **Commit** button.

    ![On the popup, the Commit button is highlighted.](images/stepbystep/media/image111.png "Commit Confirmation")

### Task 4: Submit a pull request

1. Locate and select the **Create a pull request** button.

    ![On the screen, Create a pull request is highlighted.](images/stepbystep/media/image112.png "Create a pull request")

2. This brings up the *New Pull Request* page. It shows we are submitting a request to merge code from our **new-heading** branch into the **master** branch. You have the option to change the *Title* and *Description* fields. 
    
    For the **Reviewers** field, type **Tailspin** and select **[TailspinToys]\TailspinToys Team** from the search results to assign a review to the TailspinToys Team (which you are a member of).  
    
    A member of this team must review the pull request before it can be merged and the details for the code change are included in the middle of the view.

    ![On the screen, New pull request panel is shown with create button highlighted.](images/stepbystep/media/image1044.png "New Pull Request")

3. Select the **Create** to submit the pull request.

### Task 5: Approve and complete a pull request

Typically, the next few steps would be performed by another team member, allowing the code to be peer reviewed. 

However, in this scenario, you will continue as if you are the only developer on the project.  

1.  After submitting the pull request, you are presented with Pull Request review screen. Let's assume all the changes made were acceptable to the review team.  Submitting the pull request results in this view:

    ![Screen showing the updated wull request detail with the Approval button highlighted.](images/stepbystep/media/image1045.png "Pull Request Review - Approve")

    There is a lot of functionality here, but for the purpose of this lab, let's focus on this pull request approval by confirming that the  build is green. 

    >**Note**: If the build is not green, you cannot merge the Pull Request as in step 2-4 below. You are then blocked. If you chose the **Check for linked work items** policy in task 1, you will be blocked until you create and attach a work item to your pull request. You can create a new work item by selecting **Boards** and then **Work items**. Then navigate back here and you can choose the new work item from the dropdown on the right side of the page.

2. Next, select the **Approve** button to approve of the code that was modified submitted as part of the pull request.  Here you can see all required checks succeeded and there are no merge conflicts.  Everything necessary is green! 

   The section below the **Description** notes you approved the pull request and now you can select **Complete** to merge the code from the pull request into the master branch.

    ![Screen showing the updated wull request detail with the Complete button highlighted.](images/stepbystep/media/image1046.png "Pull Request Review - Complete")

3.  On selecting **Complete** in the previous step, a **Complete pull request** panel shows. Here you can add additional comments for the merge activity. 

    ![Screen showing the Complete pull request panel box with Complete associated work items after merging and Delete new-heading after merging checked.  Customize merge commit message is unchecked.  Complete merge button is highlighted.](images/stepbystep/media/image1047.png "Complete Merge for Pull Request")

    By selecting the **Delete new-heading after merging** option, our branch will be deleted after the merge has been completed and this feature keeps your repository clean of old branches help to eliminate the possibility of confusion.

4.  Select the **Complete merge** button.  You will then see a confirmation view of the completed pull request.  

    ![Screen showing the confirmation view of the complete pull request.](images/stepbystep/media/image1048.png "Completed Pull Request")



5.  **Congratulations!** By following the tasks in these exercises, you created a new branch and changed some code in the new branch, submitted a pull request and approved the pull request which resulted in a code merge to the master branch.  

    Because you configured continuous deployment using Azure DevOps Pipelines, an automated build was triggered:

    ![Screen showing recent pipeline runs.   The most recent is related to completion of the pull request.](images/stepbystep/media/image1049.png "Merged Pipeline Runs")

    And deployment to all stages executed immediately after the successful build:

    ![Screen showing most recent pipeline run detail including each of the properly configured stages.](images/stepbystep/media/image1050.png "Merged Pipeline Run Details")

    All stages green!   Nice job!

