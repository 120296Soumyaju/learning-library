# Lab 050: Setup Cloud Environment

  ![](images/050/Title.png)

## Introduction

In Lab 50 (as Derek) you will initiate the Oracle cloud environment that you will use to create and deploy your microservices applications. This environment will be contained within a cloud Compartment, and communication within the Compartment will be via a Virtual Cloud Network (VCN). The Compartment and VCN will isolate and secure the overall environment. You will deploy two Oracle Cloud Services for this environment. An Oracle Cloud Developer Image will be used to develop and deploy your microservices code. The microservices will access data within an Autonomous Transaction Processing (ATP) Cloud Service. 

***To log issues***, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

***We recommend that you create a notes page to write down all of the credentials you will need***

## Lab 050 Objectives

- Setup your IAAS environment and create common components.
- Create a new Cloud Developer Image from Marketplace.
- Create an Autonomous Transaction Processing (ATP) Database.
- Install Visual Studio Code into the Cloud Developer Image.

## Steps

### **STEP 1:** Your Oracle Cloud Trial Account

You have already applied for and received your Oracle Cloud Free Tier Account.

### **STEP 2:** Log in to your OCI dashboard

- From any browser go to oracle.com to access the Oracle Cloud.

    [https://www.oracle.com/](https://www.oracle.com/)

    ![](images/login-screen.png)

- Click the icon in the upper right corner.  Click on **Sign in to Cloud** at the bottom of the drop down.   *NOTE:  Do NOT click the Sign-In button, this will take you to Single Sign-On, not the Oracle Cloud*

    ![](images/signup.png)   
 
- Enter your **Cloud Account Name** in the input field and click the **Next** button.

  ![](images/050/002.png)

    `Note this is NOT your email. This is the name of your tenancy noted in the email you received during signup`
- Enter your username (this may be your email address) and password and click on **Sign In**.
  ![](images/050/003.png)

- Once you log in you will see a page similar to the one below.  Click on the hamburger icon in the upper left corner to reveal the menu.

    ![](images/hamburger.png)  

### **STEP 3:** Get Your Oracle Cloud Credentials

In order to use Terraform, you will need a few different credentials which can be found on the OCI console.

- Click the **Menu icon** in the upper left corner to open the navigation menu. Under the **Governance and Administration** section, select **Identity** and select **Users**.

  ![](images/050/011.png)

- Click on your username. It will usually be in the format **oracleidentitycloudservice/username**.

  ![](images/050/012.png)

- Click **Copy** next to OCID, and save this as your **User OCID** in your notes. Next, click on the profile icon in the top right. Then click into the tenancy link.

  ![](images/050/013.png)

- Click **Copy** next to OCID, and save this as your **Tenancy OCID** in your notes. Then, copy the **Object Storage Namespace** in your notes.

  ![](images/050/014.png)

- Click the **Menu icon** in the upper left corner to open the navigation menu. Under the **Governance and Administration** section, select **Identity** and select **Compartments**.

  ![](images/050/032.png)

- Click on the OCID next to your root tenancy, then click **Copy**, and save this as your **Compartment OCID** in your notes.

  ![](images/050/033.png)

- Finally, go back to the home console and make a note of your default region. For example, if your region is US West (Phoenix), note down Phoenix in your notes.

  ![](images/050/031.png)


### **STEP 4:** Download and Install Terraform

See these instructions for [Download and Install of Terraform](https://learn.hashicorp.com/terraform/getting-started/install.html).

`Make sure to review the page before starting. Then verify that terraform was installed.`


### **STEP 5:** Download and Install the OCI CLI

Before downloading, make sure you meet the [requirements](https://docs.cloud.oracle.com/iaas/Content/API/Concepts/cliconcepts.htm#Requirements) to install the OCI CLI.

See these instructions for [Download and Install of CLI](https://docs.cloud.oracle.com/iaas/Content/API/SDKDocs/cliinstall.htm).

**Make sure to review the whole page before starting.**

- Once you have the CLI installed,

    run `$ oci setup config`

    ![](images/050/020.png)

    Press enter to choose the default location for the config file

    ![](images/050/021.png)

    Then enter the **User OCID** you saved earlier and press enter

    ![](images/050/030.png)

    Repeat the process, but with your **tenancy OCID**

    ![](images/050/022.png)

    Enter the [home region](https://docs.cloud.oracle.com/iaas/Content/General/Concepts/regions.htm) you noted earlier.

    ![](images/050/023.png)

    Enter Y to generate a new RSA key pair, then press enter to choose default values for the rest of the options

    ![](images/050/024.png)
    ![](images/050/025.png)

    Finally, run

    `$ ls ~/.oci`
    
    Verify that your files are there

    ![](images/050/026.png)

### **STEP 6:** Generate your SSH key pair

- On linux or a Mac enter this in a command shell.
    
    `$ ssh-keygen -b 2048 -t rsa`

    You can call the key whatever you want (the default is easiest).  It will create a private key and a public key. The public key is used when you are prompted for a SSH key when you create services, and the matching private key is used to access those services after creation. (eg: Cloud Developer Image).

    ![](images/050/028.png)

- On Windows, follow these [instructions](https://www.ssh.com/ssh/putty/windows/puttygen).
    You can call the key whatever you want (the default is easiest).  It will create a private key and a public key. The public key is used when you are prompted for a SSH key when you create services, and the matching private key is used to access those services after creation. (eg: Cloud Developer Image). 

	
### **STEP 7:** Prepare Terraform Script

- First, create a folder on your computer to hold the files.
    
    `$ mkdir OCI-terraform && cd OCI-terraform`

    ![](images/050/015.png)

- Then, [download](https://github.com/edercervantes/terraform-OCI) zip file for the Terraform script.

    ![](images/050/016.png)

    Add the zip file to your new folder. Then unpack it.

- Go into the new folder
    `$ cd terraform-OCI-master`

**Note: For the next steps, you can also use your IDE of choice or any text editor.**

`Open the config file you created earlier when you set up the OCI CLI. This contains most of the info you will need in the following steps.`

- In the folder terraform-OCI-master, open env.vars

    `$ nano env.vars`

    ![](images/050/017.png)

- Paste in the information matching the values in your notes/config file, then save.

- Next, open variables.tf

    Go to the OBJECT_STORAGE section and change the default value for obj_store_namespace to yours.

    ![](images/050/027.png)

<!--
![](images/050/018.png)
![](images/050/018.1.png)
![](images/050/019.png) -->

### **STEP 7:** Create Resources

- In the terminal, make sure you are inside the terraform-OCI-master folder

- Run the following commands

    `$ terraform init`
    `$ source env.vars`
    `$ terraform plan`
    `$ terraform apply`

    When prompted, input yes and hit enter.

### **STEP 8:** Connect to your marketplace developer image

[See this link for more info](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/54030984).  This info is copied below.

- Navigate to `Compute` > `Instances` and select your image to identify the IP address

	![](images/050/034.png)

- Identify the IP address.  You will use this to ssh to the image.

	![](images/050/035.png)

- SSH to the image. 
    **Note if you are on Windows you will need to use putty.**
    Open a terminal window on a Mac or command shell on Linux and enter the following command: 
    `$ ssh -i privateKey opc@<your IP address>`.  

	![](images/050/036.png)

- Enter `$ vncpasswd` to set your VNC access (make it a secure one!).

	![](images/050/037.png)

- Enter `$ vncserver` to start the vncserver.

	![](images/050/038.png)

- Enter `$ exit` to go back to your local directory.

- Open a SSH tunnel.
    ***NOTE:*** do not close this terminal window.  It maintains the tunnel to the developer image, which we access through VNC.  If for whatever reason the window is closed or you are otherwise logged out (sometimes tunnels drop), then just run this again to log in.
    
    For Windows, follow these [instructions](https://www.skyverge.com/blog/how-to-set-up-an-ssh-tunnel-with-putty/) for information on how to create a tunnel on Windows.

     This example works on Linux and the MAC. Note: on Linux you will need to be su.

     `$ ssh -i <your private key> -L 5901:localhost:5901 opc@<your marketplace compute IP>`

    ![](images/050/039.png)

- Open a vnc viewer session.  If you don't already have vncviewer you can download it [here](https://www.realvnc.com/en/connect/download/viewer/).

	![](images/050/040.png)

	![](images/050/041.png)

### **STEP 9:** Download Files Used in this Workshop

**Click to Download.  Save the file to your Downloads directory.**

[lab-resources.zip](https://oracle.github.io/learning-library/workshops/python4atp/lab-resources.zip)

**This completes the Lab!**

**You are ready to proceed to [Lab 100](LabGuide100.md)**
