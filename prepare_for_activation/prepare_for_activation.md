Before you can activate Joule there are certain number of pre-requisites that must be met.  This section describes those pre-requisites and outlines some details that need to be captured prior to running through the activation steps.

## 1. User Personas Required for Joule activation

Activation of Joule requires configuration in multiple systems.  It's important to have the right stakeholders involved when setting up the configuration.  In order to setup Joule the following user personas are required:
* SuccessFactors Admin
* SAP BTP Global Account Admin
* SAP Cloud Identity Services Admin
  
## 2. Verify Global Account Entitlements

Verify that your global account is configured with the following entitlements. For more information, see [Managing Entitlements and Quotas Using the Cockpit](https://help.sap.com/docs/BTP/65de2977205c403bbc107264b8eccf4b/c8248745dde24afb91479361de336111.html).

| Application     | Technical Name | Plan        | Required Quota | Remaining Quota |
| ----------- | ----------- | ----------- | -------------- | --------------- |
| Joule      | das-application      | foundation       |     1            |          limited       |
| SAP Build Work Zone, standard edition   | SAPLaunchpad       | foundation or standard       |      1           |       limited          |


| Service     | Technical Name | Plan        | Required Quota | Remaining Quota |
| ----------- | ----------- | ----------- | -------------- | --------------- |
| SAP Build Work Zone, standard edition      | build-workzone-standard      | foundation or standard      |     1            |          limited       |

If the entitlements are not visible it could be due to one these reasons:
  1) You don't have licenses for Joule.
  2) Joule entilements were added to different BTP Global Account to which you don't have Global Account Admin access.
  3) The start date for the Joule contract is at future date hence the entilements won't be visible in BTP until that date.
In the scenarios above, please work with Account Executive, BTP Customer Success Partner or SuccessFactors Customer Success Partner to resolve the entitlements issue prior to proceeding further with this mission.

## 3. Verify Supported Data Centers for Joule

Joule is supported in selected data centers, but this list is expanding on regular basis.  See the list of [Data Centers Supported by Joule](https://help.sap.com/docs/joule/serviceguide/data-centers-supported-by-joule). The BTP subaccount should be in one of these supported data centers for Joule setup.  We will create this subaccount in later steps.

## 4. Validate Global User ID of SuccessFactors User

In order to use Joule, SuccessFactors users must have a Global User ID(GUID) field populated in their SuccessFactors user profile and this GUID should match what's in the SAP Cloud Identity Authentication (IAS) user profile.  This should already be in place if SuccessFactors integration to SAP Cloud Identity Services was done following best practices and a provisioning job was run to replicate user profiles from SuccessFactors to IAS. If the user replication job was not run in the past or if there were errors for certain users during the job execution, those users will not have the GUID field populated in SuccessFactors.  The **Manage Login Accounts** app can be used to visualize the GUID field in SuccessFactors and compare it to the user profile in IAS.  For more information on how to get access to the Manage Login Accounts application, follow [2859043 - Manage Login Accounts tool](https://userapps.support.sap.com/sap/support/knowledge/en/2859043).<br/>
![prepare_activation](5.jpg)

## 5. SAP Cloud Identity Provisioning Service running on Neo or SAP Cloud Identity Services Landscape

As part of the activation steps we need to leverage SAP Cloud Identity Provisioning Service to read users from SuccessFactors and provision them to SAP Build Work Zone.  This requires that SAP Build Work Zone, standard edition is available as a connector under target systems in SAP Cloud Identity Provisioning Service (IPS).  This connector may not be available on IPS tenants running on NEO landscapes.  It's recommended customers migrate IPS from NEO to IPS running on SAP Cloud Identity Provisioning Service (SCI) landscape.  In most cases this migration can be done in a matter of minutes.  For more information on how to perform this migration, refer to the following links:
* [Blog: Go for your quick win! Migrate Identity Provisioning tenants to SAP Cloud Identity infrastructure](https://community.sap.com/t5/technology-blogs-by-sap/go-for-your-quick-win-migrate-identity-provisioning-tenants-to-sap-cloud/ba-p/13536739)
* [Help Documenation: Migrate Identity Provisioning Bundle Tenant](https://help.sap.com/docs/identity-provisioning/identity-provisioning/migrate-identity-provisioning-bundle-tenant)

## 6. Create API User in SuccessFactors

An API user with **Allow Admin to Access OData API through Basic Authentication** permission is required in SuccessFactors.  This user will be used to create the BTP destinations in later steps.  If the user doesn't already exist, follow the steps in the **Create API User in SuccessFactors** card to create a new API user with the correct permissions.  If you plan to use an existing API user from SuccessFactors, confirm that there aren't any IP restrictions in place for the API user.  If such IP restrictions are in place then the IPs of BTP data center where Joule will be setup must also be added to the list of whitelisted IPs. To see the list of BTP datacenters and the corresponding IPs, follow [Regions and API Endpoints Available for the Cloud Foundry Environment](https://help.sap.com/docs/btp/sap-business-technology-platform/regions-and-api-endpoints-available-for-cloud-foundry-environment).  See [2253200 - How to restrict the API access of a specific user by IP addresses] (https://userapps.support.sap.com/sap/support/knowledge/en/2253200) for more information.<br/>

![prepare_activation](3.jpg)

## 7. Activate Employee Central Quick Links

Joule supports various use cases that are specific to Employee Central module in SuccessFactors.  To enable Employee Central specific use cases, Employee Central Quick Links should already be enabled in SAP SuccessFactors.  If Employee Central Quick Links are not already enabled, follow the steps in **Activate Employee Central Quick Links** card.
  
## 8. Permissions Required in SuccessFactors

* Permissions to schedule jobs in SuccessFactors.  See [Scheduled Job Manager](https://userapps.support.sap.com/sap/support/knowledge/en/2906009)
* Permissions to [**Security Center >> X.509 Certificate Mapping**](https://userapps.support.sap.com/sap/support/knowledge/en/3300596).
* Manage Permission Roles and Manage Permission Groups access.  See [Granting Administrators Access to RBP](https://help.sap.com/docs/SAP_SUCCESSFACTORS_PLATFORM/cdd844b5f0744d238284e937deb73f39/0aa4fbb7d9914a448d70238b321ab101.html).
* Permissions to access **Extension Center** (see [Enabling Extension Center](https://help.sap.com/docs/SAP_SUCCESSFACTORS_PLATFORM/6c9f794920b947648737d914a669f195/f1eface4d74545c1a29a9de970b686d9.html?version=2405))  in SAP SuccessFactors Admin Center that include:
  * **Admin Access to MDF OData API** permission from the **Metadata Framework** category.
    ![prepare_activation](7.jpg)
  * **Create Integration with SAP BTP** permission from the **Manage Extensions** on SAP BTP category.
    ![prepare_activation](6.jpg)

**NOTE:** If Extension Center is not visible in Admin Center, choose either one of 2 options documented in note [3414682 - Unable to View Extension Center even related permissions are granted](https://userapps.support.sap.com/sap/support/knowledge/en/3414682) to activate Extension Center.

## 9. Determine SuccessFactors Data Center

To validate whether SuccessFactors instance can be setup for Joule, you will need to find the correct data center for your SAP SuccessFactors instance.  To learn more, visit [2089448 - SuccessFactors Data Center Name, Location, Production Login URL, Production Domain Name, External Mail Server Details and Outbound IP addresses](https://me.sap.com/notes/0002089448)

For example, DC68 data center tenants the screenshot shows the corresponding SuccessFactors tenant URLs.<br/>
![prepare_activation](1.jpg)

**Note**: If your SuccessFactors tenant is using common super domain, make note of the **Pre CSD Migration URL** of your tenant as well.  This URL will be used when running the booster in the BTP Global Account.

## 10. Find API URLs for SuccessFactors tenant

We need to know the **API Server** and **mTLS Certificate Server** URLs for our SuccessFactors tenant.  This information can be found here: [List of SFSF API Servers](https://help.sap.com/docs/SAP_SUCCESSFACTORS_PLATFORM/d599f15995d348a1b45ba5603e2aba9b/af2b8d5437494b12be88fe374eba75b6.html)<br/>
![prepare_activation](2.jpg)

For example, for DC68 production SuccessFactors tenants the corresponding **API Server** and **mTLS Certificate Server** URLs for our SuccessFactors tenant are:   
* **API Server**: https://api4.successfactors.com/                         
* **mTLS Certificate Server**: https://api4.cert.successfactors.com

## 11. SAP Cloud Identity Services tenant(s) and SuccessFactors Details

To setup Joule, the SuccessFactors tenant should already be integrated to use SAP Cloud Identity Service.  To find out which IAS/IPS instance the SuccessFactors tenant is using access **Admin Center >> Monitoring Tool for Identity Authentication Service/Identity Provisioning Service Upgrade**.  Make a note of the **Identity Authentication Service Tenant URL** and **Identity Provisioning Service Tenant URL**.  When setting up the BTP subaccount trust with IAS in later steps, it will be important to select the same IAS tenant that is used by SuccessFactors.  In addition, the date of when the activatation was done will be important to pick the right domain to use when setting up BTP Subaccount trust to SAP Cloud Identity Authentication Service (IAS). <br/>
![prepare_activation](4.jpg)

## 12. Domain used for SuccessFactors trust with SAP Cloud Identity Services

In addition to knowing the URL of SAP Cloud Identity Services tenant, we also need to know which domain was used during the integration between SuccessFactors and SAP Cloud Identity Authentication Service.  Use the table below to determine which domain is relevant for your integration:

| Criteria     | Domain to Use |
| ----------- | ----------- |
| SuccessFactors tenant already migrated to common super domain   | ias.accounts.**cloud.sap**     | 
| **Initiate the SAP Cloud Identity Services Identity Authentication Service Integration** job triggered **after Nov 20, 2023** in Upgrade Center   | ias.accounts.**cloud.sap**     | 
| **Initiate the SAP Cloud Identity Services Identity Authentication Service Integration** job triggered **before Nov 20, 2023** in Upgrade Center   |ias.accounts.**ondemand.com**     | 

Knowing which domain to use is relevant when setting up trust between BTP Subaccount and SAP Cloud Identity Authentication Service in later steps.

## 13. Validate SuccessFactors IP Restriction Management

Some of our SuccessFactors customers have IP restrictions in place to prevent user access to SuccessFactors from outside of that IP range.  For more information on IP Restriction Management in SuccessFactors follow this SAP Note: [2089414 - System: How to restrict access to SuccessFactors by IP address - IP Restriction Management](https://userapps.support.sap.com/sap/support/knowledge/en/2089414).  If such IP restrictions are in place then the IPs of BTP data center where Joule will be setup must also be added to the list of whitelisted IPs. To see the list of BTP datacenters and the corresponding IPs, follow [Regions and API Endpoints Available for the Cloud Foundry Environment](https://help.sap.com/docs/btp/sap-business-technology-platform/regions-and-api-endpoints-available-for-cloud-foundry-environment)<br/>

**WARNING**: DO NOT add the BTP IPs unless you are already restricting user access to SuccessFactors based in IPs.  Please read note 2089414 in detail before making any changes in the **IP Restriction Management** app in SuccessFactors.
