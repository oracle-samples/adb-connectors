# SAP BusinessObjects

### **Connecting to the Oracle Autonomous Data Warehouse Service using an Oracle Wallet**

August 2018

Erick Carlson
 SAP Solution Architect N.A. SAP on Oracle Team erick.carlson@oracle.com



#### Table of Contents

1. Introduction

2. SAP BusinessObjects Server – Oracle Client Setup

3.  Windows Desktop – Oracle Client Setup

4. Creating and Publishing a SAP BusinessObjects

5.  Universe Report Creation with Crystal Reports

6. Report Creation with Web Intelligence

7. References

   

#### Introduction

This guide will demonstrate the steps necessary to connect SAP BusinessObjects (SAP BO) to an Oracle Autonomous Data Warehouse (ADW) for reporting. The primary focus is to validate the ability to use Oracle Wallet, required by ADW, to make a secure connection to an Oracle Database. This guide illustrations how to create a simple SAP BO Universe relying on the Oracle Call Interface (OCI), not to be confused with Oracle Cloud Infrastructure (OCI), as the driver for the connection. This document is by no means is the only way to achieve connectivity to ADW from SAP BO, it is just one example.

This walkthrough is not intended to be a detailed SAP BO reporting guide. The reporting examples simply demonstrate how to create very basic reports utilizing Crystal Reports and Web Intelligence.



#### Basic Skills

This guide relies on some basic skills necessary to configure the Oracle Client and use of SAP BO. This guide should provide the details needed to successfully complete the entire process of connecting SAP BusinessObjects to Oracle Autonomous Data Warehouse.

Required skills and tool knowledge:
 – Connecting to Linux a host and the ability to transfer files. (i.e. ssh & scp)
 – Navigating in a Linux server environment and a Windows desktop.
 – Oracle Client concepts (ORACLE_HOME & TNS_ADMIN) and tools (sqlplus & tnsping). – Oracle Database query understanding. (i.e. tables, columns & SQL)
 – Use of text editors on both Linux and Windows. (i.e. vi & notepad)



#### Pre-Requirements

There are certain requirements necessary for this guide to be successful and are listed below:

– SAP BusinessObjects Server and application login credentials.
 • Access to the Central Management Console (http://*<hostname>*:8080/BOE/CMC).

• Access to the BI Launch Pad (http://*<hostname>*:8080/BOE/BI).
 • A Windows desktop with client development tools for SAP BusinessObjects.

– SAP BusinessObjects Sever administrator operating system access.

– An Oracle 12.2+ Client installed on SAP BusinessObjects server and Windows desktop.

– [ADW Oracle Wallet and login credentials](../common/wallet/wallet.md)





![sap-pic1.1](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic1.1.png)



![sap-pic2.1](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic2.1.png)



![sap-pic3.1](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic3.1.png)





![sap-pic5.1](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic5.1.png)



![sap-pic6](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic6.png)



![sap-pic7](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic7.png)



![sap-pic8](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic8.png)



![sap-pic9](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic9.png)



![sap-pic10](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic10.png)

![sap-pic11](/Users/kirkgustafson/Documents/GitHub/backups/adw-connection-instructions-sap-bo/sap-pic11.png)

![sap-pic11](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic11.png)



![sap-pic12](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic12.png)



![sap-pic13](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic13.png)



![sap-pic14](/Users/kirkgustafson/Documents/GitHub/SAP-Business-Objects/images/sap-pic14.png)

