## Exercise 6: Monitoring and Load Testing (Optional)

Azure Load Testing Preview is a fully managed load-testing service that enables you to generate high-scale load. The service simulates traffic for your applications, regardless of where they're hosted. Developers, testers, and quality assurance (QA) engineers can use it to optimize application performance, scalability, or capacity.

## Task 1: Set up Load Testing

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
     
## Task 2: Explore Chaos Studio

In this task you will add **Targets** and create an **Expirement** on **Azure Chaos Studio** to check the resilience of the web appliccation that we created by adding  real faults and observe how our applications respond to real-world disruptions.

1. Navigate to Azure portal, on **Search resources, services, and docs** search and select **Azure Chaos Studio**.
      
      ![](media/Ex6-T2-S1.png)

2. In the **Azure Chaos Studio** select **Targets** on the left menu.

      ![](media/Ex6-T2-S2.png)
      
 3. Select **fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />** resource group from the drop-down.
 
       ![](media/Ex6-T2-S3.png)
     
 4. Click on the **fabmedical-cdb-<inject key="DeploymentID" enableCopy="false" />** **Cosmos DB** instance and form the drop-down for **Enable Targets** choose **Enable service-direct targets (All resources)**.

     ![](media/Ex6-T2-S4.png)
     
 5. Once the target is enabled, select **Expirements** on the left and click **+Create**.
 
     ![](media/Ex6-T2-S5.1.png)
 
 6. On **Create an experiment** page under **Basics** tab provide the following values and select **Next:Experiment designer>**.
 
    - Subscription: Your Azure subscription for this lab from the drop-down
    - Resource Group: fabmedical-rg-<inject key="DeploymentID" enableCopy="false" />
    - Name: fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" />
    - Region: Leave default
 
     ![](media/Ex6-T2-S6.2.png)
 
 7. On the **Experiment designer** page select **+ Add action** and choose **Add fault**.

      ![](media/Ex6-T2-S7.1.png)
 
 8. On the **Add fault** page, select the following and select Next: **Target resources**.
   
     - Faults: CosmosDB Failover
     - Duration (minutes): 5
     - Read region: Select the region 
     
      ![](media/Ex6-T2-S8.png)
       
    > **Note:** The **Read region** is available in the overview page of the **CosmoDB** instance. 
        
       ![](media/Note-1.png)
       
 
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
   
      ![](media/Ex6-T2-S14.png)
  
  15. Click on **Review + assign**. 
   
      ![](media/Ex6-T2-S15.png)
      
  16. On the Azure portal navigate back to the Chaos experiment you created **fabmedical-chaos-<inject key="DeploymentID" enableCopy="false" />** and click on **Start**.
  
      ![](media/Ex6-T2-S16.png)
 
 17. Select **Ok** for **Start this experiment pop-up**.

       ![](media/Ex6-T2-S17.png)
