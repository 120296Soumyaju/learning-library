# Tips for Workshop Developers -- Instructor Led

## Steps for creating a new workshop

- To start a new workshop, use git to create a branch from this (workshop-template) branch.
- Rename the workshop-template folder in your new branch to the title of your new workshop, observing the naming convention of the rest of the folders in the repository
- Rename the lab guide md files to be more specific to your workshop, if desired.
- Update manifest.json with the titles and descriptions of your labs (and md filenames if you changed them).
- Select theme choice for your manifest.json - current choices are: "default", "ttc"
- Update the manifest.json with your interactive tour link (Note that by removing this in the JSON the tour launcher will be hidden)
- Use LabGuide100.md as an example of how to format and structure your lab's markdown.
- Preview your lab guides by loading index.html in your favorite editor's live view (Brackets - Live Preview, Atom - atom-live-server)

## Supporting Files

- README
    - The README.md file (this file) should give a clear step-by-step overview of what the student should do to complete the workshop, beginning with any prerequisite checks or software installation (detailed in the Student Guide)
    - **Do not include this 'Tips for Workshop Developers' section in the final workshop readme**
    - An example readme follows these tips, it can be modified for your workshop
- Student Guide
    - An example student guide has been provided, but it should be modified for the requirements of this workshop.
    - It should document where to get and how to install any required software
    - Any networking settings likely to need attention should be discussed in the guide
- Images
    - Store lab images under the images/x00 folder corresponding to the lab number they belong to.
    - Images that are used in multiple lab guides can be stored directly in the images/ folder.

# Example Readme:
## IMPORTANT: How to prepare for this workshop

**First**, ***Get an Oracle Cloud Account***
- Oracle provides several methods for gaining access to Oracle Cloud Accounts used to complete the Labs in this Hands-on-Workshop.
    - For some workshop events, cloud environments will be provided.
    - For others events (e.g. **Oracle Code**), or when completing this workshop in a self-service model, you must gain access to your own Trial account. Trial accounts can be obtained at [Try It](http://cloud.oracle.com/tryit)
    - If you are attending an Oracle sponsored event, please **review your Event invitation** for more instruction on how to gain access to your Workshop Account.

**Second**, ***Configure your Client Environment***
- Your client enviroment **must be configured prior** to attempting the Hands-on-Workshop labs.
- You have two options for configuring your workshop client environment.
     - ***Option 1:*** You can install Virtual Box and download and run a pre-configured **Virtual Box Image**.
     - ***Option 2:*** You can **install and configure** Eclipse, Brackets and Git on your laptop.
- Both **Option 1 and 2 are documented** in the [Student Guide](StudentGuide.md). ***Please follow the instruction in the Student Guide*** prior to attempting the Labs.

## How to View the Lab Guides

- The Labguides are best viewed using the Workshop's [GitHub Pages Website URL](https://derekoneil.github.io/cloud-native-devops-workshop/microservices)

- Once you are viewing the Workshop's GitHub Pages website, you can see a list of Lab Guides at any time by clicking on the **Menu Icon**

    ![](images/WorkshopMenu.png)  

- To log issues and view the Lab Guide source, go to the [github oracle](https://github.com/derekoneil/cloud-native-devops-workshop/tree/master/microservices) repository.

- Visit the [Workshop Interactive Labguide](http://launch.oracle.com/?cloudnative) for a visual overview of the workshop content.

## WLS On-Prem to ACCS Workshop

This Oracle Public Cloud DevOps WLS On-Prem to ACCS Workshop will walk you through o understand the movement on a Java EE application from their on-prem WLS deployment to Oracle's Cloud, during which you will create and deploy Jave EE war files. During this workshop you will take on the role of 2 personae. As the first persona - DevOps Manager - you will create the projects, add tasks and features to be worked on, and assign tasks to developers.  The Project Manager will then start the initial sprint. The Java Developer persona will develop a new twitter feed service that will allow for retrieval and filtering of twitter data. The Deployment Engineer persona will deploy a new Twitter Feed UI that will display the twitter data to allow for analysis.  During the workshop, you will get exposure to Oracle Developer Cloud Service and Oracle Application Container Cloud Service.

## Workshop Details

**Reference the following Lab Guides by opening their Documentation Files:**

## Lab 100: Overview of App in On-prem simulation

**Documenation**: [LabGuide100.md](LabGuide100.md)

### Objectives

- Create Initial Project
    - Add Users to Project
- Create Product Issues
    - Create Issues for Twitter Feed Microservice
    - Create Issues for Twitter Feed Marketing UI
- Create Agile Board and initial Sprint
- Add Issues to Sprint

## Lab 200: Redeploy both Components to ACCS

**Documenation**: [LabGuide200.md](LabGuide200.md)

### Objectives

- Deploying the Application to the Oracle Application Cloud Service Instance
- Verifying the Application Deployment

## Lab 300: Deploy to JCS

**Documenation**: [LabGuide300.md](LabGuide300.md)

### Objectives

- Move on premise WLS to Oracle JCS.
  - Create database instance
  - Create JCS instance
  - Move application to JCS

