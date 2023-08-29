**Creating a connection from MotionBoard to   Oracle Autonomous Data Warehouse (ADW)**

**Author:** **WingArc1st Inc.**

**23/Jul/2019**





**Prerequisites**

- The  connection  destination  must  be  in  an  environment  where  it  can  communicate  with MotionBoard and runs correctly. It’s necessary that user have knowledge about network and server environment.
- This document assumes that the Autonomous Data Warehouse has been provisioned and the corresponding wallet zip file has been downloaded to the system.

**Step 1. Install MotionBoard**

If there is a pre-existing Motionboard installed jump to Step 3 which describes the steps to configure ADWC as a target.

To install Motionboard software please refer to the Install[ Documentation.](https://manual.wingarc-support.com/en-us/manual/mb/mb60/)

**Step 2. Install Oracle driver on MotionBoard (ONLY for “on premises” version)**

1. Open installer file and select “MotionBoard60 - extra”.
2. Copy  “oracle\_autonomous.zip”  to “[InstallDir]\system\resources\communicator\drivers\extra”. 
3. Restart “Motionboard 6.0” service.

![](Aspose.Words.3c89a675-007c-4ae5-840c-ff3e31b899dc.001.jpeg)

**Step 3. How to configure MotionBoard on a Windows environment**

1  Select the type of data source to connect to

1. Log in to MotionBoard as a user with administrator privileges.
1. Select Management of the board menu - System Settings - Connection/Authentication - External Connection.

![](Aspose.Words.3c89a675-007c-4ae5-840c-ff3e31b899dc.002.jpeg)

3. Click the New button on the External Connection screen.
3. Enter the name of the external connection settings in External Connection Name on the Create New External Connection screen.
3. In Connection Type, select the connection destination (data source name).
3. In Relay Service, select a connection method for connecting with the destination. If Relay Service does not appear, proceed to the next step.
3. To connect directly to the connection destination, select Disable. Usually, you select this option.
3. To use the Bridge Service, select Bridge Service and select the Bridge group to use for Bridge Group Name.
3. To use the Federation Service, select Federation Service and select the Bridge group to use for Federation Name.
3. Click the New button.
3. Click the OK button on the message to confirm saving the settings.

2  Specify information necessary for connection with Oracle Autonomous Data Warehouse

1. Click the Basic Information tab in the External Connection screen.
1. Specify Driver Type. Select to connect to “Oracle Autonomous(JDBC)”.
1. Check the settings for Relay Service and change them as necessary.
1. In Service Name, specify the name of the Oracle Autonomous Data Warehouse Service.
1. Click “Select” button of Wallet and select corresponding wallet zip file.
6. In  User  Name,  specify  the  user  ID  equivalent  to  the  server  administrator  of  Oracle Autonomous Data Warehouse.
6. Click the Password setting button of Password, and specify the password for User Name.

![](Aspose.Words.3c89a675-007c-4ae5-840c-ff3e31b899dc.003.jpeg)

3  Confirm you can connect to the connection destination

1. Click the Connection Test button.
1. If a message indicating connection succeeded is displayed, proceed to the next step.
1. If a message indicating connection failed is displayed, return to the previous step and review the setting.
1. Click the Save button.
1. Click the OK button on the message to confirm saving the settings.

**Step 4. Check connectivity between MotionBoard and Oracle** 1  Create New dashboard to check the connectivity.

1. Click the New and create new dashboard.
1. Create new data source of charts or spreadsheet.
3. Select the data source type you made in Step 2(for example “Oracle\_ADW”) from connect type.

![](Aspose.Words.3c89a675-007c-4ae5-840c-ff3e31b899dc.004.jpeg)

4. Choose table or view in table and view list.

![](Aspose.Words.3c89a675-007c-4ae5-840c-ff3e31b899dc.005.jpeg)

5. Drag and drop items from Item List to column, row and summary item field in Data Source Editor.
5. Click OK and save data source definition.

2  When a chart or spreadsheet is deployed and show its data from Oracle, then you’re now ready

to  read  data  from  Oracle  Autonomous  Data  Warehouse.  And  analyze,  visualize  the  with MotionBoard.

![](Aspose.Words.3c89a675-007c-4ae5-840c-ff3e31b899dc.006.jpeg)
