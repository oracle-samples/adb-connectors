### **Creating a connection from Looker to Oracle Autonomous Data Warehouse**

**Certification Matrix**



![Looker-pic -](/Users/kirkgustafson/Documents/GitHub/adb-connectors/Looker/images/Looker-pic -.png)

This document assumes that the Autonomous Data Warehouse Cloud (ADWC) has been provisioned and the corresponding wallet zip file has been downloaded to the system that has the Looker install. For the Oracle documentation to provision ADWC please check here.

Follow the instructions in this Looker document to configure your Oracle ADWC instance for Looker. This will include creation of the *looker* user, which is referenced later in these instructions.

https://docs.looker.com/setup-and-management/database-config/oracle

The instructions for ADWC vary slightly. The first step, *Encrypt Network Traffic*, can be skipped as connections to ADWC are secured by default. Also, the instructions reference objects owned by the *sys* user. For ADWC, the *admin* user should be substituted wherever the *sys* user is referenced.

1. Click on the *Admin* link on the top right of the Looker UI

2. From the Admin Menu on the left side of the page, click on the *Connections* link

3. From the Connections page, click the New Connection Button

4. Populate the *Connection Settings* page based on the following table. There is an example of a properly completed *Connection Settings* page at the end of this document.

   Fields highlighted in yellow indicate values that are taken from the tnsnames.ora file.

   

This file can be found by expanding the wallet zip file [downloaded](../common/wallet/wallet.md) from your Autonomous Data Warehouse instance.



![Looker-pic-2](/Users/kirkgustafson/Documents/GitHub/adb-connectors/Looker/images/Looker-pic-2.png)



Note: this includes the opening parenthesis before the word security as well as the two closing parenthesis at the end of the security section, however it does not include the final closing parenthesis - the one that matches the opening parenthesis for the

description section. For example:

`(security=(ssl_server_cert_dn="CN=ADWC-dev.uscom-east- 1.oraclecloud.com,OU=Testing Domain,O=End Point,L=Redwood Shores,ST=California,C=US"))`

Also note that some unintended formatting may be inserted when copying this value and inserting it into the field on the Looker form. Verify that no additional formatting, such as additional spaces, were added during the copy and paste process.



1. Click the *Test These Settings* button at the bottom of the page. If your settings have all been entered correctly and Looker is able to connect to your ADWC instance, you should see a success message like this below the button:
2. Once the test has completed successfully, click the *Add Connection* button to save your settings
3. After adding the connection, you will be returned to the *Connections* page. Click the Test button next to your new connection. This will perform a more complete test of your connection, verifying that all of the configuration performed in Step 1 was completed successfully. If all tests complete successfully (the test can take up to a minute to complete), you should see a success message like this:
4. You are now ready to get started exploring and visualizing your data! For instructions on how to get started, follow the Looker Developer Video Tutorials available at: https://docs.looker.com/video-library/data-modeling

Refer to our full set of online documentation at:

https://docs.looker.com



#### **Example of a completed form for adding a new connection:**



![Looker-pic-3](/Users/kirkgustafson/Documents/GitHub/adb-connectors/Looker/images/Looker-pic-3.png)