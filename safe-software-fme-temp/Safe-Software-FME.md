# **Creating a connection from FME to Oracle Autonomous Data Warehouse (ADW)



![SAFE-pic1](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic1.png)



![SAFE-pic2](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic2.png)



### **Step 1: Provision Autonomous Database plus Install and Configure Oracle Client**

1. Provision Oracle Autonomous Database, either Autonomous Database Warehouse (ADW) or Autonomous Transaction Processing (ATP), and download the [Wallet](../common/wallet/wallet.md) to the system that will have the FME installation. For the Oracle documentation to provision ADW click [here](https://docs.oracle.com/en/cloud/paas/autonomous-database/index.html). For the Oracle documentation to provision ATP, click [here](https://docs.oracle.com/en/cloud/paas/atp-cloud/create.html). Also check [Downloading Client Credentials (Wallets)](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/connect-download-wallet.html#GUID-B06202D2-0597-41AA-9481-3B174F75D4B1).
2. [Download](../common/instant-client/instant-client-windows-64.md) the Oracle Instant Client and SQL*Plus Packages to the same system that FME is installed. The next steps will validate that the Oracle Database Client can communicate with your Autonomous Database. Installing it on the same system as FME ensures that FME is also configured correctly.
3. Uncompress credentials.zip file into a secure folder.
4. In the uncompressed folder, edit the sqlnet.ora file, replacing “?/network/admin” with the name of the folder containing the client credentials. For example:

![SAFE-pic3](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic3.png)

5. Create an environment variable named `TNS_ADMIN`. Set it to the location of the secure folder containing the credentials file you saved in Step 3.
6. Test the Oracle Client with Oracle SQL*Plus. The *tnsnames.ora* file in the uncompressed folder contains either three or five database service names identifiable as either *high*, *medium* and *low*, or *high*, *medium*, *low*, *tp* and *tpurgent* (the service names presented depend on whether your database is ADW or ATP). The predefined service names provide different levels of performance and concurrency for your database. Use one of these service names (for example, ‘my_high’) as your *ConnectString*`. For more information on these service names, [click](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/index.html#GUID-9747539B-FD46-44F1-8FF8-F5AC650F15BE) here for ADW databases, and [here](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/index.html#GUID-9747539B-FD46-44F1-8FF8-F5AC650F15BE) for ATP databases.



The command to test your connection with SQL*Plus will follow this format:

```
   sqlplus connect username/password@connectString
```

For example:

```
   WALLET_LOCATION = (SOURCE = (METHOD = file) (METHOD_DATA =
(DIRECTORY="/home/adwc_credentials")))
   SSL_SERVER_DN_MATCH=yes
```



```
   sqlplus connect my_username/my_password@my_high
```

If the connection is successful you are ready to move to the next step.

### **Step 2. Install FME 2020.1 or Higher**

If there is a pre-existing FME 2020.1 or higher installed, jump to Step 3 which describes the steps to configure ADWC as a target.

To install FME software please refer to the [Install Documentation](https://www.safe.com/support/downloads/). For Mac OS only, there are additional steps...

-  [to allow FME to see the Oracle client](https://knowledge.safe.com/articles/110820/mac-os-catalina-fme-2020-and-oracle-client.html); and
- [to allow FME to see the TNS_ADMIN environment variable](https://community.safe.com/s/article/fme-macos-and-the-oracle-client-a-tip-for-setting).



### Step 3: Configuring FME to connect with Autonomous Databases

1. Open FME Workbench (2020.1 +), and navigate to **Tools** > **FME Options** (Windows/Linux). For Mac navigate to **FME Workbench** > **Preferences...**

![SAFE-pic4](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic4.png)

2. Choose the ‘Database Connections’ option on the left of the window, and then press the ‘+’ on the bottom to add a connection

![SAFE-pic5](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic5.png)



3. Under ‘Database Connection:’, choose Oracle

![SAFE-pic6](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic6.png)

4. Give your connection a name, for example ‘My Oracle Autonomous ADW’

![SAFE-pic7](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic7.png)



5. Under ‘Connection Parameters’, fill out ‘Service Name or Easy Connect:’ with the same connection parameters you used to connect with sqlplus (instructions above):

```
   username/password@connectString
```

![SAFE-pic8](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/SAFE-Software-FME/images/SAFE-pic8.png)

where connectString is one of the database service names listed in your tnsnames.ora file.

6. Click the ‘Test’ button. After a successful connection test, you should now be able to connect to your Oracle Autonomous database in FME using the Oracle Autonomous Spatial Object and Oracle Autonomous Non-Spatial readers & writers.