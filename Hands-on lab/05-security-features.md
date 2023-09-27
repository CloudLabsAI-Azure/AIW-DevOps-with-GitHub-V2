# Exercise 4: Explore GitHub's advanced security features

Duration: 40 minutes

In this exercise, you'll explore GitHub Enterprise features which are GitHub's advanced security features. You'll configure and explore Code scanning, CodeQL alerts, Repository security advisories, and GitHub Dependabots.  

## Task 1: Enabling Code scanning and CodeQL alerts 

In this task, you'll configure Code scanning and explore CodeQL alerts. Code scanning is a feature that you use to analyze the code in a GitHub repository to find security vulnerabilities and coding errors. Any problems identified by the analysis are shown on GitHub.

**Note**: To perform this task, the GitHub repository should be public. If the repository visibility is private, please go to the settings of the repository and change the visibility to public.
   
1. Select the **settings** ***(1)*** tab from the GitHub browser tab. Click on **code security and analysis** ***(2)*** under the security side blade.

   ![](media/2dgn168.png)  
   
1. Click on **Set up** **(1)** button to enable CodeQL analysis and select the **Advanced** **(2)** option for creating a CodeQL Analysis YAML file.

   ![](media/2dgn169.png)      

1. Update the workflow name to **codeql-analysis.yml** ***(1)*** and review the yaml file. Select **Commit changes** ***(2)***, then select **Commit directly to the main branch** ***(3)*** and click on **Commit new file** ***(4)***.
  
   ![](media/ex5-task1-step3a.png)

   ![](media/ex5-task1-step3b.png) 
  
1. Navigate to **Actions** ***(1)*** tab, You can review the **workflow** ***(2)*** run.
    
   ![](media/ex5-codeql-actions.png) 
  
1. Navigate to **Security** ***(1)*** tab and click on **View alerts** ***(2)***.
   
   ![](media/ex5-codescanning-viewalerts.png)
  
1. You will be navigated to **Code scanning** section. You'll be able to visualize that the **No code scanning alerts here!**.
   
   ![](media/devops1.6.png)
    
## Task 2: Repository security advisories  
 
In this task, you'll enable Repository security advisories. You can use GitHub Security Advisories to privately discuss, fix, and publish information about security vulnerabilities in your repository.  Anyone with admin permissions to a repository can create a security advisory.
 
1. Navigate to **Security** ***(1)*** tab, select **Advisories** ***(2)*** from the side blade and click on **New draft security advisory** ***(3)***.

   ![](media/ex5-t2-advisories.png)  
     
1. In the Open a draft security advisory tab, under the Advisory Details section provide the following details.

   - Title: **Improper Access Control in aiw-devops-with-github-lab-files/src/TailwindTraders.Ui.Website/src/App.js** ***(1)***
   - CVE identifier: **Request CVE ID later** ***(2)***
   - Description: **Add** ***(3)*** the below mentioned details in the description section.
   
   ```
   Impact
   What kind of vulnerability is it? Who is impacted?

   HTTP request handlers should not perform expensive operations such as accessing the file system, executing an operating system command, or interacting with a database without limiting the rate at which requests are accepted. Otherwise, the application becomes vulnerable to denial-of-service attacks where an attacker can cause the application to crash or become unresponsive by issuing a large number of requests at the same time.

   Patches
   Has the problem been patched? What versions should users upgrade to?

   It is patched and rectified the error. Please use 1.2 version

   Workarounds
   Is there a way for users to fix or remediate the vulnerability without upgrading?

   // set up rate limiter: maximum of five requests per minute
   var RateLimit = require('express-rate-limit');
   var limiter = new RateLimit({
   windowMs: 1601000, // 1 minute
   max: 5
   });

   // apply rate limiter to all requests
   app.use(limiter);

   Added the above code in app.js

   References
   Are there any links users can visit to find out more?

   https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xa4-lack-of-resources-and-rate-limiting.md
   https://codeql.github.com/codeql-query-help/javascript/js-missing-rate-limiting/
   ```
    
   ![](media/ex5-t2-securityadvisor1.png)
   
1. In the Affected products section, provide the following details and click on **Create draft security advisory** ***(7)***   
 
   - Ecosystem: **composer** ***(1)***
   - Package name: **aiw-devops-with-github-lab-files/src/TailwindTraders.Ui.Website/src/App.js** ***(2)***
   - Affected version: **<1.2** ***(3)***
   - Patched version: **1.2** ***(4)***
   - Severity: **High** ***(5)***
   - Common Weakness Enumerator (CWE): **Improper Access Control (CWE-284)** ***(6)***
  
   ![](media/ex5-t2-securityadvisor2.png)
   
 1. Once the security advisory is created, scroll-down and click on **start a temporary private fork**. It is used to collaborate on a patch for this advisory.

    ![](media/ex5-t2-securityadvisor3.png)
    
    ![](media/ex5-t2-securityadvisor4.png)
  
 1. After having the temporary fork you can request a CVE, it is used for GitHub reviews and published security advisories. Upon review, we may use this advisory to send Dependabot alerts to affected repositories and redistribute the advisory through our API and Atom feed.

    **Note**: This process may take up to 3 working days. Please do not close the security repository.
 
### Task 3: Using Dependabot

In this task, you will use Dependabot to track the versions of the packages we use in our GitHub repository and create pull requests to update packages for us.

1. In your lab files GitHub repository, navigate to the **Settings** ***(1)*** tab and select the **Code security and analysis** ***(2)*** under Security from side blade. Make sure **Dependabot alerts** is **Enabled** ***(3)***, if not click on **Enable** to Enable Dependabot alerts. Click on **Enable** ***(4)*** to Enable Dependabot security updates.

   > **Note**: Enabling the `Dependabot security updates` will also automatically enable `Dependency graph` and `Dependabot alerts`.

   ![The GitHub Repository Security Overview tab.](media/ex5-t3-enabledb.png "GitHub Repository Security Overview")

   > **Note**: The alerts for the repository may take some time to appear. The rest of the steps for this task rely on the alerts to be present. You can continue with the next exercise as this is an independent task and doesn't affect the lab. Please visit this task later and complete the task.

1. To observe Dependabot issues, navigate to the **Security** ***(1)*** tab and select the **View Dependabot alerts** ***(2)*** link.

   ![GitHub Dependabot alerts in the Security tab.](media/ex5-t3-viewdb.png "GitHub Dependabot alerts")

1. You should arrive at the `Dependabot alerts` blade in the `Security` tab.

   ![GitHub Dependabot alerts in the Security tab.](media/ex5-t3-dependabot.png "GitHub Dependabot alerts")

1. Sort the Dependabot alerts by `Package name`. Under the **Package** ***(1)*** dropdown menu, search for **node-forge** ***(2)*** by typing in the search box and select **node-forge** ***(3)*** vulnerability.

   ![Summary of the `handlebars` Dependabot alert in the list of Dependabot alerts.](media/ex5-t3-node-forge.png "`handlebars` Dependabot alert")

1. Select any of the `node-forge` Dependabot alert entries to see the alert detail. After reviewing the alert, select **Review security update**.

   ![The `handlebars` Dependabot alert detail.](media/ex5-t3-reviewsu.png "Dependabot alert detail")
   
   **Note:** If you see Create Security Update option, click on it. After it is created then select Review security update. 

1. Navigate to **Pull Requests** ***(1)*** tab, find the Dependabot security patch pull request ***(2)*** and merge it to your main branch.

   ![List of Pull Requests.](media/ex5-t3-open-nfpr.png "Pull Requests")
   
1. Click on **Merge pull request** and followed by click on **Confirm merge**. 

   ![The Pull Request Merge Button in the Pull Request detail.](media/ex5-t3-merge-pr.png "Pull Request Merge Button")
    
   >**Note**: In case you see any errors with the merge request. Retry steps 4 to 6 by selecting any other Dependabot alert.

1. Pull the latest changes from your GitHub repository to your local GitHub folder.

   ```pwsh
   cd C:\Workspaces\lab\aiw-devops-with-github-lab-files  # This path may vary depending on how
                                                            # you set up your lab files repository
   git pull
   ```
   
## Task 4: Explore Secret Scanning (READ-ONLY)   

In this task, you'll explore how secret scanning works and see how it generates alerts. GitHub scans repositories for known types of secrets, to prevent fraudulent use of secrets that were committed accidentally.

**Note**: This is a **READ-ONLY** task. Please do not perform the steps in the lab environment.

1. From your GitHub repository, click on the **Settings** tab.

   ![](media/2dg110.png)
    
1. Select **Code security (1)** from the sidebar and make sure **Secret scanning is enabled (2)**.

   ![](media/2dg111.png)   
    
1. Navigate back to **Code (1)** and click on **src (2)** folder.

   ![](media/2dg112.png)    
   
1. Click on **Add file** and select **create new file** option.

   ![](media/2dg113.png)    
   
1. Add new file with name **build.docker-compose.yml (1)** name, add the code mentioned below **commit** the file. Here, you'll expose the **application ID** of a service principal.

   ```
   version: "3.4"
   services:
   api:
      build: ./ContosoTraders.Ui.Website/
      app id: 36540dcd-7bc3-4e16-90ca-4decb9ff8c36
      app secret: i1R8Q~Hn8dHn86VlWE7xJtLR4FKTIcQBXcebqcv4
   web:
      build: ./ContosoTraders.Api.Products
   ```
   
   ![](media/2dg115.png)   
   
1. Select **Security (1)** tab and click on **Secret scanning (2)** from the sidebar. Here, you'll notice that an alert is generated referring to the same **Application ID** which was exposed in `build.docker-compose.yml` file. This is how the Secret scanning feature works and generates alerts to notify you.

   ![](media/2dg116.png) 
   
1. Click on the **Next** button present in the bottom-right corner of this lab guide.  

## Summary 

In this exercise, you explored and configured different GitHub Advance Security features.



    

