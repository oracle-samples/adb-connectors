## **Setting Up Oracle JDBC Thin Driver**



1. **Verify your JDK version**: If you are using JDK11, JDK10, or JDK9 then you don’t need to do anything for this step. If your JDK version is less than JDK8u162 then you need to download the JCE Unlimited Strength Jurisdiction Policy Files.  For more information, see [here](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/connect-jdbc-thin-wallet.html#GUID-1640CC02-BF3E-48C2-8FFE-A596614A6A40).

2. **Download Oracle JDBC Driver**: Download the 19.3 JDBC Thin driver (`ojdbc8.jar` and `ucp.jar`) from [Oracle Database 19c (19.3) JDBC Driver & UCP Downloads](https://www.oracle.com/ae/database/technologies/appdev/jdbc-downloads.html). Use the latest 19.3 JDBC driver, or newer.  You also need the additional jars: `oraclepki.jar`, `osdt_core.jar`, and `osdt_cert.jar` for use with Oracle wallets.

3. Make sure you have all the JAR files in your `classpath` or in the location indicated by your application. For example:

   `export CLASSPATH=`    `./lib/ojdbc8.jar:./lib/ucp.jar:./lib/oraclepki.jar:./lib/osdt_core.jar:./lib/osdt_cert.jar`

   `echo $CLASSPATH`



   Note: You can update the `/home/userid/.bash_profile` with the classpath, and restart for the new jars to take effect.
