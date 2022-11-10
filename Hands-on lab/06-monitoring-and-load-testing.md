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
     
 5. Once the target is enabled, select **Expirements** on the left and click create.
