
# ReservedIP Practice - Using Reserved Public IP 
  
## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[ReservedIP-Practice 1: Sign in to OCI Console and Create Reserved Public IP](#ReservedIP-practice-1)

[ReservedIP-Practice 2: Assign reserved public IP to first compute instance](#ReservedIP-practice-2)

[ReservedIP-Practice 3: ssh to compute instance using Reserved Public IP](#ReservedIP-practice-3)

[ReservedIP-Practice 4: Un-assign Reserved Public IP](#ReservedIP-practice-4)

[ReservedIP-Practice 5: Create a second compute instance and assign the same Reserved Public IP](#ReservedIP-practice-5)

[ReservedIP-Practice 6: Delete the resources](#ReservedIP-practice-6)
## Overview

Oracle Cloud Infrastructure Reserved Public IP service is an internet-scale, high-performance storage platform that offers reliable and cost-efficient data durability. The Reserved Public IP service can store an unlimited amount of unstructured data of any content type, including analytic data and rich content, like images and videos.

With Reserved Public IP, you can safely and securely store or retrieve data directly from the internet or from within the cloud platform. Reserved Public IP offers multiple management interfaces that let you easily manage storage at scale.

Reserved Public IP is a regional service and is not tied to any specific compute instance. You can access data from anywhere inside or outside the context of the Oracle Cloud Infrastructure

The purpose of this lab is to give you an overview of the Reserved Public IP Service and an example scenario to help you understand how the service works.

## Pre-Requisites

- Oracle Cloud Infrastructure account credentials (User, Password, Tenant, and Compartment)  

## Reserved IP-Practice-1 
### __Sign in to OCI console and create Reserved Public IP__

**Overview**

In this practice, you sign in to the Oracle Cloud Infrastructure console using your credentials and create Object Storage  .

Assumptions

Oracle Cloud Infrastructure account credentials (User, Password, Tenant, and Compartment) are available

**Note:** OCI UI is being updated thus some screenshots in the instructions might be different than actual UI

**Before You Begin**

- We recommend using Chrome or Edge as the broswer. Also set your browser zoom to 80%

Ensure you have below information available:

- Tenant, User name, Password, and compartment name

**Duration: 10 minutes**

**Tasks**

**1** -  Sign in to OCI Console and Create VCN and reserved public IP 

a) Sign in using your tenant name, user name and password.

b) Once signed in select the compartment assigned to you from drop down menu on left part of the screen

c) From the OCI Services menu,click **Virtual Cloud Network** under Networking and click **Create Virtual Cloud Network**

**NOTE:** Ensure the correct Compartment is selected under COMPARTMENT list
![]( img/RESERVEDIP_HOL001.PNG)
![]( img/RESERVEDIP_HOL002.PNG)

Fill out the dialog box:

**Create in Compartment:** Has the correct compartment

**Name:** Enter easy to re¬member name

**Create Virtual Cloud Network Plus Related Resources:** Select this option.

Click **Create Virtual Cloud Network**

Click **Close**

![]( img/RESERVEDIP_HOL003.PNG)
![]( img/RESERVEDIP_HOL004.PNG)

d) From **Networking** screen click **Public IPs** , then **Create Resrved Public IP** and Fill out the dialog box:

**COMPARTMENT:** Ensure correct compartment is selected
**NAME:** Provide a name (optional)

Click **Create Reserved Public IP**

![]( img/RESERVEDIP_HOL005.PNG)

## Reserved IP-Practice 2: 
### __Assign reserved public IP to first compute instance__

#### Overview

In this section we will first create a ssh key pair, launch a compute instance and assign the reserved Public IP to it. We will then verify access to this compute instance using the reserved Public IP

**Before You Begin**

You should have completed ReserverIP-Practice-1

**Duration: 10 minutes**

**Tasks**

**1** - Open built in Git bash application and generate ssh keys

a) Click the Apps icon in the toolbar and select  Git-Bash to open a terminal window.

![]( img/RESERVEDIP_HOL006.PNG)

b) Enter command **ssh-keygen**

**HINT:** You can swap between OCI window, 
git-bash sessions and any other application (Notepad, etc.) by clicking the Switch Window icon 
![]( img/RESERVEDIP_HOL007.PNG)

c) Press Enter When asked for ‘Enter File in which to save the key’, ‘Created Directory, ‘Enter passphrase’, and ‘Enter Passphrase again.
![]( img/RESERVEDIP_HOL008.PNG)

d) You should now have the Public and Private keys:
/C/Users/ PhotonUser/.ssh/id_rsa (Private Key)
/C/Users/PhotonUser/.ssh/id_rsa.pub (Public Key)
**NOTE:** id_rsa.pub will be used to create 
Compute instance and id_rsa to connect via SSH into compute instance.

**HINT:** Enter command **cd /C/Users/PhotonUser/.ssh** (No Spaces) and then **ls** to verify the two files exist. 

e) In git-bash Enter command  
**cat /C/Users/PhotonUser/.ssh/id_rsa.pub** , highlight the key and copy 
![]( img/RESERVEDIP_HOL009.PNG)

f) Click the apps icon, launch notepad and paste the key in Notepad (as backup)
![]( img/RESERVEDIP_HOL0010.PNG)

g) Switch to the OCI console. From OCI servies menu, Click **Instances** under **Compute** 

e) Click Create Instance. Fill out the dialog box:

**Name:** Enter a name 

**Availability Domain:** Select the first available domain.(usually AD1)

**Image Operating System:** For the image, we recommend using the Latest Oracle Linux available.

**Choose Instance Type:** Select Virtual Machine

**Choose Instance Shape:** Select VM.Standard.E.2.1

**Configure Boot Volume:** Leave the default

**Add SSH Keys:** Choose ‘Paste SSH Keys’ and paste the Public Key saved earlier.

**Virtual Cloud Network Compartment:** Choose your compartment

**Virtual Cloud Network:** Select the VCN you created in the previous section. 

**Subnet Compartment:** Choose your compartment. 

**Subnet:** Choose the first Subnet

f) Click **Create**
![]( img/RESERVEDIP_HOL0011.PNG)

g) Once the instance is in Running state, click Instance name

h) In the instance detail page Click **Attached VNICs** and then VNIC name
![]( img/RESERVEDIP_HOL0012.PNG)

i) In VNIC detail page Click Action icon and then **Edit**
![]( img/RESERVEDIP_HOL0013.PNG)

j) In the dialog box under Public IP Address choose
RESERVED PUBLIC IP, from the drop down list select
the Reserved Public IP created earlier. Click **Update**

k) Note down the Public IP address.

***We have successfully assigned a Reserved Public IP address to the compute instance***

## Reserved IP-Practice 3: 
### __ssh to compute instance using Reserved Public IP__

#### Overview

In this section we will ssh into the Compute instance using Reserved Public IP address and private ssh key


**Before You Begin**

You should have completed ReserverIP-Practice-2

**Duration: 5 minutes**

**Tasks**

**1** - Use built in git bash application to ssh to compute instance

a) In git-bash type cd /C/Users/PhotonUser/.ssh

b) Enter **ls** and verify id_rsa file exists

c) Enter command **ssh –i id_rsa opc@<PUBLIC_IP_OF_COMPUTE_INSTANCE>**

**NOTE:** User name is opc

**HINT:** If ‘Permission denied error’ is seen, ensure you are using ‘-i’ in the ssh command

d) Enter ‘Yes’ when prompted for security message
![]( img/RESERVEDIP_HOL0014.PNG)
 
e) Verify opc@<COMPUTE_INSTANCE_NAME(reserved-ip-instance1 in this case) appears on the prompt

***We successfully ssh into the compute instance using the reserved public IP. Next we will use the same Public IP and assign it to a different Compute instance***

## Reserved IP-Practice 4: 
### __Un-assign Reserved Public IP__

#### Overview

In this section we will us-assign the Reserved Public IP address.


**Before You Begin**

You should have completed ReserverIP-Practice-3

**Duration: 5 minutes**

**Tasks**

**1** - Unassign the reserved Public IP from the compute instance

a) From OCI services menu, Click **Instances** under Compute, Click your instance name

b) In the instance detail page Click **Attached VNICs**, and  then VNIC name

c) In VNIC detail page Click Action icon and then **Edit**

d) In the dialog box under Public IP Address choose 
**NO PUBLIC IP** (Note the Warning message indicating
Reserved Public IP will be unassigned) . Click **Update**
![]( img/RESERVEDIP_HOL0015.PNG)

***Reserved Public IP has now been un-assigned from this compute instance. Next we will create a new compute instance and assign this same Public IP to it.***

## Reserved IP-Practice 5: 
### __Create a second compute instance and assign the same Reserved Public IP. Verify the operation by ssh into second compute instance__

#### Overview

In this section we will re-assign the Reserved Public IP address to a second compute instance and ssh into it.


**Before You Begin**

You should have completed ReserverIP-Practice-4

**Duration: 10 minutes**

**Tasks**

**1** - Create a second compute instance, Re-assign the reserved Public IP 

a) From OCI servies menu, Click **Instances** under Compute 

b) Fill out th dialog box as done earlier to create second compute instance

c) Once the instance is in Running state, click Instance name

d) In the instance detail page Click **Attached VNICs**, and then VNIC name

e) In VNIC detail page Click Action icon and then **Edit**

f) In the dialog box under Public IP Address choose 
RESERVED PUBLIC IP, from the drop down list select 
the Reserved Public IP created earlier. Click **Update**

**2** - ssh into compute instance

a) In git-bash type cd /C/Users/PhotonUser/.ssh

b) Enter **ls** and verify id_rsa file exists

c) Enter Command **ssh -o GlobalKnownHostsFile=/dev/null -o  UserKnownHostsFile=/dev/null  –i id_rsa opc@<PUBLIC_IP_OF_COMPUTE_INSTANCE>**
**NOTE:** We are specifying additional options since this sameIP was used for a different compute instance earlier.

d)  Enter ‘Yes’ when prompted for security message

e) Verify opc@<COMPUTE_INSTANCE_NAME> 
(reserved-ip-instance2 in this case) appears at the 
prompt

## Reserved IP-Practice 6: 
### __Delete the resources__

#### Overview

In this section we will delete the resources


**Before You Begin**

You should have completed ReserverIP-Practice-5

**Duration: 5 minutes**

**Tasks**

**1** - Delete compute instance, reserved IP and VCN

a) Switch to  OCI console window

b) If your Compute instance is not displayed, From OCI services menu Click Instances under Compute

c) Locate first compute instance, Click Action icon and then **Terminat** 
![]( img/RESERVEDIP_HOL0016.PNG)

d) Make sure Permanently delete the attached Boot Volume is checked, Click Terminate Instance. Wait for instance to fully Terminate
![]( img/RESERVEDIP_HOL0017.PNG)

e) Repeat steps to delete the second compute instance

f) From OCI services menu Click **Virtual Cloud Networks** under Networking, list of all VCNs will 
appear.

g) Locate your VCN , Click Action icon and then **Terminate**. Click **Delete All** in the Confirmation window. Click **Close** once VCN is deleted
![]( img/RESERVEDIP_HOL0018.PNG)

h) From OCI services menu Click **Networking**, then **Public IPs**, locate the Reserved Public IP you created. Click Action icon and then **Terminate**
![]( img/RESERVEDIP_HOL0019.PNG)

***Congratulations! You have successfully completed Using Reserved Public IP address lab. In this lab you created a VCN, Reserved a Public IP, Created 2 compute instances and assigned the same Public IP to both the instance one at a time.  This lab demonstrated the option of using one IP to ssh or point to different compute instance***