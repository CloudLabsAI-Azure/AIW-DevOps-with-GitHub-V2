# Exercise 5: Monitoring and Load Testing (Optional)

Duration: 70 minutes

In this exercise, we will add monitoring and logging to gain insight on the application's usage in the cloud. Then create Azure load testing, which is a fully managed load-testing service that enables you to generate high-scale loads. The service simulates traffic for your applications, regardless of where they're hosted. Developers, testers, and quality assurance (QA) engineers can use it to optimise application performance, scalability, or capacity. We will also explore Azure Chaos Studio, which helps you measure, understand, and improve your cloud application and service resilience.

### Task 1: Monitoring using Application Insights

1. In the Azure Portal, navigate to **contoso-traders-<inject key="Deploymentid" enableCopy="false" />** **(1)** resource group and select the **Application Insights** resource with the name  **contoso-traders-ai<inject key="Deploymentid" />** **(2)**.

   ![](media/upd-ex6-t1-openai.png)
   
1. From the Overview of **contoso-traders-ai<inject key="Deploymentid"  enableCopy="false" />** Application Insights resource, you can set the **Show data for last** as per your requirement of monitoring insights.

   ![](media/upd-ex6-t1-set-showdata.png)
   
1. In the first graph, you can see the number of failed requests for the Application access.

   ![](media/upd-ex6-t1-failedrequests.png)
   
1. In the next graph, you can see the average server response time.

   ![](media/upd-ex6-t1-server-response-time.png)
   
1. In the next graph, you can see the number of server requests.

   ![](media/upd-ex6-t1-server-requests.png)
   
1. In the last graph, you can see the average availability.

   ![](media/upd-ex6-t1-availability.png)  
   
## Task 2: Set up Load Testing

In this task, you'll create an Azure Load Testing instance and run a test using a JMeter file.

1. In the Azure Portal, navigate to **contoso-traders-<inject key="Deploymentid" enableCopy="false" />** resource group and select the **Endpoint** resource with the name  **contoso-traders-ui2<inject key="Deploymentid" />**.

   ![](media/dglt1.jpg)

1. From the overview of **contoso-traders-ui2<inject key="Deploymentid" enableCopy="false" />** endpoint, copy the **Endpoint hostname** **(2)** and paste it into the notepad for later use in the task.

   ![](media/dglt2.jpg)

1. In the Azure Portal, navigate to **contoso-traders-<inject key="Deploymentid" enableCopy="false" />** **(1)** resource group and select the **Azure Load Testing** resource with the name  **contoso-traders-loadtest<inject key="Deploymentid" />** **(2)**.

   ![](media/upd-2dgn117.png)
   
1. On the left hand side pane, select **Tests** ***(1)*** and click on **+ Create** ***(2)*** and select **Create a quick test** ***(3)***.

   ![](media/2dgn96.png)

1. On the **Create test** page, under basic tab paste the **Endpoint URL** as Test URL ***(1)*** and  leave everything as default, then click **Run Test** ***(2)***.

   ![](media/ex6-task2-step5.png)

1. The test run will start running and once the test run is completed, you will be able to see **Client-side metrics**. Explore the given metrics output.

   ![](media/dglt4.jpg)
   
   **Note**: In case, the test fails due to `The test was stopped due to a high error rate. Check your script and try again. In case the issue persists, raise a ticket with a support error. This is expected as sometimes the load on the application exceeds the defined throughput.
     
## Task 3: Explore Chaos Studio

In this task you will add **Targets** and create an **Experiment** on **Azure Chaos Studio** to check the resilience of the web application that we created by adding  real faults and observe how our applications respond to real-world disruptions.

1. In the Azure Portal search for **Azure Chaos Studio (1)** and then click on it from the search results **(2)**.
   
   ![](media/Ex6-T2-S1.1.png)

1. In the **Azure Chaos Studio**, select **Targets** on the left menu.

   ![](media/Ex6-T2-S2.png)
      
1. From the drop-down menu, select **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** resource group.
 
   ![](media/2dgn122.1.png)
     
1. Click on the **contoso-traders-aks<inject key="DeploymentID" enableCopy="false" />** **(1)** **Kubernetes service** instance and form the drop-down for **Enable Targets** **(2)** choose **Enable service-direct targets (All resources)** **(3)**.

   ![](media/2dgn99.png)
     
1. Click on **Review + Enable**.

   ![](media/reviewenable.png)

1. Then click on **Enable** to Enable service direct targets. 
   
   ![](media/enable.png)

1. Wait for the deployment to be completed.  

1. In the Azure Portal search for **Azure Chaos Studio** ***(1)*** and then click on it from the search results ***(2)***.
   
   ![](media/Ex6-T2-S1.1.png)
    
1. Once the target is enabled, select **Experiments** ***(1)*** on the left, click **+ Create** ***(2)*** drop-down, and select **New experiment** **(3)** .
 
   ![](media/ex6-task3-step9.png)
 
1. On the **Create an experiment** page, under **Basics** tab provide the following values and select **Next: Permissions >** ***(4)***.

    - Subscription: Select the default subscription ***(1)***
    - Resource Group: **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** ***(2)***
    - Name: **contoso-chaos-<inject key="DeploymentID" enableCopy="false" />** ***(3)***
    - Region: Leave it to default 
 
   ![](media/E5T1S10.png)
   
1. On the **Permissions** page, leave the default selection and select **Next: Experiment designer >**.

   ![](media/E5T1S11.png)
 
1. On the **Experiment designer** page select **+ Add action (1)** and choose **Add fault (2)**.

   ![](media/Ex6-T2-S7.3.png)
 
1. On the **Add fault** page, select the following and select **Next: Target resources>** **(4)**.
   
   - Faults: **AKS Chaos Mesh Pods Chaos** ***(1)***
   - Duration (minutes): **5** ***(2)***
   - jsonSpec: Leave it to default ***(3)***
     
   ![](media/2dgn61.png)
     
1. On the **Target resources**, select the **Manually select from a list** **(1)** under **Select target resources** , select the **contoso-traders-aks<inject key="DeploymentID" enableCopy="false" />** ***(2)*** resource, and **Add** ***(3)***.
  
   ![](media/ex6-task3-step14.png)
  
1. Click on **Review + create**.
  
   ![](media/upd-review.png)
   
1. On the **Review + create** click on **Create**.
  
   ![](media/2dgn104.png)
  
1. Navigate back to the **contoso-traders-aks<inject key="DeploymentID" enableCopy="false" />** container instance and select **Access control (IAM) (1)**, click on **+ Add (2)** and select **Add role assignment (3)**. 
  
   ![](media/2dgn121.png)
  
1. In the **Add role assignment** page, under **Role** tab select **Privileged administrator roles**. Select **Owner (1)** in it and then **Next (2)**.
  
   ![](media/ex6-task3-step18.png)
  
1. Next on the **Members** tab select **Managed identity (1)**  for **Assign access to** , click on **+ Select members (2)**  on the **Select managed identities** choose **Chaos Experiment (3)** for **Managed identity** select the experiment **contoso-chaos-<inject key="DeploymentID" enableCopy="false" /> (4)**, click on **Select (5)** and click on **Next** **(6)**.  
   
   ![](media/ex6-task3-step19.png)
  
1. Next on the **Conditions** tab select **Delegation type** as **Not constrained** **(1)** and click on **Review + assign** **(2)**.

   ![](media/ex6-task3-step20.png)

1. Click on **Review + assign**. 
   
   ![](media/ex6-task3-step21.png)
      
1. On the Azure portal navigate back to the Chaos experiment you created **contoso-chaos-<inject key="DeploymentID" enableCopy="false" />** and click on **Start**.
  
   ![](media/2dgn108.png)
 
1. Select **Ok** for **Start this experiment** pop-up.

    ![](media/Ex6-T2-S17.1.png)
       
1. Once the experiment status is **Success** click on **Details** to view the run preview.
 
   ![](media/2dgn109.png)
 
1. On the **Details** preview page select **Action (1)** and view the complete detail of the run on **Fault details** under **Successful targets (2)**.
 
   ![](media/2dgn110.png)

## Summary

In this exercise, you explored monitoring using Application Insights. You also configured Load testing and Chaos experiments for the application.
