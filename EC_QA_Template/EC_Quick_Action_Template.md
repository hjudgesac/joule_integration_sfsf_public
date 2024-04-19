**NOTE**: Below steps are valid for Employee Central customers only.  You may skip this section if not testing the Employee Central specific use cases.
1. Go to **Admin Center**-> **Manage Employee Central Settings** and switch on **Employee Central Quick Actions**.</br>
![EC_QA_Template](1Manage_EC_Settings.png)

3. Go to **Admin Center >> Manage Permission Role**.
4. Under **Manage Business Configuration** >> **Employee Central Quick Action Template** enable the **Visibility** and **Actions** permissions.</br>
![EC_QA_Template](2MBC_Permission.png)

5. Save your changes.
7. Access **Admin Center** >> **Manage Data** and confirm **Employee Central Quick Action Template** objects are visible in the dropdown.</br>
![EC_QA_Template](6MD_dropdown.jpg)

9. If objects are not visible, then you can create the template objects by clicking on Create New and select Employee Central Quick Action Templates.</br>
![EC_QA_Template](4Create_EC_QA.png)

**Templates assignments to User**
Based on which use case's access you would like to assign to the user, you can control this via Role based permission
For example: To assign use case View Location, follow below steps:
1. Go to **Admin Center**-> **Manage Permission Role** and open User's role.
2. Navigate to **Employee Central Quick Actions** and select the use cse **View Location** as shown below:</br>
![EC_QA_Template](3QA_Permission.png)

4. Save Changes.

**NOTE**: Above configuration should allow you to get the response with data while interacting with JOULE.
