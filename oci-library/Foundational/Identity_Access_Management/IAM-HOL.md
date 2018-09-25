# IAM Practice - Identity and Access Management
  
## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[IAM-Practice 1: Signing in to the Console ](#iam-practice-1)

[IAM-Practice 2: Managing Users, Groups and Policies to Control Access](#iam-practice-2)


## Overview

Oracle Cloud Infrastructure Identity and Access Management (IAM) Service lets you control who has access to your cloud resources. You control the types of access a group of users has and to which specific resources.

The purpose of this lab is to give you an overview of the IAM Service components and an example scenario to help you understand how they work together.

## Pre-Requisites

- Oracle Cloud Infrastructure account credentials (User, Password, and Tenant)  

## IAM-Practice-1 
### __Signing in to the Console__

**Overview**

In this practice, you sign in to the Oracle Cloud Infrastructure console using your credentials.

Assumptions

**Note:** Some of the UIs might look a little different than the screenshots included in the instructions, but you can still use the instructions to complete the hands-on labs.

**Before You Begin**

To sign in to the Console, you need the following:

- Tenant, User name and Password

- URL for the Console: [https://console.us-ashburn-1.oraclecloud.com/](https://console.us-ashburn-1.oraclecloud.com/)

- Any browser from the supported browsers list (Recommended)

**Note:**

- **For this lab we use _cloud.admin_ and <your-name@domain.com> as the user name to demonstrate the scenarios. You must use your cloud.admin when you perform these tasks.**

- Oracle Cloud Infrastructure supports the latest versions of Google Chrome, Firefox and Internet Explorer 11.

- When you are provisioned, you will receive a customized URL for your organization. For example, https://console.us-ashburn-1.oraclecloud.com_?tenant="your-tenant-id"

- If you omit the tenant argument, the system will ask you to input your tenancy before you can log in.

**Duration: 5 minutes**

**Tasks**

**1** - Sign In

 a) Open a supported browser and go to the Console URL. For example, [https://console.us-ashburn-1.oraclecloud.com](https://console.us-ashburn-1.oraclecloud.com).

 b) Enter your tenant name: <Tenant> and click **Continue**

 ![]( img/image001.png)

 c) Oracle Cloud Infrastructure is integrated with Identity Cloud Services, you will see a screen validating your Identity Provider. You can just click **Continue**.

 ![]( img/image002.png)

 d) Enter your user name and password

 - **Username:** cloud.admin
 - **Password:** _instructor will provide password_

 ![]( img/image003.png)

When you sign in to the Console, the home page is displayed.

 ![]( img/image004.png)

The home page gives you quick links to the documentation and to Oracle Support.

## IAM-Practice-2 
### ***Managing Users, Groups and Policies to Control Access***

#### Overview

A user's permissions to access services comes from the _groups_ to which they belong. The permissions for a group are defined by policies. Policies define what actions members of a group can perform, and in which compartments. Users can access services and perform operations based on the policies set for the groups of which they are members.

We'll create users, groups, and policies to understand the concept.

**Before You Begin**

You should have completed IAM-Practice-1

**Duration: 20 minutes**

**Tasks**

**2** - Create a Group in Your Tenancy

   a) Sign in to the console, on the **Menu** click **Identity**, then select **Groups**.

   b) Click **Create Group**.

   c) In the **Create Group** dialog box, enter the following:

- **Name:** Enter a unique name for your group such as "oci-group” Note that the group name cannot contain spaces.
- **Description:** Enter a description (for example, “New group for oci users”).
- Click **Submit**.

![]( img/image005.png)

![]( img/image006.png)

**3** - Create a **Compartment** in Your Tenancy

   a) On the **Menu** click **Identity**, then select **Compartments**.

   b) Click **Create Compartment.**

   c) In the **Create Compartment** dialog box, enter the following:

 - **Name:** Enter a unique name for your compartment such as "OCI-Demo” Note that the compartment name cannot contain spaces.
 - **Description:** Enter a description (for example, “New compartment for oci demo”).
 - Click **Create Compartment**.

![]( img/image007.png)

**4** - Now, let’s **create a policy** that gives your group permissions in your assigned compartment. For example, creates a policy that gives permission to compartment OCI-Demo to members or group oci-group:

   a) On the **Menu** click **Identity**, and then click **Policies**.

   b) On the left side, select your **OCI-Demo** compartment.

   c) Click **Create Policy**.

   d) Enter a unique **Name** for your policy (For example, "Policy-for-oci-group") Note that the name can NOT contain spaces.

   e) Enter a **Description** (for example, "Policy for OCI Group").

   f) Enter the following **Statement**:

 `Allow group oci-group to manage all-resources in compartment OCI-Demo`

   g) Click **Create**.

![]( img/image008.png)

**5** - Create a New User

   a) On the **Menu** click **Identity**, and then click **Users**.

   b) Click **Create User**.

   c) In the **New User** dialog box, enter the following:

- **Name:** Enter a unique name or email address for the new user. For Example: yourname@oracle.com
    _This value is the user's login name for the Console and it must be unique across all other users in your tenancy._
- **Description:** Enter a description. For example, New oci user.

![]( img/image009.png)
    
   d) Click **Create**.

**6** - Set a Temporary Password for the Newly Created User

   a) From the list of users, click on **the user that you created** to display its details.

   b) Click **Create/Reset Password**.  
   
![]( img/image010.png)

   c) In the dialog, click **Create/Reset Password**.

![]( img/image011.png)

   d) The new one-time password is displayed.

![]( img/image012.png)

   e) Click the **Copy** link and then click **Close**. Make sure to copy this password to your notepad.

**7** - Sign out

   a) Click **Sign Out** from the user menu and log out of the cloud.admin user account.

![]( img/image013.png)

**8** - Sign in as the new yourname@oracle user using a different web browser window.

   a) Go to [https://console.us-ashburn-1.oraclecloud.com](https://console.us-ashburn-1.oraclecloud.com).

   b) Enter the Tenant name, if prompted.

   c) Sign in as yourname@oracle.com.

   d) Enter the password that you copied in [Task 4](#passwrdlabuser01).

![]( img/image014.png)

**Note:** _Since this is the first-time sign-in, the user will be prompted to change the temporary password, as shown in the screen capture._

   e) Set the new password to _Welc0me2*bmcs_. Click **Save New Password**.

![]( img/image015.png)

   f) yourname@oracle.com lands on the home page.

**9** -  Verify user permissions

   a) Go to the **Menu** click **Compute** and **Instances**.

   b) Select compartment OCI-Demo from the left menu, if it's not already selected.

   c) The message “**You don’t have access to this compartment**” appears.

![]( img/image016.png)

   d) Sign out of the Console.

**10** - Add User to a Group

   a) Sign in back as the cloud.admin using the Single Sign-on (SSO) option. Click **Identity** \> **Users**.

   b) From the **Users** list, click your user (for example, yourname@oracle.com)  to go to the user details page.

   c) Under the **Resources** menu on the left, click **Groups.**

   d) Click **Add User to Group**.

   e) From the **GROUPS** drop-down list, select the **oci-group** that you created.

   f) Click **Add**.

   g) Sign out.

**11** - Verify user permissions when a user belongs to a specific group

a) Sign in as yourname@oracle.com

b) Go to the **Menu** click **Compute** and **Instances**.

c) Select compartment **OCI-Demo** from the list of compartments on the left.

![]( img/image017.png)

d) There is no message related to permissions.

e) Go to the **Menu** click **Identity** and select **Groups.**

f) The message “You don’t have access to these resources” appears. This is expected, since your user has no permission to any groups.

g) Sign out.

