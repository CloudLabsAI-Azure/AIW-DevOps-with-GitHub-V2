# Exercise 1: Dev Box

## Task 1: Create Dev box definition

1. In Azure portal, search for **Microsoft dev box** **(1)**, and then click on it from the search results **(2)**.

  ![](media/e101.png)
  
1. Now on the left hand side blade click on **Dev Centers** **(1)** and then click on **devcenter-[DID]** **(2)**.

  ![](media/e109.png)
  
1. On the left hand side pane, click on **Dev box definitions** **(1)**, and click on **+ Create** **(2)**.

  ![](media/e110.png)
  
1. Now under Create dev box definition window, add the below details and then click on **Create** **(6)**.

  - Name: **devboxdef-01**
  - Image: **Windows 11 Enterprise + Microsoft 365 Apps 21H2**
  - Image version: **Latest**
  - Compute: **4vCPU, 16 GB RAM**
  - Storage: **256 GB SSD**

  ![](media/e112.png)
  
1. Once the definition is created, In Azure portal, search for **Microsoft dev box** **(1)**, and then click on it from the search results **(2)**.

  ![](media/e101.png)
  
>**Note:** Wait for the deployment to complete before proceeding with the lab.
  
## Task 2: Create Network connection

1. Navigate back to *Microsoft dev box* and then on the left hand side blade, click on **Network Connections** **(1)**, and then click on **Create network connection** **(2)**.

  ![](media/e113.png)
  
1. Now under *Create a network connection* window, enter the following details and click on **Review and Create**.

  - Domain join type: **Azure active directory join**
  - ResourceGroup: **devbox-rg**
  - Name: **devbox-network**
  - Virtual network: ****
  - Subnet: ****

  ![](media/e116.png)

1. After deployment validation is passed, click on **Create**.

  ![](media/e115.png)
  
>**Note:** Wait for the deployment to complete before proceeding with the lab.

1. Once the network connection is created, navigate back to the **Microsoft dev box**, and then click on **Dev center** **(1)** and then click on the **devcenter-[DID]** **(2)**.

  ![](media/e109.png)

1. Now under left hand side pane, click on **Networking** under Dev box configuration, and then click on **+ Add**.

  ![](media/e117.png)
  
1. Now under *Add network connection*, click on **Add**.

    ![](media/e118.png)
    
## Task 3: Create dev box pool

1. Return to Microsoft dev box, and click on **Projects** **(1)** then click on the **devbox-project** **(2)**.

  ![](media/ex101.png)

1. On the left hand side pane click on **Dev box pools** **(1)** and then click on **Add New** **(2)**.

  ![](media/ex102.png)
  
1. Under *Create a dev box pool* window, enter the following details and click on **Create**.

  - Name:**devbox-pool**
  - Dev box definition: **devboxdef-01**
  - Network Connection: **devbox-network**
  - Dev box Creator Privileges: **Local Administrator**
  - Licensing: Check the checkbox
  
  ![](media/e119.png)
  
## Task 4: Giving user access over Dev box

1. Return to Microsoft dev box, and click on **Projects** **(1)** then click on the **devbox-project** **(2)**.

  ![](media/ex101.png)

1. On the left hand side pane click on **Access control** **(1)** then click on **+ Add** **(2)** and select **Add role assignment** **(3)** from the drop down.

  ![](media/e120.png)

1. Under Role, select **DevCenter Dev box User** **(1)**, and then click on **Next** **(2)**.

  ![](media/e122.png)
  
1. Under Members, click on **+ Select members** **(1)**, then search and select the ODL user **(2)**, and then click on **Select** **(3)** followed by **Review + assign** **(4)**.

  ![](media/e123.png)
  
## Task 4: Launching Dev box

1. On a new browser tab, visit ```https://devbox.microsoft.com/```.

1. Here, click on **Get started** **(1)**, Name it as **devbox-01** **(2)** and then click on **Create** **(3)**.

  ![](media/e124.png)


