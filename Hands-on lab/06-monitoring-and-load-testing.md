## Exercise 6: Monitoring and Load Testing (Optional)

In this exercise, we will add monitoring and logging to gain insight on the application usage in the cloud. Then create Azure load testing which is a fully managed load-testing service that enables you to generate high-scale load. The service simulates traffic for your applications, regardless of where they're hosted. Developers, testers, and quality assurance (QA) engineers can use it to optimize application performance, scalability, or capacity. We will also explore Azure Chaos Studio that helps you measure, understand, and improve your cloud application and service resilience.

### Task 1: Set up Application Insights

1. Open the `deploy-appinsights.ps1` PowerShell script in the `C:\Workspaces\lab\mcw-continuous-delivery-lab-files\infrastructure` folder of your lab files GitHub repository and replace studentprefix value with **<inject key="Deploymentid" />** on the first line.

    ```pwsh
    $studentsuffix = "Your 3 letter abbreviation here"                                  # <-- Modify this
    $resourcegroupName = "fabmedical-rg-" + $studentsuffix
    $location1 = "westeurope"
    $appInsights = "fabmedicalai-" + $studentsuffix
    ```

2. Navigate back to the PowerShell terminal on visual studio and run the below mentioned command:

     ```
     cd C:\Workspaces\lab\mcw-continuous-delivery-lab-files\infrastructure
    ./deploy-appinsights.ps1
    ```
    
3. Now save the `AI Instrumentation Key` specified in the output - we will need it for a later step.

    ```bash
    The installed extension 'application-insights' is in preview.
    AI Instrumentation Key="55cade0c-197e-4489-961c-51e2e6423ea2"
    ```

4. Navigate to the `./content-web` folder in your GitHub lab files repository by running the below mentioned command.

   ```
   cd ..
   cd .\content-web
   ```
   
5. Now execute the following command to install JavaScript support for Application Insights via NPM to the web application frontend.

    ```bash
    npm install applicationinsights --save
    ```

6. Modify the file `./content-web/app.js` to reflect the following to add and configure Application Insights for the web application frontend in the local folder.

    ```js
    const express = require('express');
    const http = require('http');
    const path = require('path');
    const request = require('request');

    const app = express();

    const appInsights = require("applicationinsights");         // <-- Add these lines here
    appInsights.setup("55cade0c-197e-4489-961c-51e2e6423ea2");  // <-- Make sure AI Inst. Key matches
    appInsights.start();                                        // <-- key from step 2.

    app.use(express.static(path.join(__dirname, 'dist/content-web')));
    const contentApiUrl = process.env.CONTENT_API_URL || "http://localhost:3001";

    ...
    ```

7. Add and commit changes to your GitHub lab-files repository. From the root of the repository, execute the following:

    ```pwsh
    git add .
    git commit -m "Added Application Insights"
    git push
    ```

8. Wait for the GitHub Actions for your lab files repository to complete before executing the next step.

     ![](media/update8.png) 

9. Redeploy the web application by running the below commands:

    ```
    cd C:\Workspaces\lab\mcw-continuous-delivery-lab-files\infrastructure
    ./deploy-webapp.ps1
    ```
    
10. Visit the deployed website and check Application Insights in the Azure Portal to see instrumentation data.

    >**Note:** It can take upto 24 hours to get the data and logs loaded in Azure Application Insights. You can skip this step and proceed with the next tasks.

## Task 2: Set up Load Testing

In this task you'll create **Azure Load Testing** instance and run a test using Jmeter file.

1. In the Azure Portal on **Search resources, services, and docs** search and select **Azure Load Testing**.

    ![](media/Ex6-T1-S1.png)

2. On the **Azure Load Testing** page click on **+ Create**.
   
    ![](media/Ex6-T1-S2.png)
      
3.  On the **Creat a load testing resource** screen provide the following values and click **Review + create**.

    - Subscription(1): Your Azure subscription for this lab from the drop-down
    - Resource Group(2): fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />
    - Name: fabmedical_LT_<inject key="DeploymentID" enableCopy="false" />
    - Region: Leave default
    
     ![](media/Ex6-T1-S3.1.png)
 
4. Review the deatils you provided, once the validation is successful click on **Create**.
        
     ![](media/Ex6-T1-S4.png)

5.  Click on **Go to resource** on **Your deployment is completed** page.

     ![](media/Ex6-T1-S5.png)

6.  On the left, select **Tests (1)** and click on **+ Create (2)** and select **Upload a JMeter script (3)**.

     ![](media/Ex6-T1-S6.1.png)

7.  On **Create test** page under basic tab provide the **Test name** as `Demo-test` **(1)** and for **Test discription** enter `Demo Load Testing` **(2)**  then click **Next:Test plan >** **(3)**.

     ![](media/Ex6-T1-S7.png)

8. On your lab-vm navigate to **test.jmx** file and open using **Visual Studio Code**. In line 33 replace **Enter_your_end_point_URL** with the URL of **fabmedical-web-<inject key="DeploymentID" enableCopy="false" />**.
  
     > **Note**: Your end point URL should look similar to this **fabmedical-web-<inject key="DeploymentID" enableCopy="false" />.azurewebsites.net**.
  
     ![](media/Ex6-T1-S8.png)
       
9. Next on the **Test plan** tab click on the file icon **(1)** and select **test.jmx (3)** file and select **Upload (3)**.
    
     ![](media/Ex6-T1-S9.1.png)

10. Once the file has been uploaded click on **Review + create**.

     ![](media/Ex6-T1-S10.png)

11. Once the test run is completed you will be able to see **Client-side metrics**. Explore the given metrics output.

     ![](media/Ex6-T1-S11.png)
     
## Task 3: Explore Chaos Studio

In this task you will add **Targets** and create an **Expirement** on **Azure Chaos Studio** to check the resilience of the web appliccation that we created by adding  real faults and observe how our applications respond to real-world disruptions.

1.  On the Azure portal navigate to the **CosmoDB** instance **fabmedical-cdb-<inject key="DeploymentID" enableCopy="false" />**, on the overview page note down the second **Read Locations** we will require this the further steps. 
  
    > **Note:** Notice there are two regions present in both **Read Locations** and **Write Locations** the primary region is where the resource is deployed and running, and the secondary region is the backup region. When performing the Chaos experiment, we will observe that the cosmos DB instance will run undisturbed despite adding fault. This is because the primary region is being replaced by the secondary or the backup region.
     
      
     ![](media/Note-1.1.png)

2.  On **Search resources, services, and docs** search and select **Azure Chaos Studio**.
      
      ![](media/Ex6-T2-S1.png)

2. In the **Azure Chaos Studio** select **Targets** on the left menu.

      ![](media/Ex6-T2-S2.png)
      
 3. Select **fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />** resource group from the drop-down.
 
       ![](media/Ex6-T2-S3.png)
     
 4. Click on the **fabmedical-cdb-<inject key="DeploymentID" enableCopy="false" />** **Cosmos DB** instance and form the drop-down for **Enable Targets** choose **Enable service-direct targets (All resources)**.

     ![](media/Ex6-T2-S4.png)
     
 5. Once the target is enabled, select **Expirements** on the left and click **+Create**.
 
     ![](media/Ex6-T2-S5.1.png)
 
 6. On **Create an experiment** page under **Basics** tab provide the following values and select **Next:Experiment designer>** (4).
 
    - Subscription: Your Azure subscription for this lab from the drop-down
    - Resource Group: fabmedical-rg-<inject key="DeploymentID" enableCopy="false" /> (1)
    - Name: fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" /> (2)
    - Region: Leave default (3)
 
     ![](media/Ex6-T2-S6.3.png)
 
 7. On the **Experiment designer** page select **+ Add action** and choose **Add fault**.

      ![](media/Ex6-T2-S7.1.png)
 
 8. On the **Add fault** page, select the following and select **Next:Target resources>** (4).
   
     - Faults: CosmosDB Failover (1)
     - Duration (minutes): 5 (2)
     - Read region: Select the **Read Locations** you noted down in **Step-1** (3)
     
      ![](media/Ex6-T2-S8.1.png)
       
      
 
  9. On the  **Target resources** select the **CosmoDB** instance and **Add**.
  
       ![](media/Ex6-T2-S9.1.png)
  
  10. Click on **Review + create**.
  
        ![](media/Ex6-T2-S10.png)
   
  11. On the **Review + create** click on **Create**.
  
       ![](media/Ex6-T2-S11.png)
  
  12. Navigate back to the **CosmosDB** instance and select **Access control (IAM)**, click on **+ Add** select **Add role assignment**. 
  
       ![](media/Ex6-T2-S12.png)
  
  13. In the **Add role assignment page** under **Role** tab  select **Owner** and select **Next**.
  
       ![](media/Ex6-T2-S13.png)
  
  14. Next on the **Members** tab select **Managed identity (1)**  for **Assign access to** , click on **+ Selected members (2)**  on the **Select managed identities** choose **Chaos Experiment (3)** for **Managed identity** select the experiment **fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" /> (4)** click on **Select (5)**.  
   
      ![](media/Ex6-T2-S14.1.png)
  
  15. Click on **Review + assign**. 
   
      ![](media/Ex6-T2-S15.1.png)
      
  16. On the Azure portal navigate back to the Chaos experiment you created **fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" />** and click on **Start**.
  
      ![](media/Ex6-T2-S16.1.png)
 
 17. Select **Ok** for **Start this experiment pop-up**.

       ![](media/Ex6-T2-S17.png)
       
 18. Once the experiment status is **Success** click on **Details** to view the run preview.
 
      ![](media/Ex6-T2-S18.png)
 
 19. On the **Details** preview page select **Action** and view the complete detail of the run on **Fault details** under **Successful targets**.
 
        ![](media/Ex6-T2-S19.png)

 20. Navigate to **fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />** resource group and open application insights **fabmedicalai-<inject key="DeploymentID" enableCopy="false" />**. On the app insights overview page click on **Availability tile**.
 
 
 
 21. Observe the availability of the application, after adding the **CosmosDB Failover**.
