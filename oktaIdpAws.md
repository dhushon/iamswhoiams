# Incoming Federation Okta (IdP) to AWS (SP)

[General Instructions from Okta here](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-AWS-Single-Sign-on.html)

## Preparing Okta to be an IdP for AWS
1. Log into Okta and the Okta Administrative Console 
2. Select Applications->Applications from the left selection bar
3. Click "Browse App Catalog"
<img src=".//media/image-aws1.png" style="width:6.5in" alt="Browse Okta IdP Application Catalog" />
4. Search for *AWS Single Sign-on*
<img src=".//media/image-aws2.png" style="width:6.5in" alt="Find AWS Single Sign-on app in Okta Catalog" />
5. Add AWS Single Sign-on app
<img src=".//media/image-aws3.png" style="width:6.5in" alt="Add AWS SSP application to Okta tenancy" />
6. Configure General Settings including Application label:
  * Here you can see that I used **AWS Single Sign-on ADT**
  * decrease visibility of integration (given that we might use Okta for Employee facing apps that require SSO, and 
  * Click **Done**
<img src=".//media/image-aws4.png" style="width:6.5in" alt="Configure AWS SSP General Settings" />
7. Click on "sign on" in application configuration pane and then click "Edit"
<img src=".//media/image-aws5.png" style="width:6.5in" alt="Configure AWS Sign On settings"/>
8. You will see that we need to configure the SAML 2.0 SP information from AWS
<img src=".//media/image-aws6.png" style="width:6.5in" alt="View fields that require AWS SP information to fulfill" />
9. While you're here, you can download the metadata.xml file needed for IdP setup in AWS, 
<img src=".//media/image-aws03.png" style="width:6.5in" alt="View fields that require AWS SP information to fulfill" />
   * Either "right click" on *Identity Provider metadata* and "save as"a local **metadata.xml**
<img src=".//media/image-aws04.png" style="width:6.5in" alt="Download thru right click, saveas metadata.xml" />
   * Or you can copy the URL, and do a local download from the command line
 <img src=".//media/image-aws05.png" style="width:6.5in" alt="Command line download the metadata.xml link" />

## Preparing AWS to be an SP to Okta

1. Log in to the **AWS Management Console**.
2. Navigate to Security, Identity, & Compliance > **AWS Single Sign-On**
<img src=".//media/image-aws7.png" style="width:6.5in" alt="AWS Management Console, select AWS Single Sign On"/>
3. Click **Enable SSO**
<img src=".//media/image-aws8.png" style="width:6.5in" alt="Enable SSO on AWS Management Console"/>
4. Select **Settings**
<img src=".//media/image-aws9.png" style="width:6.5in" alt="Select Settings in Left Side-Bar"/>
5. Under **Identity source**, select *Change*
<img src=".//media/image-aws10.png" style="width:6.5in" alt="Select Settings in Left Side-Bar"/>
6. Enter the following:
   * Select **External identity provider**.
   * Click *Show individual metadata values.*
<img src=".//media/image-aws11.png" style="width:6.5in" alt="Select External idenity provider and Show Values"/>
7. Make a copy of the **3** AWS SSO Sign-in URL, **1** AWS SSO ACS URL, and **2** AWS SSO issuer URL values. These values will be used in the Okta console.
<img src=".//media/image-aws12.png" style="width:6.5in" alt="Download SP configuration details for okta"/>
8. Upload the Okta metadata.xml file that was created in step 9 above, to configure the Okta as the AWS IdP (arrow #4)
<img src=".//media/image-aws13.png" style="width:6.5in" alt="Upload Okta IdP metadata to AWS to configure IdP"/>
9. Click "Next: Review"
<img src=".//media/image-aws14.png" style="width:6.5in" alt="Review changes to AWS IdP configuration"/>
10. Accept changes by typing **Accept** in the text field and then click **Change Identity Source**
<img src=".//media/image-aws15.png" style="width:6.5in" alt="Review and accept"/>
11. AWS should return a complete message, now head over to Okta console to complete
<img src=".//media/image-aws16.png" style="width:6.5in" alt="Complete message"/>

## Back to Okta to enter the AWS 
10. under Advanced Sign-on Settings
   * Enter the SSO ACS URL that was copied from AWS Step 7.1
   * Enter the AWS SSO issure URL that was copied from AWS Step 7.2
   * Ensure that the Application username format is changed to **Email**
<img src=".//media/image-aws17.png" style="width:6.5in" alt="Complete message"/>
11. Click **Save** at bottom of form.

We are now substantially ready to test

## Testing the SP-initiated SSO
Using the URL from AWS Step 7.3 above... put it into the browser and you should see that AWS forwards to okta as a provider
<img src=".//media/image-aws18.png" style="width:6.5in" alt="Federated Sign-in"/>

Sometimes you will see that the AWS Sign-on will fail... this typically is caused by a lack of user/group assignment to the SP App in Okta
