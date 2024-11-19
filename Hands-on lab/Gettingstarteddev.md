# Microsoft Dev Box for Developers

### Overall Estimated Duration: 2 hours

## Overview

Azure AI services offer a comprehensive set of tools that allow you to integrate intelligent features into your applications, such as image recognition, text analysis, and language processing. With services like Azure Cognitive Services, Azure Machine Learning, and Azure OpenAI, you can leverage advanced AI capabilities to streamline workflows, solve complex problems, and enhance the functionality of your applications. These services enable you to build powerful AI-driven solutions, making it easier to address real-world challenges and drive innovation in the cloud.

## Objective

This lab is designed to equip participants with hands-on experience in exploring Azure AI services, such as Computer Vision and Cognitive Services, to enhance applications with capabilities like image recognition, text analysis, and speech processing.

-   **Explore Computer Vision :** Implement a Cognitive Services resource to analyze images using the Computer Vision service. Configure and run a client app to extract captions, objects, and tags for visual insights.
-   **Explore Cognitive Services :** Implement an Anomaly Detector resource to analyze time-series data and detect anomalies. Configure a client app to identify unusual patterns for real-world insights.

## Prerequisites

Participants should have the following prerequisites:

-   **Basic Understanding of Cloud Computing :** Familiarity with fundamental cloud concepts and services, particularly in the context of Microsoft Azure.
-   **Knowledge of Azure Cognitive Services :** Understanding of the Azure Cognitive Services suite, including how to provision and use services like Computer Vision and Anomaly Detector.
-   **Experience with the Azure Portal**: Proficiency in navigating and using the Azure Portal to manage and configure cloud resources.
-   **Familiarity with PowerShell or Cloud Shell :** Basic knowledge of using PowerShell or Cloud Shell for running commands and scripts within Azure.
-   **Basic Programming Knowledge :** Understanding of scripting or programming languages like PowerShell, which are used for configuring and running client applications in Azure.
-   **Understanding of APIs and Endpoints :** Familiarity with how to interact with APIs and use endpoints for connecting to services in Azure.
-   **Knowledge of Security Best Practices :** Awareness of security principles related to cloud services, including handling keys, authentication, and securing resources.

## Architechture

The architecture for integrating Azure AI services into applications involves using **Azure Cognitive Services**, such as **Computer Vision** for image analysis and **Anomaly Detector** for time-series data analysis. A client application communicates with these services via REST APIs, sending data for processing (images or time-series). The services are provisioned within an **Azure Resource Group** and interact with **Azure Blob Storage** for data storage. Results are returned to the application for further use, such as generating insights or triggering notifications. This architecture leverages Azure's managed services to provide scalable, intelligent capabilities for real-world applications.

## Architechture Diagram

![](../media/archdiagram.JPG)

## Explanation of Components

The architecture for this lab involves several key components:

-   **Computer Vision :** Provides image analysis capabilities, including object detection, text extraction, and image tagging.
-   **Anomaly Detector :** Analyzes time-series data to identify unusual patterns or anomalies.
-   **Azure Resource Group :** A container that organizes and manages Azure resources, including Cognitive Services, for efficient deployment and scaling.
-   **Azure Blob Storage :** Stores images or time-series data, providing scalable storage for input data used by the AI services.
-   **Output Insights :** Processed results from the AI services are returned to the client application for further action, such as generating insights or triggering automated responses.


## Getting Started with Lab

Welcome to your Getting started with Azure AI services Lab! We've prepared a seamless environment for you to explore and learn about Azure services. Let's begin by making the most of this experience:

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and **Lab Guide** will be right at your fingertips within your web browser.

   ![Create storage by clicking confirm.](../media/GettingStarted/gspage01.png)  

### Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment Details** tab.

   ![Create storage by clicking confirm.](../media/GettingStarted/ai-900-gettingstarted-04.png)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
   ![](../media/GS8.png)
 
## Managing Your Virtual Machine
 
Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!
 
  ![](../media/GS5.png)

## Lab Validation

1. After completing the task, hit the **Validate** button under Validation tab integrated within your lab guide. If you receive a success message, you can proceed to the next task, if not, carefully read the error message and retry the step, following the instructions in the lab guide.

   ![Inline Validation](../media/inline-validation.png)

1. You can also validate the task by navigating to the **Lab Validation** tab, from the upper right corner in the lab guide section.

   ![Lab Validation](../media/lab-validation.png)

1. If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

 
## Let's Get Started with Azure Portal
 
1. On your virtual machine, click on the Azure Portal icon as shown below:
 
    ![](../media/GS1.png)
 
1. You'll see the **Sign into Microsoft Azure** tab. Here, enter your credentials:
 
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>
 
      ![](../media/GS2.png "Enter Email")
 
3. Next, provide your password:
 
   - **Password:** <inject key="AzureAdUserPassword"></inject>
 
      ![](../media/GS3.png "Enter Password")

1. If you see the pop-up Action Required, click **Ask Later**.

   ![](../media/asklater.png)

   >**NOTE:** Do not enable MFA, select **Ask Later**.
 
1. If you see the pop-up **Stay Signed in?**, click **No**.

   ![](../media/GS9.png)

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue the lab.

1. If a **Welcome to Microsoft Azure** popup window appears, click **Maybe Later** to skip the tour.

## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on **Next** from the lower right corner to move on to the next page.

![](../media/GS4.png)

### Happy Learning!!

