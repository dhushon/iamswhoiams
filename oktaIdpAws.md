# Incoming Federation Okta (IdP) to AWS (SP)

[General Instructions from Okta here](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-AWS-Single-Sign-on.html)

## Preparing Okta to be an IdP for AWS
1. Log into Okta and the Okta Administrative Console 
2. Select Applications->Applications from the left selection bar
3. Click "Browse App Catalog"
<img src=".//media/image-aws1.png" style="width:6.5in" alt="Browse Okta IdP Application Catalog" />
4. Search for "AWS Single Sign-on"
<img src=".//media/image-aws2.png" style="width:6.5in" alt="Find AWS Single Sign-on app in Okta Catalog" />
5. Add AWS Single Sign-on app
<img src=".//media/image-aws3.png" style="width:6.5in" alt="Add AWS SSP application to Okta tenancy" />
6. Configure General Settings including Application label:
  * Here you can see that I used "AWS Single Sign-on ADT" 
  * decrease visibility of integration (given that we might use Okta for Employee facing apps that require SSO, and 
  * Click "Done"
<img src=".//media/image-aws4.png" style="width:6.5in" alt="Configure AWS SSP General Settings" />
7. Click on "sign on" in application configuration pane and then click "Edit"
<img src=".//media/image-aws5.png" style="width:6.5in" alt="Configure AWS Sign On settings"/>
8. You will see that we need to configure the SAML 2.0 SP information from AWS
<img src=".//media/image-aws6.png" style="width:6.5in" alt="View fields that require AWS SP information to fulfill" />

## Preparing AWS to be an SP to Okta


