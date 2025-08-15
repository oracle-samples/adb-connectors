Creating a connection from Fivetran HVR to Oracle Autonomous Data Warehouse
## Author

Mark Van de Wiel

---

## Overview

This document provides an overview of the steps required to configure Fivetran HVR to connect to the Oracle Autonomous Data Warehouse Cloud (ADWC).

Fivetran HVR supports log-based Change Data Capture (CDC) for heterogeneous data replication from several source database technologies into a multitude of destination technologies and data formats. HVR 6.1 and 6.2 are the latest versions certified to deliver data into the Oracle ADWC (versions 19c and 23ai).

For optimum performance integrating changes into the Oracle ADWC, Fivetran recommends an architecture that features the use of agents. Agents are installations of the HVR software that are located as close as possible to the source and destination technologies. The use of agents optimizes network communication and distributes load.

HVR features such as initial load, ongoing replication, and compare/repair all take advantage of the agents. With the Oracle ADWC as the target, the recommended setup is to include an agent in the Oracle Cloud, in the same availability domain as the ADWC—containerized, on a VM, or installed on a Bare Metal instance. TCP/IP communication between Fivetran HVR installations is always encrypted over TLS 1.3.

---

## Connecting Fivetran HVR to the Oracle ADWC

![ADWC Connection Architecture](hvr-software/images/wta1.png)

### Step 1: Provision ADWC and Install & Configure the Oracle Client

1. **Provision the Oracle Autonomous Data Warehouse Cloud (ADWC)** and download the corresponding `credentials.zip` file to the system that will have the HVR target agent installation.  
    - For Oracle documentation to provision ADWC, [click here](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/index.html).  
    - Also check [Downloading Client Credentials (Wallets)](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/adbwd/download-wallet.html).

2. **Un-compress the `credentials.zip` file** into a secure folder.

3. **Download the Oracle 19c Database Client** to the system that runs the HVR integration agent.

4. **Edit the `sqlnet.ora` file**, replacing `?/network/admin` with the name of the folder containing the client credentials.

    Example:
    ```ini
    WALLET_LOCATION = (SOURCE = (METHOD = file) (METHOD_DATA =
    (DIRECTORY="/home/adwc_credentials")))
    SSL_SERVER_DN_MATCH = yes
    ```

5. The `TNS_ADMIN` environment variable can be set to point to an alternative location for the `sqlnet.ora` and `tnsnames.ora` files. Define the variable if you plan to not use `$ORACLE_HOME/network/admin`.

6. The `tnsnames.ora` file provided with the credentials zip file contains three database service names: **high**, **medium**, and **low**. These provide different levels of performance and concurrency for Autonomous Data Warehouse Cloud. Use one of these service names in your TNS connect string.

7. **Test the Oracle Client with Oracle SQL\*Plus:**
    ```sh
    sqlplus username@<connect string>
    # Enter password at prompt
    ```
    or
    ```sh
    sqlplus /nolog
    SQL> connect username@<connect string>
    # Enter password at prompt
    ```

    If the connection is successful, you are ready to move to the next step.

---

### Step 2: Install HVR

- Follow the installation instructions to install HVR.
- Ensure the HVR hub can reach an agent installation through TCP/IP communication.
- Open the firewall for the HVR listener port to the machine running the HVR agent, as needed.
- Make sure the operating system allows the connection.

---

### Step 3: Create an HVR Location to Connect with ADWC

- In the HVR console, create a new **Location**.
- Choose location type **Oracle**, and enter your configuration information.
- If the HVR hub resides in the Oracle Cloud, you may choose to connect directly to ADWC.
- Use the connect string you tested during the first installation step.
![Creating a New Location in HVR](hvr-software/images/wta2.png)

- Typically, users will connect to the ADWC using an agent running on a VM in the Oracle Cloud.


---

### Step 4: Create a Channel to Deliver Data into the ADWC

- In the HVR console, create a new **Channel**.
- Choose your source location, target Oracle ADWC, and complete the channel setup.
- Refresh the tables and start replicating data!

![Creating a Channel in HVR](hvr-software/images/wta3.png)

- The channel configuration screen allows you to select tables, define replication options, and set up scheduling.
- After saving the channel, you can monitor replication status and review logs for troubleshooting.
- For more details on channel configuration, refer to the [Fivetran HVR documentation](https://fivetran.com/docs/hvr).

**Last Edited By: Blake Hendricks**