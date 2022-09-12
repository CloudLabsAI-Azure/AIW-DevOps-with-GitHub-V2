## Exercise 2: Create Azure DevOps project and Git Repository

Duration: 15 Minutes

In this exercise, you will create and configure an Azure DevOps account along with an Agile project.

### Task 1: Create Azure DevOps Account

1. Browse to the **Azure DevOps** site at ```https://dev.azure.com```.

2. If you do not already have an account, select the **Start free** button.
    
    ![In this screenshot, a Start free button is shown on the Azure DevOps home page.](images/stepbystep/media/image56.png "Azure DevOps Product Home Page")

3. Authenticate with a Microsoft account.

4. Choose **Continue** to accept the Terms of Service, Privacy Statement, and Code of Conduct.

5. Choose a name for new your project. For the purposes of this scenario, we will use *TailspinToys*. Choose **Private** in the Visibility section so that our project is only visible to those who we specifically grant access. Then, select **+ Create project**.
    
    ![In the Create a project to get started window, TailspinToys is highlighted in the Project name box, Private is highlighted in the Visibility box, and Create project is highlighted at the bottom.](images/stepbystep/media/image57.png "Azure DevOps Create a Project")

6. Once the Project is created, choose the **Repos** menu option in the left-hand navigation.

    ![In the TailspinToys project window, Repos is highlighted in the left-hand navigation.](images/stepbystep/media/image58.png "TailspinToys navigation window")

7. On the *Repos* page for the **TailspinToys** repository and locate the "Push an existing repository from command line" section. Choose the **Copy push commands to clipboard** button to copy the contents of the panel. We're going to use these commands in an upcoming step.

    ![In the "Add some code!" window, URLs appear to clone to your computer or push an existing repository from command line.](images/stepbystep/media/image59.png "TailspinToys is empty. Add some code! window")


### Task 2: Create a Service Connection 

In this Task, you will configure the Azure DevOps with a Service Connection that allows Azure Dev Ops to securely connect to the resource group you just created in Azure.   

**Before continuing, make sure that you are signed in to both the Azure Portal and Azure DevOps using the same Microsoft account**!

1. In Azure DevOps, ensure you are in the project that you just created, and from the bottom corner of the page, select **Project settings**..
    
    ![In left-hand navigation Azure DevOps Project Settings is highlighted.](images/stepbystep/media/image988.png "Azure DevOps Project Settings")

2. Under Pipelines, select **Service connections**.

    ![In the left-hand navigation Service Connections is highlighted.](images/stepbystep/media/image989.png "Azure DevOps Service Connections")

3. If this is your first service connection, you will see the below image and you can select **Create service connection** button to create your first service connection.

    ![In Create First Service Connection Dialog, Create Service Connection is highlighted.](images/stepbystep/media/image990.png "Create Service Connection")
    
    However, if there are existing service connections you will see a view like below, can add a new one by selecting **New Service connection**:

    ![In Service Connection View, New Service Connection is highlighted.](images/stepbystep/media/image991.png "Service Connections View")

    In either case, you will get a **New service connection** panel showing common connection types.   
    
    ![In New Service Connection Panel, Azure Resource Manager is highlighted.](images/stepbystep/media/image992.png "New Service Connection")

4. On this panel, **Select *Azure Resource Manager** and then select **Next**.

    ![In New Service Connection Panel, Service Principal(automatic) radio button is highlighted.](images/stepbystep/media/image993.png "Selecting Service Principal")
   
5. Near the top of the page, select **Service Principal (Automatic)** and select **Next** to view the **New Azure service connection** panel:

    ![In New Service Connection Panel, Subscription(automatic) radio button and Service Connection Text Value are highlighted.](images/stepbystep/media/image994.png "New Azure Service Connection")

    
6. On this panel ensure the following settings:

    **Scope level:**  Subscription

    **Subscription:**	Choose your Azure subscription

    **Resource Group:**	Choose the resource group you created earlier
    
    **Service Connection Name:**	 Enter a string value such as "LabConnection"  so you can find this later. 

    Ensure **Grand access permissions to all pipelines** is checked

    >**Note**: During the Service Connection creation process, you might be prompted to sign into your Microsoft account if Azure DevOps detects it requires authentication. 
    
7. And finally, select **Save**.   
 
    Azure DevOps performs a test connection to verify that it can connect to your Azure subscription. If Azure DevOps can't connect, you have the chance to sign in a second time.

    Now you have a valid service connection!   Azure DevOps will use this to perform deployments in the resource group you created earlier.   

### Task 3: Add the Tailspin Toys source code repository to Azure DevOps

In this Task, you will configure the Git repository for the Azure DevOps instance you just created. Using Git command line tools from Azure Cloud Shell, you will configure the remote repository and then push your source code up to your Azure DevOps repository.

1. Open the **Azure Cloud Shell** to the folder where the Student Files were unzipped (e.g. studentfiles). Then, navigate to the **tailspintoysweb** folder which contains the source code for our web application.

    > **Note**: If this folder doesn't exist ensure you followed the instructions in the 'Before the hands-on lab'.  
    
    If you are using the Azure Cloud Shell you will be prompted for credentials to connect to your Azure DevOps instance when using Git. 
    
    The best way to authenticate is to use a personal access token, (or PAT), configured with scope *Code, Full permissions*. After this configuration, you can then use the PAT as a password (leaving the username empty) when prompted by Git. 

2. Open *Cloud Shell Editor* to this folder by typing: 
   
   ```bash
   code .
   ``` 

   Be sure to include the period '.' after the code command as this instructs the Cloud Shell Editor window to open *in the current directory location*.   Then, press **Enter**. 
   
3. In Azure Cloud Shell, initialize a local Git repository by running the following commands:

    > If a ".git" folder and local repository already exists in the folder, then you will need to delete the ".git" folder first before running the commands below to initialize the Git repository.

    ```bash
    git init
    git add . 
    git commit -m "initial checkin"
    ```

4. Paste the first command you copied from Azure DevOps. It will resemble the command below:
    
    ```bash
    git remote add origin https://<your-org>@dev.azure.com/<your-org>/TailspinToys/_git/TailspinToys
    git push -u origin --all
    ```  

5. In case the *Password for 'https://\<your-org>@dev.azure.com':* prompt appears, follow the next steps to generate a PAT (Personal Access Token) for your Azure DevOps organization. Otherwise, skip to step 13.
    
    > **Note**: **Do Not Close Azure Cloud Shell**. Use a different browser tab for the steps for creating a new PAT token.  Also, these PAT configuration steps are also useful when using a multi-factored protected user account with Azure DevOps.

6. In Azure DevOps, choose on the second to last icon on the top menu in the left-hand side of the screen, representing a user and a small gear icon.

7. From the context menu, choose **Personal access tokens**.

    ![Selecting the player settings icon in the top menu bar](images/stepbystep/media/image132.png "Personal access tokens menu option")

8. If the *Create a new personal access token* panel has appeared, skip to the next step. Otherwise, select the **+ New Token** button.

    ![Forcing the 'Create a new personal access token' to appear](images/stepbystep/media/image133.png "New Personal Access Token")

9. In the *Create a new personal access token* panel, type in a descriptive name for the new token, and from the *Code* section, choose **Full** and **Status**.

    ![Creating a new PAT (Personal Access Token) in Azure Devops](images/stepbystep/media/image134.png "Create a Personal Access Token")

10. In the *Create a new personal access token* panel, select the **Create** button.

11. From the success confirmation panel, select the **Copy to clipboard** button to copy the newly created PAT token to clipboard.

    ![Copying the newly created PAT token to the clipboard](images/stepbystep/media/image135.png "PAT Success confirmation page")

12. In Azure Cloud Shell, paste the PAT token and press **Enter**.   Git will push the contents of your local repository in Azure Cloud Shell to your new Azure DevOps project repository.  

    ![The cloud terminal is shown in this screen to highlight that the PAT is not shown when you paste it in the cloud shell.  Even so, using the PAT as your password allows you to push the code to your Azure DevOps Repo](images/stepbystep/media/image1064.png "PAT is not shown after pasting, but the cloud shell does use it")  

13. Navigate to the Repos > Files page which shows the files in the repository. You may need to refresh the page to see the updated files. Your source code is now appearing in Azure DevOps.

    ![The newly created files show up in Repos > Files section.](images/stepbystep/media/image136.png "Azure DevOps Repo File View")

14. In the files for your repo, navigate to the folder `Client App -> src`.  If there is a file named **package-lock.json**, hover on the file, and from the context menu, choose **Delete**.

    ![The context menu shows up on the package-lock.json file, from the ClientApp directory.](images/stepbystep/media/image137.png "Deleting package-lock.json")  

    >**Note**: If there is no package.json file then you don't need to do anything else here.  You can skip to Exercise 3. 

15. Confirm the deletion, and when the commit panel shows, validate the commit message and choose **Commit**.

