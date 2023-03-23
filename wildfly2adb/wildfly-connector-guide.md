**Introduction**

WildFly is a free, open-source application server that is widely used for building and deploying enterprise-level Java applications. In this guide, we will walk you through the steps to install the latest version of WildFly on Linux and connect it to the Oracle Autonomous Database. We will also cover the installation and configuration of the JDBC driver, adding the driver, and configuring the datasource manually.


Prerequisites:


| Validation Matrix  | Version  |
| ------------- | ------------- |
| App Version  | X.0.0  |
| Oracle Client  | 19.17  |

### **Prerequisites**

- A Linux-based operating system with Root access to the server
- Required access and credits to provision ADWC instance on Oracle Cloud.
- Download Oracle JDBC Thin driver is downloaded on the app server.
- If ADWC is already configured you have the ADMIN user password and ADB Wallet is downloaded on app server.

## **Configure the Connection**

## Step 1: Download WildFly
Visit the WildFly download page at [https://www.wildfly.org/downloads/](https://www.wildfly.org/downloads/ ) and download the latest version of WildFly.
Choose the **standalone** version.

## Step 2: After downloading, extract the WildFly archive to a location of your choice using the following command:

```
tar xf wildfly-<version>.tar.gz -C /opt/  
```

## Step 3: Extract Autonomous Wallet
Download the wallet from your Oracle Cloud account.
Log in to your Oracle Cloud account and navigate to your Autonomous Database instance.
Click the DB Connection button to open the Download Client Credentials dialog.
Choose the Wallet option and click Download.
Save the wallet zip file to a directory of your choice, for example, /opt/oracle/wallet.
Extract the contents of the wallet zip file to a directory of your choice, for example, /opt/oracle/wallet.
Set the appropriate file permissions on the wallet directory and files, for example:

```
chmod -R 600 /opt/oracle/wallet
```

## Step 4: Add the Oracle JDBC driver to WildFly

1. Download the ojdbc8-full version from Oracle. The full version downloads companion jars, which include oraclepki.jar, osdt_core.jar, and osdt_cert.jar. These files are required to connect to an Autonomous database with the wallet.

2. Create a new directory named oracle in the WildFly module directory and copy the Oracle JDBC driver jar file. Use the following commands to achieve this:  

    ```
    mkdir -p $WILDFLY_HOME/modules/system/layers/base/com/oracle/main/
    cd $WILDFLY_HOME/modules/system/layers/base/com/oracle/main/
    sudo cp </path/to>/ojdbc8-full.jar .
    ```

  Replace </path/to/>ojdbc8-full.jar with the actual path to the downloaded Oracle JDBC driver jar file.


## Step 5: Create a module.xml file

Create a module.xml file in the main directory with the following contents

```
<module xmlns="urn:jboss:module:1.1" name="com.oracle">
        <resources> <resource-root path="ojdbc8.jar"/>
                <resource-root path="oraclepki.jar"/>
                <resource-root path="osdt_cert.jar"/>
                <resource-root path="osdt_core.jar"/>
        </resources>
        <dependencies>
               <module name="javax.api"/>
               <module name="javax.transaction.api"/>
        </dependencies>
</module>

```
Save the file and close it.


## Step 6: Add the driver configuration.

In the configuration file standalone.xml, add the entry within the <drivers> ... </drivers> tag. Edit file $WILDFLY_HOME/standalone/configuration/standalone.xml and add the following:

```
<driver name="oracle" module="com.oracle">
    <driver-class>oracle.jdbc.driver.OracleDriver</driver-class>
</driver>
```

## Step 7: Create a Datasource configuration file

Edit file $WILDFLY_HOME/standalone/configuration/standalone.xml and add the following within the tag <datasources>...</datasources>.

```
<datasource jndi-name="java:jboss/datasources/oracleDS_mtls2" pool-name="MTLS2" enabled="true" use-java-context="true" statistics-enabled="true">
    <connection-url>jdbc:oracle:thin:@orcl_mtls_low?TNS_ADMIN=/opt/oracle/wallet</connection-url>
    <driver-class>oracle.jdbc.driver.OracleDriver</driver-class>
    <driver>oracle</driver>
    <pool>
        <initial-pool-size>0</initial-pool-size>
        <max-pool-size>25</max-pool-size>
        <fair>false</fair>
        <flush-strategy>AllIdleConnections</flush-strategy>
    </pool>
    <security>
        <user-name>USERNAME</user-name>
        <password>YOURPASSWORD</password>
    </security>
    <validation>
        <valid-connection-checker class-name="org.jboss.jca.adapters.jdbc.extensions.oracle.OracleValidConnectionChecker"/>          <background-validation>true</background-validation>
        <stale-connection-checker class-name="org.jboss.jca.adapters.jdbc.extensions.oracle.OracleStaleConnectionChecker"/>          <exception-sorter class-name="org.jboss.jca.adapters.jdbc.extensions.oracle.OracleExceptionSorter"/>          </validation>
</datasource>
```

Replace the USERNAME and YOURPASSWORD with your schema username and password.

Note: if you are familiar with the WildFly command line, add the lines using the following jboss-cli.sh.


## Step 8: Test Connection

After configuring the data source, you can test the connection.

Example:

```
[root@wildfly-adb ~]# /opt/wildfly/bin/jboss-cli.sh --connect  /subsystem=datasources/datasource=MTLS2:test-connection-in-pool()
 {
    "outcome" => "success",
     "result" => [true]
}
```

## Step 9: Deploy Your Application

After configuring the data source, you can deploy your Java application to WildFly. You can do this by copying your application WAR file to the WildFly deployments directory or from the WildFly admin console.


## **Acknowledgements**
* **Author(s)** - Vijay Balebail
* **Contributor(s)** - Milton Wan, Rajeev Rumale
* **Last Updated By/Date** -  23rd March 2023
