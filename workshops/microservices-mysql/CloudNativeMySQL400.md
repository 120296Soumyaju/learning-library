![](images/400/PictureTitle.png)  
Update: October 1, 2017

## Introduction

This is the fourth of several labs that are part of the **Oracle Cloud DevOps: Cloud Native Microservices MySQL workshop.** This workshop will walk you through the Software Development Lifecycle (SDLC) for a Cloud Native project that will create and use several Microservices.

In the first lab (100), the Project Manager created a new project in the Developer Cloud Service and also created and assigned tasks to the developers of this application. In the second lab (200), the Java developer created a new microservice to retrieve and filter Twitter data. In the third lab (300), the full stack developer created a microservice to extract data from the MySQL database. In this lab (400), you will assume the persona of the UI developer, who will create a next generation product catalog UI. The product catalog will combine both the Twitter Feed Microservice and the Product Catalog Microservice into a single unified view for the consumer.

**To log issues**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives

- Access Developer Cloud Service
- Import code from an external Git repository
- Import a project into Brackets
- Build and deploy a project using Developer Cloud Service and Oracle Application Container Cloud Service

## Required Artifacts

- The following lab requires an Oracle Public Cloud account that will be supplied by your instructor. You will need to download and install the latest version of Brackets or use a supplied compute VM. Instructions are found in the Student Guide.

# Create A Next Generation Product Catalog UI

## Explore Developer Cloud Service

### **STEP 1**: Review Agile Board

- This Lab assumes that you just completed Lab 300 and are still connected to the Oracle Cloud, that you're still in the Developer cloud Service Dashboard, and you're viewing the "Alpha Office Product Catalog Project." If for some reason that is not the case, follow the first several Steps of Lab 100 to once again view the Developer Cloud Service Console.

- Although you will remain connected to the Oracle Cloud using the user account you were provided, you will take on the Persona of ***John Dunbar*** as you perform the following steps.

    ![](images/john.png)  

- Within the **Alpha Office Product Catalog Project**, click on **Agile** found on the left hand navigation.

    ![](images/400/Picture11.png)  

### **STEP 2**: Display the Active Sprint

- On the **Microservices** Board, click **Active Sprints**

    ![](images/400/Picture13.png)  

## Create Initial Git Repository

### **STEP 3**: Create Initial Git Repository

To begin development on our Product Catalog UI, we could start coding from scratch. However, prior to the formal kickoff of this project, you (as John Dunbar) have already started doing some proof-of-concept development outside of the Developer Cloud Service in order to assess the feasibility of your assignment. You want to bring that existing code into the Developer Cloud Service as a starting point for your UI. You will do that by cloning your external GIT repository into the Developer Cloud Service. Your first step will be to accept your task using the agile board.

- Drag and drop **Feature 4 - Create Alpha Office Product Catalog UI** into the **In Progress** swim-lane.  

    ![](images/400/Picture14.1.png)  

- Leave the defaults, and Click **OK**.

    ![](images/400/Picture14.2.png)  

- Your Sprint progress will appear as shown below.

    ![](images/400/Picture16.2.png)  

- In the left hand navigation panel, click **Project**

- Click **New Repository**. In the New Repository wizard enter the following information and click **Create**.

    **Name:** `AlphaOfficeProductCatalogUI`

    **Description:** `Alpha Office Product Catalog UI`

    **Initial content:** `Import existing repository`

    **Enter the URL:** `https://github.com/pcdavies/ProductCatalogUI.git`

    ![](images/400/Picture18.2.png)  

- You have now created a new GIT repository stored within the Developer Cloud Services that is based on an existing repository.

    ![](images/400/Picture19.png)  

## Create Default Build and Deployment Process

### **STEP 4**: Create Default Build Process

Now that we have the source code in our managed GIT repository, we need to create a build process that will be triggered whenever a commit is made to the master branch. We will use NPM package manager to set up a Node.js build process in this section.

- On the left side navigation panel click **Build** to access the build page.

- Click **New Job**.

- In the New Job popup enter `Product Catalog UI Build` for the Job Name, and then click **Save**.

    ![](images/400/Picture21.png)  

- You are now placed into the job configuration screen.

    ![](images/400/Picture22.png)  

- Click the **Source Control** tab. Click **Git** and select the **AlphaOfficeMyProductCatalogUI.git** from the drop down.

    ![](images/400/Picture24.png)  

- Click the **Triggers** tab.

  **Select**: `Based on SCM polling schedule`

    ![](images/400/Picture25.png)  

- Click the **Build Steps** tab. Click **Add Build Step**, and select **Execute shell**.

    ![](images/400/Picture26.png)  

- For **Command** enter: `npm install`

    ![](images/400/Picture27.png)  

- Click the **Post Build** tab and complete the following:
  - Check **Archive the artifacts**.
  - Enter `**/target/*` for **Files to Archive**.  
  - Verify **GZIP** in the Compression Type.
  
    ![](images/400/Picture28.png)  

- Click **Save** to complete the configuration.

- Click the **Build Now** button to start the build immediately. 

    ![](images/400/Picture28_5.png)  

- Wait, as it may take up to a few minutes for the queued job to execute, but when it does, the status will change to the following:

    ![](images/400/Picture29.png)  

  **NOTE:** Once the build begins, it should take approximately 1 to 2 minutes for the build to complete. Once complete, you will be able to see the number of successful test runs in the Test Result Trend section. ***Wait for the build to complete before continuing to the next step***, as we need the build artifact to complete the deployment configuration.

- After the build begins, you can also click on the **Console Icon** ![](images/400/Picture29.1.png) to monitor the build log details.

    ![](images/400/Picture30.png)  

### **STEP 5**: Create Default Deployment Process

Now that we have an automated build process, we will setup up a deployment configuration that will push out build artifacts to a node.js environment running on Application Container Cloud Service whenever a successful build occurs.

- On the navigation panel click **Deploy** to access the Deployment page. Click **New Configuration**.

- Enter the following data:

  **Configuration Name**: `DeployProductCatalogUI`

  **Application Name**: `AlphaOfficeProductCatalogUI`

    ![](images/400/Picture32.png)  

- Click on **Deployment Target** drop down and select deployment defined in lab 200.

    ![](images/400/Picture33.png)  

- In Deployment window, click **Test Connection**. If Successful, click **Use Connection**:

    ![](images/400/Picture34.3.png)  

- Set the following Properties as follows:

  - **Runtime**: `Node`

  - **Subscription**: `Hourly`

  - **Type:** `Automatic` and `Deploy stable builds only`

  - **Job:** `Product Catalog UI Build`

  - **Artifact:** `target/msdbw-mysqlmicroservice.zip`

    ![](images/400/Picture35.3.png)  

- To reduce the number of resources that are used we will modify the default deployment of 2 instances. Click **Include ACCS Deployment** and enter the following in the text box:

```
{
  "memory": "1G",
  "instances": "1"
}  
```
![](images/400/Picture35.4.png)  

- Click **Save**

    ![](images/400/Picture36.2.png) 

- A message shows the deployment has been created

    ![](images/400/Picture37.1.png) 

- Click the gear drop down for **AlphaOfficeProductCatalogUI** and select **Start**

    ![](images/400/Picture37.2.png)  

- Wait until the message **Starting application** changes to **Last deployment succeeded**

    ![](images/400/Picture38.2.png)  

    ![](images/400/Picture38.3.png)  

## Verify Product Catalog UI deployment

### **STEP 6**: Test Product Catalog UI

- We are able to access the application directly from Developer Cloud Service. Click **AlphaOfficeProductCatalogUI** to launch the application.

    ![](images/400/Picture39.png)  

- A new tab in the browser should open with application running.

    ![](images/400/Picture42.png)  

- The UI application is running, but REST services have not been activated.

# Add Microservice endpoints

Now that we have our default application, we want to modify this application to use the deployed Microserivces from lab 200 and lab 300. For this task we will use the Brackets text editor to download code from Developer Cloud Service and make our modifications. Once the new code is ready for deployment, we will check in the code which will trigger a new build and deployment. Normally we would want to check the code into a branch and go through the code review and merge process defined in lab 200. To save time we are not including that step.

## Clone Project to Brackets Text Editor

### **STEP 7**:	Start Brackets Text Editor

- Start **Brackets** text editor. How you start Brackets will depend on your OS. We have documented how to start Brackets from our OEL image.

***Note***: If you do not have Brackets installed, please follow the **Student Guide** that is part of this Workshop. You will find instruction on how to install Git and Configure Brackets.

- Right click **Brackets** desktop icon and select **Open**

    ![](images/400/image052.png)  

- Brackets should open with the **ProductCatalogUI** folder already loaded.

    ![](images/400/image053.2.png)  

### **STEP 8**: Copy GIT URL

- Back in Developer Cloud Service, click on **Project**. On right side, select the URL for **AlphaOfficeProductCatalogUI.git**. Right click and select **Copy**

    ![](images/400/image054.2.png)  

### **STEP 9**: Clone GIT Repository

- Back in the Brackets editor, Click on ![](images/400/image055.png) GIT icon found on the right side of the editor.

  ![](images/400/image055.5.png)  

- Click **Clone**

  ![](images/400/image056.png)  

- Paste in Git URL that you captured from Developer Cloud Service. Username should be populated automatically. Enter your **Password** and click **Save credentials**. Once completed click **OK** to start the cloning process.

    ![](images/400/image057.png)  

- While the clone is running a dialog box will show you the progress.

    ![](images/300/image058.png)  

- You now have a local copy of the repository.

    ![](images/400/image059.png)

### **STEP 10**: Edit the UI Code

- Note to Pat's team - Lab Guide 400 Steps 10 and Step 11 are works in progress - I'm having problems with the Brackets editor and I am not clear on Dennis' intentions for merging into the DCS master branch.  See below. 

- First go back to Developer Cloud Service to obtain the URLs for the two microservices created in Labs 200 and 300.  Click on **Deploy** in the dashboard, and then right click on the name AlphaOfficeMySQLREST to copy the URL for the microservice.  Do the same for the JavaTwitterMicroservice.  Save these URLs because you will be pasting them into the UI code.

    ![](images/400/image060.png)

- In Brackets, choose the public/js/alphaOffice.js file to edit.  You will be pasting the URLs of the two microservices into the code in order to access these services.  Paste the URL for the AlphaOfficeMySQLREST microservice as the value for the Javascript variable dbServiceURL.  Paste the URL for the JavaTwitterMicroservice microservice as the value for the Javascript variable twitterServiceBaseURL.

    ![](images/400/image062.png)

- Choose **Save** from the Brackets file menu.

    ![](images/400/image063.png)

### **STEP 11**: Push the Edited Code Back to the Developer Cloud Service

- Note to Pat's team - Again this step is a work in progress.  Dennis intended this step to be the shortest and simplest way to push this edit to the DCS master branch.  His text is "Normally we would want to check the code into a branch and go through the code review and merge process defined in lab 200. To save time we are not including that step."  Any suggestions of the best way to do this?  Below are the images and verbiage I used for the Devops MySQL lab I helped Derrick create last spring:

- Make sure both check boxes are checked at the bottom left of the Brackets screen. (One checkbox is on the same line as the Commit button, and one is on the same line as alphOffice.js.)

- Then click Commit. 

    ![](images/400/image070.png)

- Note: there are a number of formatting and other non-fatal warnings that will be reported for the server.js file. Ignore these.

- Enter a comment for the commit and click OK.

    ![](images/400/image071.png)

- You may need to enter a Git username. (Enter your username for your cloud service.) And you may need to enter some email address. (Any will do.) Finally, click OK.

    ![](images/400/image072.png)

- Click on the Git Push Icon.

    ![](images/400/image073.png)

- Enter your cloud username and password that you were given. Make sure Save credentials to remote url (in plain text) is checked. Finally, click OK.

    ![](images/400/image074.png)

- The edited branch within the local Git repository has been successfully pushed to the repository in the Oracle Developer Cloud Service. Click OK.

    ![](images/400/image075.png)

- At this point I don't know what the best way is to proceed.  If someone has some extra cycles and can help me figure out the best way to update the master branch without creating another branch, I would appreciate the help.  

### **STEP 12**: Test Product Catalog UI with Edited Code

- To test the edited code, refresh the browser window that was opened in Step 6. The REST services have now been activated, and the UI application is fully functional.

   ![](images/400/Picture50.png)  

### **STEP 13**: Complete Task

We have now verified that the Product Catalog UI has been deployed and functions properly. To complete this lab, we will mark the Issue as completed in the Sprint.

- Back in the Developer Cloud Service window, click **Agile**, followed by clicking **Active Sprints**.

- Drag and drop **Feature 4** from **In Progress** to **Completed**.

    ![](images/400/Picture56.2.png)  


- In the Change Progress popup click **Next**.

    ![](images/400/Picture57.png)  

- In the **Add Time Spent** popup, set the **Time Spent** to `1` and click **OK**.

    ![](images/400/Picture57.5.png)  

- Your Sprint should now look like the following:

    ![](images/400/Picture58.2.png)  

- **You are now done with this lab.**
