## Exercise 5: Monitoring and Load Testing (Optional)

In this exercise, we will add monitoring and logging to gain insight on the application's usage in the cloud. Then create Azure load testing, which is a fully managed load-testing service that enables you to generate high-scale loads. The service simulates traffic for your applications, regardless of where they're hosted. Developers, testers, and quality assurance (QA) engineers can use it to optimise application performance, scalability, or capacity. We will also explore Azure Chaos Studio, which helps you measure, understand, and improve your cloud application and service resilience.

### Task 1: Monitoring using Application Insights

1. In the Azure Portal, navigate to **Tailwind-<inject key="Deploymentid" />** **(1)** resource group and select the **Application Insights** resource with the name  **tailwind-traders-ai<inject key="Deploymentid" />** **(2)**.

   ![](media/ex6-t1-openai.png)
   
1. From the Overview of **tailwind-traders-ai<inject key="Deploymentid" />** Application Insights resource, you can set the **Show data for last** as per your requirment of monitoring insights.

   ![](media/ex6-t1-set-showdata.png)
   
1. In the first graph, you can see the number of failed requests for the Application access.

   ![](media/ex6-t1-failedrequests.png)
   
1. In the next graph, you can see the average server response time.

   ![](media/ex6-t1-server-response-time.png)
   
1. In the next graph, you can see the number of server requests.

   ![](media/ex6-t1-server-requests.png)
   
1. In the last graph, you can see the average availability.

   ![](media/ex6-t1-availability.png)  
   
## Task 2: Set up Load Testing

In this task, you'll create Azure Load Testing instance and run a test using a JMeter file.

1. In the Azure Portal, navigate to **Tailwind-<inject key="Deploymentid" />** resource group and select the **Container App** resource with the name  **tailwind-traders-carts<inject key="Deploymentid" />**.

1. From the Overview of **tailwind-traders-carts<inject key="Deploymentid" />** **(1)** Container App, copy the **Application Url** **(2)** and paste it in notepad for later use in the task.

   ![](media/ex6-t2-copyappurl.png)

1. In the Azure Portal, navigate to **Tailwind-<inject key="Deploymentid" />** **(1)** resource group and select the **Azure Load Testing** resource with the name  **tailwind-traders-loadtest<inject key="Deploymentid" />** **(2)**.

   ![](media/ex6-open-loadtest.png)

1. On the left hand side pane, select **Tests (1)** and click on **+ Create (2)** and select **Upload a JMeter script (3)**.

   ![](media/ex6-t2-loadtest-create.png)

1. On the **Create test** page, under basic tab provide the **Test name** as `Demo-test` **(1)** and for **Test discription** enter `Demo Load Testing` **(2)**, then click **Next:Test plan >** **(3)**.

   ![](media/Ex6-T1-S7.2.png)

1. On your lab-vm open **File Explorer** and navigate to the following path `C:\Workspaces\lab\aiw-devops-with-github-lab-files\tests\loadtests` **(1)**. Right click on the file named **tailwind-traders-carts.jmx** **(2)** and click on **Open with Code** **(3)**.

   ![](media/ex6-t2-cartsjmx-open.png)

1. In line number 68, replace **${Domain}** with **Application Url** of Container App which you have copied earlier in the task step-2 and save the file. 
 
   ![](media/ex6-t2-cartsjmx.png)
       
1. Next, on the **Test plan** tab, click on the file icon **(1)**, select the **tailwind-traders-carts.jmx **(2)** file from your lab-vm `C:\Workspaces\lab\aiw-devops-with-github-lab-files\tests\loadtests` and select **Upload (3)**.
    
   ![](media/ex6-t2-jmxupload.png)

1. Once the file has completed uploading **(1)**, click on **Review + create (2)**.

   ![](media/ex6-t2-create-test.png)
   
1. Once the validation passed, click on **Create**.

   ![](media/ex6-t2-create-test2.png)  

1. Once the test run is completed, you will be able to see **Client-side metrics**. Explore the given metrics output.

   ![](media/Ex6-T1-S11.png)
     
## Task 3: Explore Chaos Studio

In this task you will add **Targets** and create an **Expirement** on **Azure Chaos Studio** to check the resilience of the web appliccation that we created by adding  real faults and observe how our applications respond to real-world disruptions.

1. Navigate to the **CosmoDB** instance **fabmedical-cdb-<inject key="DeploymentID" enableCopy="false" />** in the Azure portal, on the overview page, take note of the second list of **Read Locations** we will require this the further steps. 
 
   > **Note:** Notice there are two regions present in both **Read Locations** and **Write Locations** the primary region is where the resource is deployed and running, and the secondary region is the backup region. When performing the Chaos experiment, we will observe that the Cosmos DB instance will run undisturbed despite adding a fault. This is because the primary region is being replaced by the secondary or the backup region.
           
   ![](media/Note-1.2.png)

2. In the Azure Portal search for **Azure Chaos Studio (1)** and then click on it from the search results **(2)**.
   
   ![](media/Ex6-T2-S1.1.png)

3. In the **Azure Chaos Studio**, select **Targets** on the left menu.

   ![](media/Ex6-T2-S2.png)
      
4. From the drop-down menu, select **fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />** resource group.
 
   ![](media/Ex6-T2-S3.png)
     
5. Click on the **fabmedical-cdb-<inject key="DeploymentID" enableCopy="false" />** **Cosmos DB** instance and form the drop-down for **Enable Targets (1)** choose **Enable service-direct targets (All resources) (2)**.

   ![](media/Ex6-T2-S4.3.png)
     
6. Once the target is enabled, select **Expirements** on the left and click **+Create**.
 
   ![](media/Ex6-T2-S5.3.png)
 
7. On the **Create an experiment** page, under **Basics** tab provide the following values and select **Next:Experiment designer>** **(5)**.

    - Subscription: select the default subscription **(1)**
    - Resource Group: fabmedical-rg-<inject key="DeploymentID" enableCopy="false" /> **(2)**
    - Name: fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" /> **(3)**
    - Region: Leave it to default **(4)**
 
    ![](media/Ex6-T2-S6.5.png)
 
8. On the **Experiment designer** page select **+ Add action (1)** and choose **Add fault (2)**.

   ![](media/Ex6-T2-S7.3.png)
 
9. On the **Add fault** page, select the following and select **Next:Target resources>** **(4)**.
   
    - Faults: CosmosDB Failover **(1)**
    - Duration (minutes): 5 **(2)**
    - Read region: Select the **Read Locations** you noted down in **Step-1** **(3)**
     
    ![](media/Ex6-T2-S8.3.png)
     
10. On the  **Target resources** select the **CosmoDB** instance and **Add**.
  
    ![](media/Ex6-T2-S9.3.png)
  
11. Click on **Review + create**.
  
    ![](media/Ex6-T2-S10.png)
   
12. On the **Review + create** click on **Create**.
  
    ![](media/Ex6-T2-S11.png)
  
13. Navigate back to the **CosmosDB** instance and select **Access control (IAM) (1)**, click on **+ Add (2)** and select **Add role assignment (3)**. 
  
    ![](media/Ex6-T2-S12.2.png)
  
14. In the **Add role assignment page** under **Role** tab  select **Owner (1)** and select **Next (2)**.
  
    ![](media/Ex6-T2-S13.2.png)
  
15. Next on the **Members** tab select **Managed identity (1)**  for **Assign access to** , click on **+ Selected members (2)**  on the **Select managed identities** choose **Chaos Experiment (3)** for **Managed identity** select the experiment **fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" /> (4)** click on **Select (5)**.  
   
    ![](media/Ex6-T2-S14.2.png)
  
16. Click on **Review + assign**. 
   
    ![](media/Ex6-T2-S15.1.png)
      
17. On the Azure portal navigate back to the Chaos experiment you created **fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" />** and click on **Start**.
  
    ![](media/Ex6-T2-S16.1.png)
 
18. Select **Ok** for **Start this experiment** pop-up.

    ![](media/Ex6-T2-S17.1.png)
       
19. Once the experiment status is **Success** click on **Details** to view the run preview.
 
    ![](media/Ex6-T2-S18.png)
 
20. On the **Details** preview page select **Action (1)** and view the complete detail of the run on **Fault details** under **Successful targets (2)**.
 
    ![](media/Ex6-T2-S19.1.png)

21. Navigate to **fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />** resource group and open application insights **fabmedicalai-<inject key="DeploymentID" enableCopy="false" />**. On the app insights overview page click on **Availability tile**.
 
 
22. Observe the availability of the application, after adding the **CosmosDB Failover**.
