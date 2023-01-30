## **Install Oracle Instant Client** for Windows 64-bit

This guide shows you how to install Oracle Instant Client for Windows 64-bit on your machine.  The Instant Client has the Oracle Net driver and associated libraries to connect to an Oracle database.  

## **Download and Configure**

Download the Instant Client [here](https://www.oracle.com/database/technologies/instant-client/downloads.html).  Select the client for your OS.  You can download Version 19.13.0.0 and Basic Package.

See the [Instant Client Home Page](https://www.oracle.com/database/technologies/instant-client.html) for more information about Instant Client packages.

Client-server version interoperability is detailed in [Doc ID 207303.1](https://support.oracle.com/epmos/faces/DocumentDisplay?id=207303.1). For example, Oracle Call Interface 19, 18 and 12.2 can connect to Oracle Database 11.2 or later. Some tools may have other restrictions.

1. Download the appropriate Instant Client packages for your platform. All installations require the Basic or Basic Light package.
2. Unzip the packages into a single directory such as `C:\oracle\instantclient_19_3`
3. Add this directory to the `PATH` environment variable. If you have multiple versions of Oracle libraries installed, make sure the new directory occurs first in the path. Restart any terminal windows or otherwise make sure the new PATH is used by your applications.
4. Download and install the correct Visual Studio Redistributable from Microsoft. Instant Client 19 requires the [Visual Studio 2017 redistributable](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads). Instant Client 18 and 12.2 require the [Visual Studio 2013 redistributable](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads). Instant Client 12.1 requires the [Visual Studio 2010 redistributable](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads).
5. If you intend to co-locate optional Oracle configuration files such as tnsnames.ora, sqlnet.ora, ldap.ora, or oraaccess.xml with Instant Client, then create a subdirectory such as `C:\oracle\instantclient_19_3\network\admin`
6. This is the default Oracle client configuration directory for applications linked with this Instant Client.

7. Alternatively, Oracle client configuration files can be put in another, accessible directory. Then set the environment variable TNS_ADMIN to that directory name.

8. Start your application.
9. ODBC users should follow the [ODBC Installation Instructions](https://www.oracle.com/database/technologies/releasenote-odbc-ic.html).



## **Acknowledgements**
* **Author(s)** - Milton Wan, Database Product Management
* **Contributor(s)** - 
* **Last Updated By/Date** - Milton Wan, December 2021
