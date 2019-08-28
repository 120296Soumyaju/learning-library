#  Redacting in an Autonomous Database
Redaction allows for the masking of sensitive data from the end-user layer. 
Until now if you wanted to mask the data on real time you needed to do it on the application layer or 
to use either custom made views or Virtual Private Database, all these solutions lacking functionalities 
that Data Redaction finally brings. With Data Redaction is now possible to easily totally or partially mask the data, 
randomize the data and set the masking conditions.

<img src="./img/carddetail.png" alt="image-alt-text">
  
## Table of Contents

[Objectives](#objectives)

[Pre-Requisites](#pre-requisites)

[Sign in to OCI Console](#sign-in-to-oci-console)

[Create an ATP instance](#create-an-atp-instance)

[Start using SQL Developer Web](#start-using-sql-developer-web)

[Redact Sensitive Data](#redact-sensitive-data)

[Delete the Resources](#delete-the-resources)

## Objectives
The objective of this lab is to mask the CUST_LAST_NAME and CUST_MAIN_PHONE_NUMBER column values from the TEST.CUSTOMERS table.

## Pre-Requisites

* The lab requires an Oracle Public Cloud account with Autonomous Transaction Processing Cloud Service.
* Granting DBMS_REDACT access to the user creating the redaction policy is required to complete the operation. The user ADMIN is already granted the EXECUTE object privilege on SYS.DBMS_REDACT package.

  <img src="./img/Priv_DBMS_REDACT.png" alt="image-alt-text">

## Sign in to OCI Console

* **Tenant Name:** {{Cloud Tenant}}
* **User Name:** {{User Name}}
* **Password:** {{Password}}

1. In Oracle Cloud, click Sign In. Sign in using your tenant name. Then click Next.

2. Enter your user name and password.

<img src="./img/Cloud.png" alt="image-alt-text">

## Create an ATP instance

1. From the Oracle Cloud Infrastructure console, create a database of the Autonomous Transaction Processing (ATP) type.

   <img src="./img/ATP_creation.png" alt="image-alt-text">

2. In the Create administrator credentials section, enter a password for the ADMIN user.

   <img src="./img/ADMIN_pass.png" alt="image-alt-text">

3. Click Create Autonomous Database. The ATP instance is being provisioned.

4. Wait until the ATP instance is available. Your database is now ready.

   <img src="./img/ATP_instance.png" alt="image-alt-text">

## Start using SQL Developer Web

1. Click the Service Console tab.

   <img src="./img/Service_console.png" alt="image-alt-text">

2. Click the Development tab. Then click the SQL Developer Web.

   <img src="./img/Devt.png" alt="image-alt-text">
   
3. In SQL Developer Web, sign in with the ADMIN user and the password that you defined during the instance creation. Then click Sign In.

   <img src="./img/SQLDevWeb_login.png" alt="image-alt-text">
   
4. Before starting redacting data, you create a new user and a table with sensitive data. Use the following commands in the Worksheet:
```
      DROP USER test CASCADE;
      CREATE USER test IDENTIFIED BY *your_password*;
      ALTER USER test QUOTA UNLIMITED ON DATA;  
      GRANT create session, create table TO test;
  
      BEGIN 
          ords_admin.enable_schema (p_enabled => TRUE, p_schema => 'TEST', 
	                            p_url_mapping_type => 'BASE_PATH',
          p_url_mapping_pattern   => 'peeps', -- this flag says, use 'peeps' in the URIs 
          p_auto_rest_auth        => TRUE  -- this flag says, don't expose my REST APIs 
      );
      COMMIT;
      END;
      /

      CREATE TABLE test.customers AS SELECT * FROM sh.customers;
   ```
      
   <img src="./img/Create_User_Test.png" alt="image-alt-text">
   <img src="./img/Enable_TEST_user_create_table.png" alt="image-alt-text">

5. Display the data from the TEST.CUSTOMERS table, by copying, pasting, and executing the query in the Worksheet.
```
      SELECT cust_first_name, cust_last_name, cust_main_phone_number FROM test.customers;
``` 
   <img src="./img/Query_not_redacted.png" alt="image-alt-text">
 
## Redact Sensitive Data

1. The table TEST.CUSTOMERS holds columns whose data is sensitive.

   Create a redaction policy on the CUST_LAST_NAME and CUST_MAIN_PHONE_NUMBER columns using the ADD_POLICY and ALTER_POLICY procedures in the DBMS_REDACT package. A policy is made up of several distinct sections.

    * Identify the object : The OBJECT_SCHEMA, OBJECT_NAME and COLUMN_NAME parameters identify the column to be redacted.
    * Give it a name : The POLICY_NAME parameter assigns a name to the policy.
    * What should happen? : The FUNCTION_TYPE parameter determines the type of redaction that should take place. The allowable values are listed here. Depending on the type of redaction selected, you may be required to specify the FUNCTION_PARAMETERS or various REGEXP_* parameters.
    * When should it happen? : The EXPRESSION parameter determines when the redaction should take place. For example, an expression of “1=1” means the redaction will always take place. Alternatively, situational expressions can be defined using the SYS_CONTEXT function.

   Copy, paste, and execute the following statements in the Worksheet:
   * The first procedure creates a new policy. The policy will display null for the CUST_LAST_NAME values for all rows.
   * The second procedure adds a column to be redacted to the existing policy. The policy will display different strings for the CUST_MAIN_PHONE_NUMBER values for all rows.
``` 
     EXEC DBMS_REDACT.ADD_POLICY( object_schema => 'TEST', object_name => 'CUSTOMERS', -
                                  policy_name => 'CUST_POLICY', column_name => 'CUST_LAST_NAME', -
                                  function_type => DBMS_REDACT.NULLIFY, expression => '1=1' 

     EXEC DBMS_REDACT. ALTER_POLICY( object_schema => 'TEST', object_name => 'CUSTOMERS',- 
                                     policy_name => 'CUST_POLICY', action => DBMS_REDACT.ADD_COLUMN, -
                                     column_name => 'CUST_MAIN_PHONE_NUMBER', -
				     function_type => DBMS_REDACT.PARTIAL, -
                                     function_parameters  => 'VVVFVVVFVVVV,VVV-VVV-VVVV,*,6,7', expression => '1=1' )
```

   <img src="./img/Create_alter_policy.png" alt="image-alt-text">

2. Display the redacted values. First delete the commands from the Worksheet and reload the query from the SQL History by clicking twice on the command.

   <img src="./img/Query2.png" alt="image-alt-text">
   
   
   <img src="./img/Query_not_redacted.png" alt="image-alt-text">
   
   What is the reason why the columns still display the values as they are stored in the database? This is because the ADMIN user is granted the EXEMPT REDACTION POLICY privilege.
   
   <img src="./img/Priv_Exempt_Redact.png" alt="image-alt-text">
   
3. Log in as TEST.
  
   To log in as TEST, edit the current URL used to work in SQL Developer Web in the Worksheet as ADMIN by replacing the "admin" string by "peeps".
   
   Example: 
   ```
   https://xxxxxxxxxxxxxxx.oraclecloudapps.com/ords/admin/_sdw/?nav=worksheet
   ```
   ==>
   ```
   https://xxxxxxxxxxxxxxx.oraclecloudapps.com/ords/peeps/_sdw/?nav=worksheet
   ```

   Re-launch the URL in your browser. Enter TEST as the username and the TEST password.

4. Display the data in the TEST.CUSTOMERS table. Copy, paste, and execute the query in the Worksheet.

   SELECT cust_first_name, cust_last_name, cust_main_phone_number FROM test.customers;
   
   <img src="./img/TEST_redacted_columns.png" alt="image-alt-text">
   
   You can observe that you cannot view the customers lastname and that their phone numbers are partially redacted.

## Delete the Resources

1. Log out SQL Developer Web.

   <img src="./img/Log_out.png" alt="image-alt-text">
   
2. Switch to OCI console window.

2. From your ATP details page, hand over the action icon and click **Terminate**. In the confirmation window, provide the ATP instance name and click **Terminate Database**.

   <img src="./img/Terminate.png" alt="image-alt-text">
   

**Congratulations! You have successfully completed the lab.**
