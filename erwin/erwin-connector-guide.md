# **Connecting Erwin Data Modeler to Oracle Autonomous Database**

### Pedro Torres

This step by step tutorial guides how to configure Erwin Data Modeler connectivity to Oracle Autonomous Database (ADB).

![Picture1](./images/ERWINpic1.png)
## **Prerequisites**

This document assumes the following:
- Autonomous Database (ADB) is provisioned. ADB includes Autonomous Data Warehouse (ADW) or Autonomous Transaction Processing (ATP), or Autonomous JSON Database (AJD).  To provision ADB, see [here](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/autonomous-provision.html#GUID-0B230036-0A05-4CA3-AF9D-97A255AE0C08).

![Picture2](./images/ERWINpic2.png)


1. [Download](lab?=wallet) the corresponding ADB credentials zip file to the system that has Erwin Data Modeler installed.

​	These credential files will be used to connect Erwin Data Modeler to ADB.

![Picture3](./images/ERWINpic3.png)


2. Download and Install Erwin Data Modeler – https://erwin.com/order-fulfillment/

   ![Picture4](./images/ERWINpic4.png)

3. Validate if you are using Windows version for 32-bit or 64-bit. Control Panel -> System and Security -> System

![Picture5](./images/ERWINpic5.png)

4. In this case is for 64 bits

   ![Picture6](./images/ERWINpic6.png)

5. The following instructions assume you are using 62-bit. If you are using 32-bit, the instructions are the same, except to download the 32-bit Erwin Data Modeler.

6. Download Oracle Client 19.3 of this Oracle.com web page:

​		https://www.oracle.com/database/technologies/oracle19c-windows-downloads.html

![Picture7](./images/ERWINpic7.png)

7. Install the Client.

![Picture8](./images/ERWINpic8.png)

8. Navigate to where you downloaded the Oracle ADB credentials. Unzip the contents to a directory.

![Picture9](./images/ERWINpic9.png)

9. I will use Physical according the TNSNAMES.ora in the wallet file

![Picture10](./images/ERWINpic10.png)

10. In the Windows environment variables dialog, create the TNS_ADMIN variable and set it to the directory location where you unzipped the ADB credentials.

![Picture11](./images/ERWINpic11.png)

​		*Note: The tnsnames.ora net service names will be used to connect to ADB.

11. Modify the sqlnet.ora file. Change the directory location where the wallet (cwallet.sso) has been unzipped. It is recommended you remove the quotes around the directory location as well.

![Picture12](./images/ERWINpic12.png)

12. Validate that the Oracle Database Client can communicate with ADW, and since it is installed on the same system as the Erwin Data Modeler, it ensures that Erwin to ADW is also configured correctly. (you can use SqlDeveloper to validate)

![Picture13](./images/ERWINpic13.png)

13. Open Erwin Data Modeler and create a file.

![Picture14](./images/ERWINpic14.png)

14. Use reverse Engineer

![Picture15](./images/ERWINpic15.png)

15. Select the objects that you need validate in your Reverse Engineer file.

![Picture16](./images/ERWINpic16.png)

16. Connect to user that you need to do reverse Engineer and retrieve the information (in this case PTORRESR):

![Picture17](./images/ERWINpic17.png)

17. Validate report from the ADW

![Picture18](./images/ERWINpic18.png)
