## **Install Oracle Instant Client** for Linux x86-64

This guide shows you how to install Oracle Instant Client for Linux on your machine.  The Instant Client has the Oracle Net driver and associated libraries to connect to an Oracle database.  

## **Download**

Download the Instant Client [here](https://www.oracle.com/database/technologies/instant-client/downloads.html).  Select the client for your OS.  You can download Version 19.13.0.0 and Basic Package.

For general Instant Client information, see the [Home Page](https://www.oracle.com/database/technologies/instant-client.html).

ODBC users should follow the [ODBC Installation Instructions](https://www.oracle.com/database/technologies/releasenote-odbc-ic.html).

The "Database Client Installation Guide for Linux" chapter on Installing Oracle Instant Client is [here](https://www.oracle.com/pls/topic/lookup?ctx=dblatest&id=GUID-3AD5FA09-8A7C-4757-8481-7A6A6ADF479E).

Instant Client RPMs are also available without click-through from [yum.oracle.com](http://yum.oracle.com/) for [Oracle Linux 8](https://yum.oracle.com/repo/OracleLinux/OL8/oracle/instantclient21/x86_64/) and [Oracle Linux 7](https://yum.oracle.com/repo/OracleLinux/OL7/oracle/instantclient21/x86_64/). Older RPM packages are available for [Oracle Linux 8](https://yum.oracle.com/repo/OracleLinux/OL8/oracle/instantclient/x86_64/), [Oracle Linux 7](https://yum.oracle.com/repo/OracleLinux/OL7/oracle/instantclient/x86_64/) and [Oracle Linux 6](https://yum.oracle.com/repo/OracleLinux/OL6/oracle/instantclient/x86_64/).

Client-server version interoperability is detailed in [Doc ID 207303.1](https://support.oracle.com/epmos/faces/DocumentDisplay?id=207303.1). For example, Oracle Call Interface 19.3 can connect to Oracle Database 11.2 or later. Some tools may have other restrictions.

**Installation of ZIP files:**

1. Download the desired Instant Client ZIP files. All installations require a Basic or Basic Light package.
2. Unzip the packages into a single directory such as `/opt/oracle/instantclient_19_3` that is accessible to your application. For example:
3. ```
   cd /opt/oracle      
   unzip instantclient-basic-linux.x64-19.3.0.0.0dbru.zip
   ```

4. The various packages install into subdirectories of `/usr/lib/oracle`, `/usr/include/oracle`, and `/usr/share/oracle`.

5. Prior to version 18.3, create the appropriate links for the version of Instant Client. For example:
6. ```
   cd /opt/oracle/instantclient_12_2
   ln -s libclntsh.so.12.1 libclntsh.so
   ln -s libocci.so.12.1 libocci.so
   ```

7. Install the operating system `libaio` package. This is called `libaio1` on some Linux distributions. On Oracle Linux 8 prior to Instant Client 21 you also need the libnsl package.
8. For example, on Oracle Linux, run:

9. `sudo yum install libaio`

10. If Instant Client is the only Oracle Software installed on this system then update the runtime link path, for example:
11. ```
    sudo sh -c "echo /opt/oracle/instantclient_19_3 > \
          /etc/ld.so.conf.d/oracle-instantclient.conf"
      sudo ldconfig
    ```

12. Alternatively, set the `LD_LIBRARY_PATH` environment variable prior to running applications. For example:

13. `export LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3:$LD_LIBRARY_PATH`

14. The variable can optionally be added to configuration files such as `~/.bash_profile` and to application configuration files such as `/etc/sysconfig/httpd`.

15. If you intend to co-locate optional Oracle configuration files such as `tnsnames.ora`, `sqlnet.ora`, `ldap.ora`, or `oraaccess.xml` with Instant Client, put them in the `network/admin` subdirectory. This needs to be created for 12.2 and earlier, for example:
16. `mkdir -p /opt/oracle/instantclient_12_2/network/admin`

17. This is the default Oracle configuration directory for applications linked with this Instant Client.

18. Alternatively, Oracle configuration files can be put in another, accessible directory. Then set the environment variable `TNS_ADMIN` to that directory name.

19. To use binaries such as sqlplus from the SQL*Plus package, unzip the package to the same directory as the Basic package and then update your `PATH` environment variable, for example:
20. `export PATH=/opt/oracle/instantclient_19_3:$PATH`

21. Start your application.



**Installation of RPM files:**

1. Download the desired Instant Client RPM packages. All installations require a Basic or Basic Light RPM.
2. Install the packages with `yum`. For example:
3. `sudo yum install oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64.rpm`

4. Note that from 19.3, by default only one version of the Instant Client RPM libraries can be installed at a time.

5. Prior to 19.3, if Instant Client is the only Oracle Software installed on this system then update the runtime link path, for example:
6. ```
   sudo sh -c "echo /usr/lib/oracle/18.3/client64/lib > \
         /etc/ld.so.conf.d/oracle-instantclient.conf"
     sudo ldconfig
   ```

7. For Instant Client 19.3 RPM packages, these commands are automatically run.

8. An alternative to using `ldconfig` for older versions, is to set the `LD_LIBRARY_PATH` environment variable in each shell prior to running applications. For example:

9. `export LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib:$LD_LIBRARY_PATH`

10. The variable can optionally be added to configuration files such as `~/.bash_profile` and to application configuration files such as `/etc/sysconfig/httpd`.

11. If you intend to co-locate optional Oracle configuration files such as `tnsnames.ora`, `sqlnet.ora` `ldap.ora`, or `oraaccess.xml` with Instant Client, put them in the `network/admin` subdirectory. This needs to be created for 12.2 and earlier, for example:
12. `sudo mkdir -p /usr/lib/oracle/12.2/client64/lib/network/admin`

13. This is the default Oracle configuration directory for applications linked with this Instant Client.

14. Alternatively, Oracle configuration files can be put in another, accessible directory. Then set the environment variable `TNS_ADMIN` to that directory name.

15. To use binaries from the tools package, use `yum` to install the package and then update your `PATH` environment variable, for example:
16. `export PATH=/usr/lib/oracle/19.3/client64/bin:$PATH`

17. Start your application.



## **Acknowledgements**
* **Author(s)** - Milton Wan, Database Product Management
* **Contributor(s)** - 
* **Last Updated By/Date** - Milton Wan, December 2021
