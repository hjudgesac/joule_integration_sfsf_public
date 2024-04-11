## **Create Subaccount and Cloud Foundry Space**


1. Access [BTP Cockpit URL](https://cockpit.btp.cloud.sap).
2. Select the BTP Global Account that has the Joule entitlements and click **Continue**.                         
![run_booster](1.png)

3. From the Navigation Pane on the left, select **Account Explorer**.  Click **Create** >> **Subaccount**.
![run_booster](3.jpg)

4. Specify **Display Name** and **Region** and click **Create**.                             
![run_booster](3-1.jpg)   
**Note**: The **Region** must be from one of the supported data centers for Joule and correspond to your SuccessFactors tenant.  See [Data Center Mapping between SAP SuccessFactors and Joule](https://help.sap.com/docs/joule/serviceguide/data-center-mapping-between-sap-successfactors-and-joule)

5. Click **Enable Cloud Foundry**. 
![run_booster](4.jpg)

6. Leave the default settings and click **Create**.              
![run_booster](5.jpg)

7. From the Navigation Pane, expand **Cloud Foundry** and click **Spaces**.                                                         
![run_booster](6.jpg)

8. Click **Create Space**.                                                                                                                   
![run_booster](7.jpg)

9. Specify a **Space Name** and click **Create**.                                       
![run_booster](8.jpg)


## **Add Entitlements**


1. From the Navigation Pane, select **Entitlements** and click **Edit**.
![run_booster](9.jpg)

2. Click **Add Service Plans**.                           
![run_booster](10.jpg)

3. Search for "Joule".  Click **Joule** and choose **foundation (Application)** from the list of available plans.
![run_booster](11.jpg)

4. Search for "workzone".  Click **SAP Build Work Zone, standard edition** and choose the **foundation** and **foundation (Application)** plans.  Click **Add 3 Service Plans**.                                       
![run_booster](12.jpg)

5. Click **Save**.                      
![run_booster](13.jpg)


## **Add Trusted Domains**


1. From the Navigation Pane, select **Settings** and click **Add**.
![run_booster](14.jpg)

2. Add your **SuccessFactor tenant domain** and click **Add**.  For example, https:///hcm-us10.hr.cloud.sap.                  
**NOTE**:  Do not add trailing slash(/) at the end of the URL.     
![run_booster](15.jpg)
 
