![](images/100/lab100.png)

Update May 2, 2017

## Introduction

This is the first of several labs that are part of the Oracle Public Cloud GoldenGate Cloud Service workshop. These labs will give you a basic understanding of the Oracle GoldenGate Cloud Service and many of the capabilities around real time data replication and migration.  Throughout the workshop the following use cases will be covered.  These will be covered in more detail in labs 200, 300, and 400.  In lab 500 you will review GGCS monitoring.

- Lab 200: Migration and replication of data from an on-premise 11g database to a DBCS 12c multi-tenant database:

	![](images/100/i2.png)

- Lab 300: Replication of data from a DBCS 12c multi-tenant database back to an on-premise 11g datbase:

	![](images/100/i3.png)

- Lab 400: Replication and transformation of data from a DBCS 12c pluggable database to a DBCS 12c reporting data warehouse with Business Intelligence analytics access:

	![](images/100/i4.png)

This lab will:
- Familiarize you with the Oracle Cloud environment and services that will be used in the following labs.
- Familiarize you with an on-premise 11g Database environment that will be replicated to a DBCS 12c environment.  Note: this is set up as an image running in Oracle IAAS/compute, but process and configuration steps are the same as though the image was running outside the cloud.
- Walk through the steps to create a GoldenGate Cloud Service that will manage data replication between on-premise and cloud environments, and manage replication between different cloud environments.
- Walk you through creating a new GoldenGate enabled Database Cloud Service.

	Not sure this will be in lab 100:  "You will then VNC into the Oracle GoldenGate (OGG) 'on-premise' image desktop and review the OGG configuration.  You will also set up the SQL Developer connections to the source 11g and target 12c databases and review the source data that will be replicated.  Next you will connect to the GGCS and review the environment and configuration.then connect to the database image using the ssh private key and familiarize yourself with the image layout. Next you will learn how to create an ssh configuration file that can be used to tunnel simultaneously multiple ports to a remote OPC instance. Using the tunnels, you will learn how to access various Database consoles."
 
- To log issues and view the Lab Guide source, go to the [github oracle](https://github.com/pcdavies/GoldenGateCloudService/tree/master/workshops/goldengate) repository.

## Objectives

-   Create a GoldenGate Cloud Service

-   SSH Configuration

-   Explore VM and Consoles

## Required Artifacts

-   The following lab requires a VNC Viewer to connect to an Image
    running on Oracle's IaaS Compute Service.

## Review Cloud Services

### **STEP 1**: Login to your Oracle Cloud account and Review Services

-   Open a browser and go to the following URL:

	https://cloud.oracle.com

-   Click **Sign In** in the upper right hand corner of the browser

	![](images/100/i5.png)

- **IMPORTANT** - Under my services, select from the drop down list the correct data center and click on **My Services**. If you are unsure of the data center you should select, and this is an in-person training event, ***ask your instructor*** which **Region** to select from the drop down list. If you received your account through an Oracle Trial, your Trial confirmation email should provide a URL that will pre-select the region for you.

	![](images/100/i6.png)

-   Enter the **identity domain** and click **Go**

	**NOTE**: The **Identity Domain, User Name** and **Password** values will be given to you from your instructor.

	![](images/100/i7.png)

-   Once your Identity Domain is set, enter your User Name and Password and click **Sign In**

	**NOTE**: the **Identity Domain, User Name** and **Password** values will be given to you from your instructor.

	![](images/100/i8.png)

-   You will be presented with a Dashboard summarizing all of your available services.

	![](images/100/i9.png)

-   If all of your services are not visible, **click** on **Customize Dashboard.** You can then add services to the dashboard by clicking **Show**. If you do not want to see a specific service click **Hide**.

	![](images/100/i10.png)

- Review services that will be used in the GGCS Labs:
	- The Compute node will serve as your on-premise 11g database instance.  It will be migrated in Lab 200 to a target DBCS 12c pluggable databse in lab 200, and a GG target (reverse data replication) in lab 300.
	- The Database Service (DBCS) will be a GG target in lab 200 and a GG source in lab 300.
	- The GGCS instance is not yet in your identity domain.  You will create and configure this in Labs 200 - 500.
	- Finally note that BICS is not available in this identiity domain.  That will be provided in a separate Identity Domain.

	![](images/100/i11.png)

### **STEP 2**: Gather Information Required for Access to Images and GG Configuration

- Select the Database Cloud Service:

	![](images/100/i12.png)

- Open the Service Console:

	![](images/100/i13.png)

- Select the DBCS12c Service: 

	![](images/100/i14.png)

- Note the Public IP (**write this down**).  Also note the Service Name (DBCS12c - you will need this when creating GGCS)

	![](images/100/i15.png)

- Exit back out the the Cloud Dashboard:

	![](images/100/i16.png)

- Select the Compute Image:

	![](images/100/i17.png)

- Then open Service Console:

	![](images/100/i18.png)

- Identity Domains will have multiple sites. Please ask you instructor which site the Client Image is running on. If needed, click the Site drop down to access the Site Selector, and choose the correct site.

	![](images/100/i19.png)

- Note the public IP of the GG_On-premise image (**write this down**):

	![](images/100/i20.png)

### **STEP 3**: Create GoldenGate Cloud Service Instance

- Return to Dashboard (upper right), select GGCS, then Open Service Console, and then Create Service Instance:

	![](images/100/i21.png)

- Enter Service Name ggcsservice-ggcs-1 as the name, take the defaults and then hit Next:

	![](images/100/i22.png)

- Enter the following details:

	![](images/100/i23.png)

- Hit 'Next' and then submit.  The instance create process will take several minutes.

### **STEP 4**: Review Compute Image (On-premise OGG)

For the GoldenGate Cloud Service Workshop we will be using a compute Image that will represent your on-premises environment. In this image we have installed a 11g database that we will be migrating to our Oracle Public Cloud Database instance. The image also contains SQL Developer 4.1 that will be used to connect to both your local and cloud database.

- Start your vnc viewer and enter the IP address of the Compute image noted above.  Enter the cloud login password.

	![](images/100/i24.png)



-