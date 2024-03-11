# Accessing Azure AD OAuth token via Python and Connecting to Autonomous Database (ADB) Using SQL Developer

In today’s technological landscape, integrating applications with Azure Active Directory (AD) is becoming increasingly common. This blog post is part 2 and aims to guide you through the process of accessing Azure AD using Python, acquiring access tokens interactively, and subsequently connecting to an Autonomous Database (ADB) using SQL Developer.

## Interactive Access Token Acquisition

To begin, let’s focus on acquiring an access token interactively through a Python program. This demonstration assumes you have the necessary prerequisites and have registered your application within Azure as described[in Part 1.](https://medium.com/@vbalebai/oracle-database-access-with-azure-ad-oauth2-integration-7cfce8e9da54)

## Prerequisites:

Before starting, ensure you have the following information ready:

- Tenant ID: Directory (tenant) ID for your registered application in Microsoft Azure portal.
- Client ID: Application (client) ID associated with your registered application.
- Redirect URI: Set as ‘[http://localhost](http://localhost/)' for your application in Microsoft Azure portal.
- Install the MSAL Python SDK on your local machine by running `pip install msal`.
- Save the provided [Python code snippet](https://github.com/vijaybalebail/AzOAuth2ADB) as `get-tokens.py` on your local machine.

## Running the Program:

Execute the Python program `get-tokens.py` as follows:

![vblog2img1](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-2/images/vblog2img1.png)

This program will prompt a browser window where you’ll enter your Azure user ID and password. Upon successful validation, the access token will be displayed.

![vblog2img2](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-2/images/vblog2img2.webp)

## Validating the Access Token:

To validate the access token, copy and paste it into [https://jwt.io](https://jwt.io/) and ensure that the ‘app roles’ mapped to the ADB are visible.

![vblog2img3](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-2/images/vblog2img3.webp)

## Connecting to ADB Using SQL Developer

Now, let’s proceed with connecting to an Autonomous Database (ADB) using SQL Developer.

## Steps:

1. Download the Latest SQL Developer: Ensure you have [SQL Developer 23c, ](https://www.thatjeffsmith.com/archive/2023/04/oracle-sql-developer-23-1-is-now-available/)which supports Azure OAUTH2 tokens and necessary JDBC thin drivers.
2. Prepare Token and ADB Wallet: Save the obtained token in a file, e.g., `F:/t1/token`. If ADB is configured using mTLS, download and extract the wallet zip file into a directory.
3. Create Connection in SQL Developer:

- Choose “Custom JDBC” when creating a new connection.
- Configure the JDBC URL similar to the example below: `jdbc:oracle:thin:@(description=(retry_count=2)(retry_delay=3)(address=(protocol=tcps)(port=1522)(host=adb.us-phoenix-1.oraclecloud.com))(connect_data=(service_name=bk8uwrvkgqzvi2h_k0mu7kr1pye5zn6w_low.adb.oraclecloud.com))(security=(ssl_server_dn_match=yes)(TOKEN_AUTH=OAUTH)(TOKEN_LOCATION=F:\t1\token)(my_wallet_directory=F:\t1\oauth_mtls)))`
- Include `(TOKEN_AUTH=OAUTH)(TOKEN_LOCATION=F:\t1\token)` to point to the token file.
- Include `(my_wallet_directory=F:\t1\oauth_mtls)` to point to the directory where the ADB wallet file is extracted.
- set connection type to OS

![vblog2img4](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-2/images/vblog2img4.webp)

Connect to ADB: Once configured, establish the connection. Execute queries to check the connected username using SQL Developer:

![vblog2img5](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-2/images/vblog2img5.png)

### Conclusion:

With these steps completed, you should now be successfully connected to your Autonomous Database (ADB) using SQL Developer, leveraging Azure AD access tokens acquired through Python. Explore the database, execute queries, and ensure seamless connectivity to your ADB.

Happy coding!