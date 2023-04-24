**Introduction**

This step by step tutorial guides how to configure Erwin Data Modeler connectivity to Oracle Autonomous Database (ADB).

![Picture1](./images/erwin_pic1.png =500x500)

## **Prerequisites**

This document assumes the following:
- Autonomous Database (ADB) is provisioned. ADB includes Autonomous Data Warehouse (ADW) or Autonomous Transaction Processing (ATP), or Autonomous JSON Database (AJD).  To provision ADB, see [here](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/autonomous-provision.html#GUID-0B230036-0A05-4CA3-AF9D-97A255AE0C08).

![Picture2](./images/erwin_pic2.png =500x500)


1. [Download](lab?=wallet) the corresponding ADB credentials zip file to the system that has Erwin Data Modeler installed.
    These credential files will be used to connect Erwin Data Modeler to ADB.
    ![Picture3](./images/erwin_pic3.png =500x500)

2. Download and Install Erwin Data Modeler – https://erwin.com/order-fulfillment/
    ![Picture4](./images/erwin_pic4.png =500x500)

3. Validate if you are using Windows version for 32-bit or 64-bit. Control Panel -> System and Security -> System
    ![Picture5](./images/erwin_pic5.png =500x500)

4. In this case is for 64 bits
    ![Picture6](./images/erwin_pic6.png =500x500)

5. The following instructions assume you are using 62-bit. If you are using 32-bit, the instructions are the same, except to download the 32-bit Erwin Data Modeler.

6. Download Oracle Client 19.3 of this Oracle.com web page:
  [https://www.oracle.com/database/technologies/oracle19c-windows-downloads.html](https://www.oracle.com/database/technologies/oracle19c-windows-downloads.html)
    ![Picture7](./images/erwin_pic7.png =500x500)

7. Install the Client.

    ![Picture8](./images/erwin_pic8.png =500x500)

8. Navigate to where you downloaded the Oracle ADB credentials. Unzip the contents to a directory.

    ![Picture9](./images/erwin_pic9.png =500x500)

9. I will use Physical according the TNSNAMES.ora in the wallet file

    ![Picture10](./images/erwin_pic10.png =500x500)

10. In the Windows environment variables dialog, create the TNS_ADMIN variable and set it to the directory location where you unzipped the ADB credentials.

    ![Picture11](./images/erwin_pic11.png =500x500)

    *Note: The tnsnames.ora net service names will be used to connect to ADB.

11. Modify the sqlnet.ora file. Change the directory location where the wallet (cwallet.sso) has been unzipped. It is recommended you remove the quotes around the directory location as well.

    ![Picture12](./images/erwin_pic12.png =500x500)

12. Validate that the Oracle Database Client can communicate with ADW, and since it is installed on the same system as the Erwin Data Modeler, it ensures that Erwin to ADW is also configured correctly. (you can use SqlDeveloper to validate)

    ![Picture13](./images/erwin_pic13.png =500x500)

13. Open Erwin Data Modeler and create a file.

    ![Picture14](./images/erwin_pic14.png =500x500)

14. Use reverse Engineer

    ![Picture15](./images/erwin_pic15.png =500x500)

15. Select the objects that you need validate in your Reverse Engineer file.

    ![Picture16](./images/erwin_pic16.png =500x500)

16. Connect to user that you need to do reverse Engineer and retrieve the information (in this case PTORRESR):

    ![Picture17](./images/erwin_pic17.png =500x500)

17. Validate report from the ADW

    ![Picture18](./images/erwin_pic18.png =500x500)
