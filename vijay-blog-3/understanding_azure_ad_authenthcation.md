# Understanding Azure AD Authentication: Interactive vs. Non-Interactive Token Acquisition

![vblog3img1](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/vijay-blog-3/images/vblog3img1.webp)

In the realm of Azure Active Directory (Azure AD), obtaining authentication tokens is a pivotal aspect of securing access to resources. Two primary methods — Interactive and Non-Interactive — facilitate this process. In this blog post, we delve into the distinctions between these methods and shed light on when Non-Interactive methods prove particularly advantageous.

## Interactive Token Acquisition: A User-Centric Approach

The Interactive method involves user interaction, typically in the form of a login prompt. When an application initiates the authentication process, users are redirected to a new browser tab and prompted to provide their credentials interactively. This scenario is common in applications with a user interface, such as web applications or those executed on a device where user interaction is feasible.

### Pros:

1. User-Friendly: Allows for a seamless user experience and a browser redirection to login into Azure AD.
2. Multi-Factor Authentication (MFA): Supports MFA for enhanced security. -> Leverages Azure AD MFA for user login

### Cons:

1. User Presence Required: Implies that user presence is necessary for token acquisition.
2. Automated Scenarios: Can only run when a browser can run on that server and not possible to integrate into any automated process.

## Non-Interactive Token Acquisition: Automation and Service Principals

In contrast, Non-Interactive methods called “Client Credential flow” are designed for scenarios where user interaction is impractical or unnecessary. This method is often employed in automated processes, background tasks, or services that don’t have a user interface. Service principals, representing applications rather than users, play a central role in Non-Interactive token acquisition.

### Pros:

1. Automation-Friendly: Suited for scenarios where user interaction is not possible or desired.
2. Background Tasks: Ideal for tasks running in the background, devoid of user intervention.
3. The server need not have a browser as connect to applications

### Cons:

1. Multi-Factor Authentication Challenges: Might face challenges when dealing with MFA due to the absence of a user.

## When Non-Interactive is Useful: Scenarios and Considerations

1. Automation and Scripting: Non-Interactive methods are indispensable when scripting or automating tasks that require access to Azure AD-secured resources. This is prevalent in scenarios such as scheduled jobs or data synchronization processes.
2. Service-to-Service Communication: Applications communicating with each other, especially in a microservices architecture, benefit from Non-Interactive methods. Service principals authenticate the applications without user involvement.
3. Backend Services: Backend services, devoid of user interfaces, often rely on Non-Interactive methods for acquiring tokens securely.
4. Resource Access without User Presence: In scenarios where resource access is required without the need for direct user interaction, such as background data processing or API access.

## Microsoft Authentication Library (MSAL)

Microsoft provides us with libraries to interact with Azure AD and get the token. Below are some sample program that connect to Azure using MSAL to get tokens. These tokens, once obtained, can be securely stored in a directory and configure Oracle Database connection strings. This opens up connection to Oracle databases, whether residing in the cloud or on-premises, with enhanced authentication and security. This demonstration assumes you have the necessary prerequisites and have registered your application within Azure as described[ in Part 1.](https://medium.com/@vbalebai/oracle-database-access-with-azure-ad-oauth2-integration-7cfce8e9da54)

## Python Example:

### Interactive Token Acquisition:

![vblog3img2](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/vijay-blog-3/images/vblog3img2.png)

### Non-Interactive Token Acquisition:

![vblog3img3](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/vijay-blog-3/images/vblog3img3.png)

## Java Example:

### Non-Interactive Token Acquisition:

![vblog3img4](/Users/kirkgustafson/Documents/GitHub/adb-connectors-1/vijay-blog-3/images/vblog3img4.png)