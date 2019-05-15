![](./media/adbtitle.png)
# Lab 1:  Connecting to Autonomous Database

## Table of Contents

- [Module 1: Create and monitor a sanctioned application](#module-1--create-and-monitor-a-sanctioned-application)
- [Module 2: Create a Policy Alert and Display Threats](#module-2--create-a-policy-alert-and-display-threats)


***** 

## Module 1:  Create and monitor a sanctioned application

The following hands-on labs assume that you are familiar with Oracle Cloud Platform console navigation, as well as access to Oracle CASB Cloud Service console.
In order to ease the process, we recommend using two separate browsers or windows.
We will enroll third-party services as part of the exercise and it's imperative to navigate back and forth between CASB and the vendors' dashboards to complete the lab.

Oracle CASB monitors your sanctioned applications after a simple registration process. This enables you to manage risk events from a centralized platform instead of having to enter the individual application to see and remediate security threats. Oracle CASB monitors risk events such as blacklisted IP addresses, anomalous user behavior and unwanted security configurations in the application.
As part of this first part of the module we will enrol two applications, Box and SalesForce.

### Add Box as a Sanctioned Application

1. Navigate to https://developer.box.com/
*  Click the Console button in the top right corner

![Box Console](./media/box_console.png)
<p align="center">Figure 1-1</p>

* Click Sign up

![Box Sign Up](./media/box_signup.png)
<p align="center">Figure 1-2</p>

* Select the section Individual Plans and click to Sign Up in the Individual account

![Box Select Plan](./media/box_selectplan.png)
<p align="center">Figure 1-3</p>

* Enter required information and click Submit, you will receive a verification email

![Box Verify Account](./media/box_verifyaccount.png)
<p align="center">Figure 1-4</p>


* Once you have the account for Box, you have to configure it for monitoring.

2. Now that you have create your developer account on Box, let's configure the service account for Monitoring

* Log in to developer.box.com
* Go to My Apps and create an application

![Box Create Application](./media/box_createapp_1.png)
<p align="center">Figure 1-5</p>


* Select Custom App and click next

![Box Create Application](./media/box_createapp_2.png)
<p align="center">Figure 1-6</p>

* Select the recommended authentication method OAuth 2.0 with JWT (Server Authentication) and click next

![Box Create Application](./media/box_authentication.png)
<p align="center">Figure 1-7</p>


* Give an unique name to your app and click Create App

![Box Create Application](./media/box_uniquename.png)
<p align="center">Figure 1-8</p>


* Click on your new application, and in the section Configuration, select the following:

  1. Authentication Method: OAuth 2.0 with JWT (Server Authentication)
  ![Box Config app](./media/box_appconfig_1.png)
<p align="center">Figure 1-9</p>

  2. Application access: **Enterprise**
  ![Box Config app](./media/box_appconfig_2.png)
<p align="center">Figure 1-10</p>

  3. Save your changes. An Admin Console tab is now added to your main Box.com account.

3. Create the Dedicated Oracle CASB Cloud Service User
    * Create a dedicated user for Oracle CASB Cloud Service in the Box account that you want to monitor. This user is dedicated for use by Oracle CASB Cloud Service and shouldn’t be used for any other purpose.
    * Log in to the Box developer account.
    * Select the Admin Console tab.
    * Click the Users & Groups section.
    * Click the + Users button.


 ![Box Config app](./media/box_usercreation.png)
<p align="center">Figure 1-11</p>


* In the Name field, give the service account an identifier (example: occs.trialservice).
* If you are going to be the tenant master administrator for Oracle CASB Cloud Service, then provide your email address in the Email field and click **Add User**
* Open the recently created user and grant this user the Co-Admin role. This account must have either the Admin or Co-Admin role.

 ![Box Config app](./media/box_useredit.png)
<p align="center">Figure 1-12</p>

* Assign additional privileges to this user.
At a minimum, the user should be able to run new reports and access existing reports. If you want to be able to push security controls from Oracle CASB Cloud Service to this Box instance, then this user must also have these privileges:

`Users and Groups: Manage users`

`Users and Groups: Manage groups`

`Reports and Settings: View settings and apps for your company`

`Reports and Settings: Edit settings and apps for your company`

`Reports and Settings: Run new reports and access existing reports`

![Box Config user](./media/box_priv.png)
<p align="center">Figure 1-13</p>


* Click *Save*


* In the users list you should be able now to see the Oracle CASB Cloud Service user that you just created.

![Box New Account](./media/box_newaccount.png)
<p align="center">Figure 1-14</p>


* Check the email account that you provided for that user.
You should have a message from Box telling you to set a password for this user.

![Box Verification](./media/box_password_verification.png)
<p align="center">Figure 1-15</p>

* Create a complex password for this account.
For example, at least 12 characters in length, with a combination of uppercase and lowercase letters, numbers, and special characters.

![Box New Password](./media/box_newpassword.png)
<p align="center">Figure 1-15</p>


* You will use this user name and password to register your Box instance in Oracle CASB Cloud Service. Have a recovery procedure in case there are issues with the account.


4. Adding a Box instance (Push Security Controls Mode)

* You will add or register your Box instance to Oracle CASB Cloud Service to be monitored, and with the capability to push security configuration settings.
To register a Box instance with the Oracle CASB Cloud Service, you need the user ID and password that belongs to a Box administrator with the appropriate privileges in the account that you want to monitor. This user must be dedicated to the Oracle CASB Cloud Service. We will use the co-admin user that we created in the previous steps.

* In push security controls mode, Oracle CASB Cloud Service checks various security control values in the Box instance, and sets them to the values that you set at registration time. Later, you receive notifications when these security configuration settings change.

* Oracle CASB Cloud Service monitors these settings in Box:

  * Password policies, authentication policies, and session settings: These are in the Box business settings page, Security tab.
  * Settings: These additional security settings are in the Box business settings page, Content & Sharing tab.


* Login to your Cloud dashboard and open Oracle CASB Cloud Service console
* Select Applications from the Navigation menu.
* Click **Add/Modify App**
* In the Select an app type page, click the icon for box and click Next.


![CASB add box](./media/casb_addbox.png)
<p align="center">Figure 1-16</p>

* In the Select an instance page, enter a unique name for your application instance.

![CASB box name](./media/casb_boxname.png)
<p align="center">Figure 1-17</p>

* Click Next.
* In the Select monitoring type page, select Push controls and monitor to have Oracle
CASB Cloud Service set your preferred values in the application and subsequently monitor for deviations from these values.

![CASB box push config](./media/casb_boxpush.png)
<p align="center">Figure 1-18</p>

* Oracle CASB Cloud Service generates a security control alert in Risk Events whenever it detects a mismatch between the selections that you make on this page and the settings in the Box instance.

* Click Next.

* In the Select security controls page, select the Standard security controls. In this mode, you will ensure that these values are set to the application's own defaults.
* Select the checkbox.

![CASB box security controls](./media/casb_box_securitycontrols.png)
<p align="center">Figure 1-19</p>

* Click Next.
* In the Enter credentials page, select Sign in with Box username and password.
* Enter the credentials for the dedicated co-admin user that you set up to communicate with Oracle CASB Cloud Service.
  * User name. The username of the Oracle CASB Cloud Service user.
  * Password. The password of the Oracle CASB Cloud Service user.

![CASB box testing credentials](./media/casb_box_credentials.png)
<p align="center">Figure 1-20</p>

* When you are done entering your credentials, click Test Credentials. A new window pops up to ask you if you set the right permissions for that user in your Box account. Click Ok.

![CASB box accept credentials](./media/casb_box_credentials_2.png)
<p align="center">Figure 1-21</p>

* It can take a minute or two for the application to receive and accept your credentials.
* When testing is done, you see a success message.
* Click **Submit**
* Click **Done**
* When the registration process is complete, your application instance appears on the Applications page. You start to see data for this instance after 30 minutes or so; although a complete synchronization will take longer.

****

### Add SalesForce as a Sanctioned Application

You’ll now add SalesForce as a sanctioned application for monitoring in Oracle CASB, so this business critical application remains compliant with security standards.

1. Navigate to https://developer.salesforce.com/
    * Click the sign-up button in the top right corner
    * Enter the required information
    * Click Sign me up

![SF registration](./media/sf_registration.png)
<p align="center">Figure 1-22</p>


2. You will get an email to confirm your account. Click Verify Account


![SF verification](./media/sf_verification.png)
<p align="center">Figure 1-23</p>


3. Create a password for your account

![SF Create Password](./media/sf_password.png)
<p align="center">Figure 1-24</p>


4. Login to your Salesforce account.
5. On the left Panel navigate to Users => Profiles
    * Click new profile

![SF Create profile](./media/sf_profile.png)
<p align="center">Figure 1-25</p>

6. Existing Profile needs to be set to System Administrator and Profile Name can be named whatever you like, for example, CASBUSER.

![SF Set profile](./media/sf_setprofile.png)
<p align="center">Figure 1-26</p>

7. Press save

8. Navigate to Users => Users 
    * Click New User

![SF create user](./media/sf_createuser.png)
<p align="center">Figure 1-27</p>

9. The following Screen will appear. Fill in the required fields. User License must be set to Salesforce
    * Profile name will be the name of the profile we previously created
    * Save

![SF modify user](./media/sf_modifyuser.png)
<p align="center">Figure 1-28</p>


10. An email will be triggered allowing for verification

![SF verification](./media/sf_verification_newuser.png)
<p align="center">Figure 1-29</p>

11. Click to Verify account in the link attached in the email and fill password details for the new user. Now you will see the following:

![SF Dahsboard](./media/sf_dashboard.png)
<p align="center">Figure 1-30</p>

This is the last step we need to complete in SalesForce.

12. Now go to the CASB Console and select the SalesForce application to add the instance in Oracle CASB.

![CASB SF enrolment](./media/casb_sf_enroll.png)
<p align="center">Figure 1-31</p>

13. Enter a unique name for you instance. Click the checkboxes from the picture below. Click Next.

![CASB SF Unique name](./media/casb_sf_uniquename.png)
<p align="center">Figure 1-32</p>

14. Select Push controls and monitor

![CASB SF Push](./media/casb_sf_push.png)
<p align="center">Figure 1-33</p>

15. Select Standard Security Controls. Check Approval box and Press Next

![CASB SF security controls](./media/casb_sf_securitycontrols.png)
<p align="center">Figure 1-34</p>

16. You will redirected to the below page. Login with your User Credentials (the user that you created recently in SalesForce)

![CASB SF credentials](./media/casb_sf_allowcredentials.png)
<p align="center">Figure 1-35</p>

17. Allow Access

![CASB SF Allow Access](./media/casb_sf_allowaccess.png)
<p align="center">Figure 1-36</p>


18. Success! You will now be able to monitor SalesForce! Click Done to finish

![CASB SF completion](./media/casb_sf_complete.png)
<p align="center">Figure 1-37</p>


****

## Module 2:  Create a policy alert and display threats

In Oracle CASB you can create application specific to specify the monitoring you want for your sanctioned applications. This adds another layer of customizable security for you. Oracle CASB also has pre-made Managed Policies for the applications to make sure application specific security can be enabled from the beginning.
You will now create a policy in CASB that will trigger an alert every time a user is logged in to SalesForce.

1. Login to your cloud platform account and select Oracle CASB Cloud Service.
2. Select Configuration in the Navigation menu to the left 
3. Select Policy Management
4. Click New Policy
    * Fill out the fields as shown below
    * Click Next

![CASB Create new policy](./media/casb_sf_newpolicy.png)
<p align="center">Figure 2-1</p>


5. Fill out the fields as shown below. Click Next

![CASB Create new policy_2](./media/casb_sf_newpolicy_2.png)
<p align="center">Figure 2-2</p>

6. Click Next

![CASB Create new policy_3](./media/casb_sf_newpolicy_3.png)
<p align="center">Figure 2-2</p>

7. Click Next

![CASB Create new policy_4](./media/casb_sf_newpolicy_4.png)
<p align="center">Figure 2-3</p>

8. Populate fields as shown below. You can fill the message box with anything you consider such as "Verify SalesForce login activities". click Next

![CASB Create new policy_5](./media/casb_sf_newpolicy_5.png)
<p align="center">Figure 2-4</p>

9. Review details previously entered and click submit

![CASB Create new policy_6](./media/casb_sf_newpolicy_review.png)
<p align="center">Figure 2-5</p>

We must now trigger the policy that we created

10. Log in to the ![Salesforce console](https://developer.salesforce.com) as the **user we created to be monitored by Oracle CASB**

11. Once logged in to Salesforce, you should be able to see the dashboard

![Login SF](./media/sf_login.png)
<p align="center">Figure 2-6</p>


12. This triggered the policy and an alert for Salesforce was generated. Every time a user logs in to Salesforce, you will be able to check it in your Salesforce instance. Navigate back to Oracle CASB Cloud Service console and click on **Policy alerts** and you will see all the alerts received for Salesforce.

![CASB SF alert](./media/casb_sf_policyalerts.png)
<p align="center">Figure 2-7</p>

13. Click on a single policy alert generated by an authentication action to see the details

![CASB SF alert_2](./media/casb_sf_polictyalerts_2.png)
<p align="center">Figure 2-8</p>


****
**You have successfully connected and run an operation against ATP with Oracle OML. We will use OML in other labs.**

***END OF LAB***

[Back to Top](#table-of-contents)   
