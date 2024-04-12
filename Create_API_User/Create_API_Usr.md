**Note**: Follow these steps only if you don't have an existing API user in SuccessFactors with the required permissions.
1. Login to SuccessFactors application.
2. Go to **Admin Center**-> **Import Employee Data** and Generate the template for Basic Import.</br>
![Create_API_User](1download_template.jpg)
3. Enter relevant detail for following fields:
Status, UserId, Username, FirstName, LastName, Email ID, Manager (as NO_MANAGER ) and HR as (NO_HR) fields
4. **Save** the changes.
5. Go back to **Import Employee Data** screen and Import the csv file for Entity **Basic Import** after data validation.</br>
![Create_API_User](2Basic_Import.jpg)
6. Access **Admin Center > Reset User Password**.
7. Search for the newly created API user and reset the user password.</br>
![Create_API_User](3reset_password.jpg)
8. Access **Admin Center > Manage Permission Role**.
9. Select an existing **Permission Role** or create a new one.
10. Assign **Manage Integration Tools** > **Allow Admin to Access OData API through Basic Authentication** and click **Save Changes**:</br>
![Create_API_User](1API_Permission.jpg)
11. Assign this permission role to a permission group in SuccessFactors.  Ensure the newly created user is also a a member of this group.
