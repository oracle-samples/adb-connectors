# Oracle Database Access with Azure AD OAuth2 Integration

In the world of database management and security, connecting Azure Active Directory (AD) with OAuth2 token to Oracle Database offers a robust authentication method, ensuring secure access control while streamlining user management. This integration leverages Azure AD’s powerful identity and access management features to authenticate users accessing Oracle Database through OAuth2 tokens.

## Understanding OAuth2 and Azure AD Integration:

OAuth2 stands as an authorization framework facilitating secure and controlled access to resources. Azure AD, as an OAuth2 identity provider, enables users to obtain access tokens that validate their identities and permissions.

Integrating Azure AD with Oracle Database through OAuth2 grants users access based on their Azure AD credentials, strengthening security measures and simplifying access control.

The blog is part of a 3 part series of blogs. Part 1 is the setup. [Part 2](https://medium.com/@vbalebai/accessing-azure-ad-oauth-token-via-python-and-connecting-to-autonomous-database-adb-using-sql-5c4f77da71d9) is to get an access token in an interactive way and test the connection to Oracle ADB. Part 3 is use of Oracle development in java, python, .NET.

## Steps to Connect Azure AD with OAuth2 Token to Oracle Database:

### Prerequisite:

A login username/password and tenant domain in Azure.

Oracle Autonomous data. — This can have a wallet using mTLS or without it.

### Step 1 : Azure AD setup:

Azure Portal Access: Log in to the Azure portal ([https://portal.azure.com](https://portal.azure.com/)) using the provided username/password. Navigate to Azure Active Directory > App registrations > New registration.

![VBlog1img1](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/VBlog1img1.webp)

- *Register Your Application:* Enter essential details like name, redirect URIs, etc., to complete the application registration.

![blog1img2](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/blog1img2.webp)

Click Register.

![vblog1img3](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img3.webp)

- *Add App URI:* Post registering the new App, proceed to add an Application ID URI, crucial for the Database configuration. The Client id is already in the URI in the format of api://Client_id. replace api:// with your tenant domain name and “SAVE” it..

![img](https://miro.medium.com/v2/resize:fit:700/1*RO5mcK4DrfG1BkKuSknKDw.png)

- *Create Scope :* Generate the required Scope by selecting ‘Expose an API’ and setting values like oracle_ADB_access. Ensure that **‘Admins and Users’** toggle is selected and **Enabled**.

![vblog1img4](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img4.webp)

- Create App Roles (e.g., admin_role, hr_role) to request the necessary scope for database authorization.

![vblog1img6](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img6.webp)

## Step 2: Assign role Privilages in Enterprise App.

From the portal home , access the enterprise app by searching for the registered app name. In the user section, map Azure user IDs with respective roles (e.g., admin_role, hr_role).

![vblog1img7](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img7.webp)

![vblogimg8](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblogimg8.webp)

In the user section, search for the Azure user id you logged into portal. This is the user id for role mapping. From the portal home , access the enterprise app by searching for the registered app name. In the user section, map Azure user IDs with respective roles (e.g., admin_role, hr_role).

![vblog1img9](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img9.webp)

Next, map the role admin_role to it. Repeat the steps for hr_role.

![vblog1img10](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img10.webp)

![vblog1img11](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img11.webp)

### Step 3: Oracle Database Configuration

- Log in to Oracle Database with administrative privileges.

![vblog1img12](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img12.webp)

- *Create OAuth2 Authentication Profile:* Utilize the DBMS_CLOUD_ADMIN.ENABLE_EXTERNAL_AUTHENTICATION procedure, specifying Azure AD parameters, such as tenant ID, application ID, and application ID URI.

![vblog1img13](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img13.png)

- *Configure Database Authentication:* Verify the Azure AD configuration within the database by checking the identity_provider_type parameter.

![vblog1img14](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img14.png)

*Create Users and Roles:* Establish users and roles that align with Azure AD roles, allowing access to the database solely through valid tokens.

![vblog1img15](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img15.png)

### Step 4: Registering the Oracle DB Client App with Azure AD

To get the token from Azure, we need to register a client. For other ways to access the token, checkout the [documentation.](https://docs.oracle.com/en/database/oracle/oracle-database/19/dbseg/authenticating-and-authorizing-microsoft-azure-active-directory-users-oracle-databases.html#GUID-B2F6E625-F004-4FA3-9F36-ECD9DDCB30E3)

Azure AD Admin Access: Log in to the Azure portal as an administrator with Microsoft Azure AD privileges from https://portal.azure.com.

1. Register Database Instance: In the Azure Active Directory admin center, select “App registrations” and create a new registration for the Oracle Database Client App.

![vblog1img16](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img16.webp)

Set this application as public and set the url to [http://localhost](http://localhost/).

Setting API Permissions: Navigate to “API Permissions,” allowing the required permissions for the registered database.

![vblog1img17](/Users/kirkgustafson/Documents/GitHub/vijay-blogs/vijay-blog-1/images/vblog1img17.webp)

This robust integration of Azure AD with Oracle Database through OAuth2 tokens not only fortifies security but also streamlines user access and management. With this method, managing user roles and permissions becomes more efficient, ensuring secure and controlled access to critical databases.

[Part 2](https://medium.com/@vbalebai/accessing-azure-ad-oauth-token-via-python-and-connecting-to-autonomous-database-adb-using-sql-5c4f77da71d9) : Get token and validate and test DB connection using sql*dev

Part 3 : run a Java, Python, OCI function connections.

