# Exercise 1: Implement Dev Box

Duration: 40 minutes

Microsoft Dev Box is a service that provides self-service access to high-performance, preconfigured, and ready-to-code cloud-based workstations called dev boxes.
In the exercise, you'll configure a dev box environment access the dev box, and explore its features.

## Task 1: Create Dev box definition

In this task, you'll create a Dev box definition. Dev box definitions define the image and SKU (compute + storage) that will be used in the creation of the dev boxes.

1. In the Azure portal, search for **Microsoft dev box** **(1)**, and then click on it from the search results **(2)**.

   ![](media/ex1-t1.png)
  
1. Now on the left-hand side blade click on **Dev Centers** **(1)** and then click on **devcenter-<inject key="DeploymentID" enableCopy="false" />** **(2)**.

   ![](media/devops1.1.png)
  
1. On the left-hand side pane, click on **Dev box definitions** **(1)**, and click on **+ Create** **(2)**.

   ![](media/dev-def.png)
  
1. Now under the Create dev box definition window, add the below details and then click on **Create** **(6)**.

   - Name: **devboxdef-01** **(1)**
   - Image: From the drop-down select **Windows 11 Enterprise + Microsoft 365 Apps 21H2 | Hibernate Supported** **(2)**
   - Image version: **Latest** **(3)**
   - Compute: **8vCPU, 32 GB RAM** **(4)**
   - Storage: **1024 GB SSD** **(5)**

   ![](media/devbox.png)
  
1. Once the definition is created. In the Azure portal, search for **Microsoft dev box** **(1)**, and then click on it from the search results **(2)**.

   ![](media/ex1-t1-5.png)
  
   >**Note:** Wait for the deployment to complete before proceeding with the lab.

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Click the Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation Page.
   > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

      <validation step="37bc692b-33c9-4300-b8f7-6d8d12d44c96" />
  
## Task 2: Create a Network connection

In this task, you'll configure the network connection using Dev Center. Network connections determine the region into which dev boxes are deployed and allow them to be connected to your existing virtual networks.

1. Navigate back to the **Microsoft dev box**, and then click on **Dev center** **(1)** and then click on the **devcenter-<inject key="DeploymentID" enableCopy="false" />** **(2)**.

      ![](media/devops1.1.png)

1. Now under left-hand side pane, click on **Networking** under Dev box configuration, and then click on **+ Add**.

      ![](media/e117.png)
  
1. Now under *Add network connection*, select the **fabrikam-connection-<inject key="location" enableCopy="false" />** **(1)** for Network Connection from the drop-down and then click on **Add** **(2)**.

      ![](media/E1T2S3.png)

     >**Note**: Please select the network connection with respect to the resource group region, you can check the resource group location by navigating to **Resource groups** and check the region with respect to **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** resource group.

     ![](media/devops-ex1-t2.png)

## Task 3: Create a dev box pool

In this task, you'll create a Dev pool using a previously configured network connection and Dev Box definitions. A dev box pool is a collection of dev boxes that you manage together. 

1. Return to the Microsoft dev box, and click on **Projects** **(1)** then click on the **devproject<inject key="DeploymentID" enableCopy="false" />** **(2)**.

      ![](media/2dgn75.png)

1. On the left hand side pane click on **Dev box pools** **(1)** and then click on **Create dev box pool** **(2)**.

      ![](media/2dgn76.png)
  
1. Under *Create a dev box pool* window, enter the following details and click on **Create** **(7)**.

   - Name: **devbox-pool-<inject key="DeploymentID" enableCopy="false" />** **(1)**
   - Dev box definition: **devboxdef-01** **(2)**
   - Network Connection: **fabrikam-connection-<inject key="location" enableCopy="false" />** **(3)**
   - Dev box Creator Privileges: **Local Administrator** **(4)**
   - Auto-stop: Select **No** button **(5)**
   - Licensing: Check the checkbox **(6)**
  
      ![](media/E1T3S3.png)

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Click the Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation Page.
   > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.
   
      <validation step="8532054d-6bd4-41ae-a310-928c9ed41958" />

## Task 4: Create and connect to a Dev Box via the Microsoft Dev Box portal

In this task, you'll access a Dev Box using Developer and explore its features.

1. On a new browser tab, visit ```https://devbox.microsoft.com/```.

2. Here, click on **Get started** **(1)**, Name it as **devbox-01** **(2)** and then click on **Create** **(3)**.

   ![](media/24-05-2024(3).png)
   
1. The Devbox creation will take around 60 - 90 minutes time. You can move to the next exercise and come back later to check on the Devbox environment.

   ![](media/2dgn86.png)

1. On **Your Dev box** page, click on the drop down button **(1)** and click on **Open in browser** **(2)**.

   ![](media/2dgn147.png)

1. In Session settings, click on **Connect**.

   ![](media/ex1-t4-1.png)

1. Under **Sign in to Cloud PC** page, enter your credentials and click on **Sign In**.

  - Username: <inject key="AzureAdUserEmail"></inject>

  - Password: <inject key="AzureAdUserPassword"></inject>
  
    ![](media/2dgn150.png)

7. Now the Dev box will start configuring your account and a remote session of your Dev box will launch.

   ![](media/2dgn151.png)  

## Summary

In this exercise, you have created a Dev box definition, Network connection, and Dev box pool in Microsoft Dev Box. Also, you have accessed a Dev Box and explored its features.
