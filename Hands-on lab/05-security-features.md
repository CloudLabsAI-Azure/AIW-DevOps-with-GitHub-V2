# Exercise 3: Explore GitHub advance security features 

Duration 60 minutes

Once the Fabrikamk Medical Conferences developer workflow has been deployed, we can apply the github advance security features.


## Task 1: Enabling Codescanning and CodeQL alerts 

What is codescanning? 
Code scanning is a feature that you use to analyze the code in a GitHub repository to find security vulnerabilities and coding errors. Any problems identified by the analysis are shown in GitHub.

1. Make sure your repository is public

   **Note:** If the repository visibility is private, go to the settings of the repository and change the visibility to public.
   
1. Go to seetings tab of the repository, then under security tab select code security and analysis.
   Click on Setup button of the code scanning. 

   ![](media/adse11.png)
   

1. By reaching into Codescanning pane under security tab, click on configure codeQL alerts.


   ![](media/adse12.png)
   
  
1. It will generate a workflow codeql-analysis.yml. Review the yml file, you can find how many languages supported by codeQL and click on Start Commit, then click on      commit new file
  
  
   ![](media/adse13.png)
  
  
  
      **Note** For most projects, this workflow file will not need changing; you simply need to commit it to your repository. You may wish to alter this file to             override the set of languages analyzed or to provide custom queries or build logic.
  
  1. Under Actions tab you can see the workflow committed successfully.
    
      ![](media/adse14.png)
  
  
1. Go to Codescanning under security tab you can see code scanning alerts enabled. Click on View alerts
   
   
    ![](media/adse15.png)
    
    
 1. Click on the Missing rate Limiting alert and find on which line the alert showing, it will be on 73 line of the App.js file.


    ![](media/adse16.png)
    
    Under security tab you can see the Missing rate Limiting in App.js file under Content-web folder
    
    ![](media/adse17.png)
    
  1. Open App.js file from the content-web folder and Add the following code after the 6th line of App.js file
  
     ```pwsh
       // set up rate limiter: maximum of five requests per minute
        var RateLimit = require('express-rate-limit');
       var limiter = new RateLimit({
        windowMs: 1*60*1000, // 1 minute
        max: 5
        });
      ```
         
      
      After adding the code it will looks like this
      
      ![](media/adse18.png)
      
  1. Add the following code before the alert line which would be 79 starts with app.get('*', (req, res) => {
   
      ```pwsh
        // apply rate limiter to all requests
        app.use(limiter);
      ```
    
   1. After adding the code it will looks like this
        
      ![](media/adse19.png)
      
 1. After adding the entire code go down and  click commit the file. It will successfully commit.
 
    ![](media/adse21.png)
  
  1. Go to codescanning under security tab, you can see the missing rate limit cleared.
  
      ![](media/adse22.png)

      
 ## Task 2: Repository security advisories  
 
 You can use GitHub Security Advisories to privately discuss, fix, and publish information about security vulnerabilities in your repository.  Anyone with admin permissions to a repository can create a security advisory. Anyone with admin permissions to a repository also has admin permissions to all security advisories in that repository. People with admin permissions to a security advisory can add collaborators, and collaborators have write permissions to the security advisory.
 
 1. Create Security Repository advisories
 
     Go to Security tab and then select advisories and then select New draft security advisory option.
     
     ![](media/adse23.png)
     
  1. In the affected Product section Select the ecosystem as composer, provide the package name as **mcw-continuous-delivery-lab-files/content-web/app.js**, provide     affected version as <1.2 and patched version as 1.2 and provide severity as high
  
      ![](media/secad1.png)
     
   1. In the Common Weakness Enumerator Section provide CWE-284 which stands Improper Access Control havinig Missing Rate Limiting, provide the title if its not generated automatically as **Improper Access Control in mcw-continuous-delivery-lab-files/content-web/app.js**
    
      ![](media/secad4.png)
      
   1. In the description box include the following:
       
       Impact
       
      _What kind of vulnerability is it? Who is impacted?_

      HTTP request handlers should not perform expensive operations such as accessing the file system, executing an operating system command or interacting with a      database without limiting the rate at which requests are accepted. Otherwise, the application becomes vulnerable to denial-of-service attacks where an attacker can cause the application to crash or become unresponsive by issuing a large number of requests at the same time.
      

       Patches
       
      _Has the problem been patched? What versions should users upgrade to?_

      It is patched and rectified the error. Please use 1.2 version


       Workarounds
       
      _ Is there a way for users to fix or remediate the vulnerability without upgrading?_

      // set up rate limiter: maximum of five requests per minute
      var RateLimit = require('express-rate-limit');
      var limiter = new RateLimit({
       windowMs: 1*60*1000, // 1 minute
        max: 5
        });

       // apply rate limiter to all requests
       app.use(limiter);

       Added the above code in app.js

       References
       
      _Are there any links users can visit to find out more?_

      https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xa4-lack-of-resources-and-rate-limiting.md
      https://codeql.github.com/codeql-query-help/javascript/js-missing-rate-limiting/
    
  1. After filled the description box fill the Credit section with current user name. Then click on Create draft security advisory.
 
     ![](media/adse24.png)
    
 1. Once created the security advisory go to start a temporary private fork, it is used to collaborate on a patch for this advisory.

    ![](media/secad8.png)
  
 1. After having the temporary fork you can request for a CVE, it is used for GitHub reviews published security advisories. Upon review, we may use this advisory to send Dependabot alerts to affected repositories and redistribute the advisory through our API and Atom feed.

**Note**: This process may take up to 3 working days. Please do not close the security repository.
 
### Task 4: Using Dependabot

Another part of continuous integration is having a bot help track versions of the packages used in the application and notify us when there are newer versions. In this task, we will use Dependabot to track the versions of the packages we use in our GitHub repository and create pull requests to update packages for us.

1. In your lab files GitHub repository, navigate to the `Security` tab. Select the `Enable Dependabot alerts` button.

    ![The GitHub Repository Security Overview tab.](media/hol-ex1-task2-step1-1.png "GitHub Repository Security Overview")

2. You should arrive at the `Security & analysis` blade under the `Settings` tab. Enable `Dependabot security updates`.

    > **Note**: Enabling the `Dependabot security updates` will also automatically enable `Dependency graph` and `Dependabot alerts`.

    ![The GitHub Repository Security and Analysis blade under the GitHub repository Settings tab. We enable Dependabot alerts and security updates here.](media/hol-ex1-task2-step2-1.png "GitHub Security & Analysis Settings")

    > **Note**: The alerts for the repository may take some time to appear. The rest of the steps for this task rely on the alerts to be present. You can continue with the next exercise as this is an independent task and doesn't affect the lab. Please visit this task later and complete the task.

3. To observe Dependabot issues, navigate to the `Security` tab and select the `View Dependabot alerts` link. You should arrive at the `Dependabot alerts` blade in the `Security` tab.

    ![GitHub Dependabot alerts in the Security tab.](media/hol-ex1-task2-step3-1.png "GitHub Dependabot alerts")

4. Sort the Dependabot alerts by `Package name`. Locate the `handlebars` vulnerability by typing `handlebars` in the search box under the `Package` dropdown menu.

    ![Summary of the `handlebars` Dependabot alert in the list of Dependabot alerts.](media/hol-ex1-task2-step4-1.png "`handlebars` Dependabot alert")

5. Select any of the `handlebars` Dependabot alert entries to see the alert detail. After reviewing the alert, select `Create Dependabot security update` and wait a few moments for GitHub to create the security update.

    ![The `handlebars` Dependabot alert detail.](media/hol-ex1-task2-step5-1.png "Dependabot alert detail")

    ![The Dependabot security update message observed when creating a Dependabot security update.](media/hol-ex1-task2-step5-2.png "Dependabot security update message")

6. In the `Pull Requests` tab, find the Dependabot security patch pull request and merge it to your main branch.

    ![List of Pull Requests.](media/hol-ex1-task2-step6-1.png "Pull Requests")

    ![The Pull Request Merge Button in the Pull Request detail.](media/hol-ex1-task2-step6-2.png "Pull Request Merge Button")
    
    >**Note**: In case if you see any errors with merge request. Retry step 4 to step 6 by selecting any other`handlebars` Dependabot alert.

7. Pull the latest changes from your GitHub repository to your local GitHub folder.

    ```pwsh
    cd C:\Workspaces\lab\mcw-continuous-delivery-lab-files  # This path may vary depending on how
                                                            # you set up your lab files repository
    git pull
    ```
    
  
  

 
 
 

  
  

    
