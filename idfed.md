# Federating AAD with Okta for Multi-Cloud Self-Service Project Creation

The goal of this project is to demonstrate the ability to create a non-authoritative Enterprise IdP (SP?) for use in building Advance Development Tenancies (ADT) in a variety of Public Cloud and SaaS platforms. Since the ADT’s MAY use subscriptions/accounts slaved off 2, existing parent domains and maybe more provided by clients/partners, it’s important that administrative access be maintained by IT, Security and Audit for the purpose of monitoring and emergency actions.

At the same time, it is likely that 3<sup>rd</sup> parties will need to be involved in the development, integration, and demonstration of these projects and as such, an easier way to grant privileged/non-privileged principal accounts as well as service accounts will be pre-requisite to success.

To prevent misconfiguration, privilege bleed-thru and resource visibility, as well as Commercial/GCC multi-directory challenges, using an Hybrid IdP WILL be important to the success of this project.<img src=".//media/image1.png" style="width:6.5in" />

The goal being to create a [Layered](https://www.okta.com/resources/whitepaper/using-okta-for-hybrid-microsoft-aad-join/) IdP/SP Domain capability for ADT in which Okta becomes the delegate AuthN/Z provider for the ADT created accounts and services. One interesting point is that Okta CAN act as an LDAPS IdP and therefore for some remaining DataCenter assets running linux with LDAP, Okta might become a more authoritative IdP for those services in it’s hybrid mode.  Still, my experience points to the fact that Okta does enable unified & automated identity-driven security that makes everything easier to deploy, integrate, visualize, and manage.

Still, we do expect that Employees / Devices / Productivity services will remain in EAD as the primary IdP whether thru AAD or AD Connect for the hybridization or authoritative reference.

## Get Instance of Azure Active Directory (AAD)

Free trials of AAD are available from Microsoft
[here](https://azure.microsoft.com/en-us/trial/get-started-active-directory/)

<img src=".//media/image2.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />

I used my GitHub account identity to provision my instance and was able to setup via the portal. Notice that automation of the creation of specific creation, development, promotion, deployment, and destruction inclusive of specific Service Principals and the assignment of principals to groups will likely leverage the Azure CLI or PowerShell environments for continuous changes in membership.

<img src=".//media/image3.png" style="width:6.5in" alt="Graphical user interface, text, application, email Description automatically generated" />

### Provision Users

Click on Manage->Users:

<img src=".//media/image4.png" style="width:6.5in" alt="Create Test Users" />
To create users - email, firstName, lastName, company and principalEmailAddr are all mappable fields.

### Provision Groups

Click on Manage->Groups:

<img src=".//media/image5.png" style="width:6.5in;height:2.86667in" alt="Create initial groups" />
I had started out creating groups so I could add a group to the application vs. each user, but given my trial instance vs. previous, I could not use the group at this point.

### Configure Azure AD as an Identity Provider \[to a Service Provider

First go into Azure AD -> Add Application (which is a Service Provider)
and it will take you to the Gallery.

1.  Click on “+ Create your own application”.
2.  A pop-up will appear to right, name your application, I used “Okta SP”
3.  Click Create

<img src=".//media/image6.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />

Click Setup Single Sign On

<img src=".//media/image7.png" style="width:6.5in" alt="Graphical user interface, application, website Description automatically generated" />

Then select SAML

<img src=".//media/image8.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />
AAD will then provide a set of integration points:
<img src=".//media/image11.png" style="width:6.5in" alt="SAML IdP Integration Keys" />

Click "Download" where you see the "3" to download the Base64 Certificate

<img src=".//media/image10.png" style="width:4.80556" alt="Download IdP Certificat to local host" />

### Setup Okta with Azure AD as Identity Provider (IdP)
In a new window or tab (recognizing that you will be cutting and pasting between the okta and azure ad management consoles...

1.  Log into your Okta tenant / or secure a trial tenant and configure

2.  <img src=".//media/image12.png" style="width:6.12847in;height:2.98924in" />Navigate
    to ‘Admin’ → ‘Security’ → ‘Identity Providers’

3.  <img src=".//media/image13.png" style="width:3.04653in;height:3.36042in" />Click
    on ‘Add Identity Provider’

4.  Click on ‘Add SAML 2.0 IdP’

5.  <img src=".//media/image14.png" style="width:5.84236in;height:2.86875in" />Now
    Name the IdP something reasonable

6.  Enter the following information (choose a name of your choice)

> Enabling JIT is a choice. You can choose not to enable
> JIT if you don’t want Okta to auto-create users when they login
> for the first time using Azure AD account. Given the "provision thru" model of our 
> user-story and automation, it is an important facet of the layered provisioning and routing.
<img src=".//media/image15.png" style="width:6.16181in" />

7.  Copy & paste SAML protocol settings from Azure AD to Okta paying special attention to the fact that from the Azure Setup/Signing Certificate and Okta the field order shifts.
<img src=".//media/image17.png" style="width:6.5in" />

8.  Now Click ‘Add Identity Provider’
<img src=".//media/image18.png" style="width:6.5in" alt="Graphical user interface, text, application Description automatically generated" />

9.  Now go back and expand the Identity provider
<img src=".//media/image19.png" style="width:6.5in" alt="Graphical user interface, text, application, email Description automatically generated" />

10. And COPY the two SAML protocol settings from Okta to Azure AD (note a reversed field / text entry box order again)
<img src=".//media/image20.png" style="width:6.5in;height:2.76944in" alt="Graphical user interface, text, application Description automatically generated" />

Inbound Federation is now complete!

### Mapping the “Claims”

The IdP responds to authentication requests with a token that include meta data that is useful for establishing identity, groups, roles and other potential decisioning within the upstream Provider.  In our case we are including companyName / organization and can map this to employees to facilitate Okta JIT adds to employee groups.

<img src=".//media/image21.png" style="width:6.5in" alt="Graphical user interface, text, application, email Description automatically generated" />

11. Click on ‘Edit’ to update the claims. Importantly the Claim Name must match the field names in Okta directly. As such nomenclature such as namespace definitions must be removed, and the keys matched.

### Testing the SP->IdP Inbound Federation

Now you can test the log thru semantics in Azure AD.

12. My configuration required one last setting, the assignment of IdP users/groups to the Application “Okta SP” as individuals need to be permissioned for the service. This might be an interesting place to ensure that employees are trained before allowing their credentials to be authorized for use in the ATD environment.

## Federating Okta as an IdP to AWS as an SP

Step 2: [here](/oktaIdpAws.md)

## Automation Development

Okta API’s are available
[here](https://developer.okta.com/docs/reference/)
