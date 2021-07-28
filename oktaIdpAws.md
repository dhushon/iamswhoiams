# Incoming Federation Okta (IdP) to AWS (SP)

[General Instructions from Okta here](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-AWS-Single-Sign-on.html)

1. Log into Okta Administrative Console
2. Select Applications->Applications
3. Browse App Catalog
<img src=".//media/image-aws1.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />
4. Search for "AWS Single Sign-on"
<img src=".//media/image-aws2.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />
5. Add AWS Single Sign-on app
<img src=".//media/image-aws3.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />
6, Configure General Settings including Application label:
	* Here you can see that I used "AWS Single Sign-on ADT" 
	* decrease visibility of integration (given that we might use Okta for Employee facing apps that require SSO, and 
	*  Click "Done"
<img src=".//media/image-aws4.png" style="width:6.5in" alt="Graphical user interface, application Description automatically generated" />


