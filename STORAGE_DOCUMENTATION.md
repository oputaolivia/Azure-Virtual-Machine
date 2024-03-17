# Manage Azure Storage
---

# Job skills
- Task 1: Create and configure a storage account.
- Task 2: Create and configure secure blob storage.
- Task 3: Create and configure secure Azure file storage.

## Task 1: Create and configure a storage account.
1. Login to the [Azure Portal](https://portal.azure.com/)
2. Search for and select `Storage accounts`, and then click + __Create__.
3. On the __Basics__ tab of the Create a __storage account__ blade, I specified the subscription and resource group in the project details section.
4. In the Instance details section I give the storage account a name, selected __South Africa North__ as region, performance to __Standard__, redundancy to __Geo-redundant storage__ and then enabled __Make read access to data in the event of regional availability__.
5. On the __Advance__ tab, everything was left as default.
6. On the __Networking__ tab, for the network access I selected __Disable public access and use private access__, others where left t default.
7. On __Data Protection__ tab, everything was left as default.
8. On __Encryption__ tab, everything was left as default.
9. Select ___Review__, wait for the validation process to complete, and then click __Create__.
10. Once the storage account is deployed, select __Go to resource__.
> Review the Overview blade and the additional configurations that can be changed. These are global settings for the storage account. Notice the storage account can be used for Blob containers, File shares, Queues, and Tables.
11. In the __Security + Networking__ section, select the __Networking__ blade. 
12. I changed the public network access from disabled to __Enabled from selected virtual networks and IP addresses__. In the Firewall section, I checked the box for Add your client IP address and saved my changes.
> In the Redundancy blade at the Data management section, I Noticed the information about your primary and secondary data center locations. The storage account was replicated in a single datacenter within my region geography.
13. In the __Data management section__, select the __Lifecycle management__ blade, and then select __Add a rule__.
14. On the __details__ tab, input  rule name and leave others as default.
15. On the __Base Blob__ tab, select _last modified_ and input 30 days in the __if based blobs were__ section and select __Move to cool__ in the __then__ section.
> What this does is to move the file to cool storage, if the last time it was modified was 30 days ago. There are 3 tiers of Azure storage; Cool, Hot and Archieve.

## Create and configure secure blob storage
Create a blob container and upload an image. Blob containers are directory-like structures that store unstructured data.

### Create a blob container and a time-based retention policy
1. Continue in the Azure portal, working with the already created storage account.
2. In the __Data storage__ section, select __Containers__ blade.
3. Click __+ Container__ and Create a container. Input a container name and notice that the access level is set to private.
4. On the container, scroll to the ellipsis (…) on the far right, select __Access Policy__.
5. In the Immutable blob storage area, select __Add policy__. 
6. I selected __Time based retention__ for policy type and Set retention period for	180 days, then saved.

### Manage blob uploads
1. On the __Container__ page, select the just created container.
2. Select an image from local machine and upload.
3. On the __Upload blob blade__, expand the __Advanced__ section. I choice __Block blob__ as the blob type, selected a block size of __4 MiB__ , chose Hot for the access tier, added an upload folder and selected __Use existing default container scope__ as  the encryption scope.
4. click on __Upload__.
5. Select the uploaded file and review the options including Download, Delete, Change tier, and Acquire lease.
6. copy the blob file url, open an InPrivate browser and paste it. I noticed that i get an error message saying `Public Access Not Permitted`.
> This is expected, since the container you created has the public access level set to Private (no anonymous access).

### Configure limited access to the blob storage
1.  On the container, scroll to the ellipsis (…) on the far right, select __Generate SAS__.
2. Select the signing key as __Key 1__, assign a __read__ permission, enter start and expiry dates & time, leave allowed IP addresses blank and click __Generate SAS token and URL__.
3. Copy the __Blob SAS URL__ and paste it in the InPrivate Browser.
> Viola!! the image i now accessible.

## Task 3: Create and configure an Azure File storage
Create and configure Azure File shares. Storage Browser would be used to manage the file share.

### Create the file share and upload a file
1. In the storage account click on __File shares__ blade in the __data storage__ section and click __+ File Share__
2. On the __Basics__ tab I gave the file share a name, and kept everyother settings at default.
3. On the __BackUp__ tab, I disabled backup.
4. Click __Review + Create__, after validation select __Create__.

### Explore Storage Browser and upload a file
1. Returning to the storage account, select the __Storage Browser__ blade. Select __File shares__ and verify the file share directory that was created the previous section is present and select __Upload__.
> The Azure Storage Browser is a portal tool that lets you quickly view all the storage services under your account.
2. Chose a file from my local machine and clicked on __upload__.

### Restrict network access to the storage account
1. In the portal, search for and select __Virtual networks__ and click on  __+ Create__. 
2. On the __Basics__ tab. In the project details section assign a resource group and subscription. In the instance details section, give the virtual network a name in my case `vnet1` and I chose `South Africa North` as my region.
3. Taking the defaults for other parameters, select __Review + create__, and then __Create__.
4. Once the virtual network has been created, select __Go to resource__.
5. In the __Settings__ section, select the __Subnets blade__, select the default subnet. In the Service endpoints section I chose Microsoft.Storage in the Services drop-down and saved.
6. On the __Security + Networking__ section, select the __Networking__ blade and click on __+ Add existing Virtual Network__. select the subscription, the just created virtual network and leave the subnets as default and click __Enable__.
7. After it has been enabled click on __Add__.
8. In the __Firewall__ section, Delete the machine IP address. 
> Allowed traffic should only come from the virtual network.
9. Click on __Save__.
10. Select the Storage browser and Refresh the page. Navigate to the file share or blob content that was created.
> I received a message not authorized to perform this operation, because i am not connecting from the virtual network. 
