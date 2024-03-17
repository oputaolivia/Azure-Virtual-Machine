# Manage Azure Storage
---

# Job skills
- Task 1: Create and configure a storage account.
- Task 2: Create and configure secure blob storage.
- Task 3: Create and configure secure Azure file storage.

## Task 1: Create and configure a storage account.
Create a blob container and upload an image. Blob containers are directory-like structures that store unstructured data.
### Create and configure secure blob storage
1. Login to the [Azure Portal](https://portal.azure.com/)
  ![1](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/70d197a4-abe5-4f19-b3a6-fe82812b88b4)

2. Search for and select `Storage accounts`, and then click + __Create__.
   ![2](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/c561b51f-ef73-4281-a54b-312f32b0f021)

3. On the __Basics__ tab of the Create a __storage account__ blade, I specified the subscription and resource group in the project details section.
   ![3](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/4c26ef9a-7250-43cd-afee-ad5dbed430ef)

4. In the Instance details section I give the storage account a name, selected __South Africa North__ as region, performance to __Standard__, redundancy to __Geo-redundant storage__ and then enabled __Make read access to data in the event of regional availability__.
   ![4](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/2d85acc1-83fc-4c54-acf4-5f7023fd7cce)

5. On the __Advance__ tab, everything was left as default.
    ![5](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/2c82aeeb-0964-4b0d-8cc3-f5c64cf3fa8b)

6. On the __Networking__ tab, for the network access I selected __Disable public access and use private access__, others where left default.
    ![6](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/33295fa0-5caf-4144-a712-1166bd6cb983)

7. On __Data Protection__ tab, everything was left as default.
    ![7](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/b0ec8721-5d7b-4f50-90c7-7b178d684242)

8. On __Encryption__ tab, everything was left as default.
  ![9](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/bb56f879-04a5-4fe8-b1ef-44d5c0cad939)

9. Select ___Review__, wait for the validation process to complete, and then click __Create__.
    ![10](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/74d275ed-70df-42e5-892f-e3c272678791)

10. Once the storage account is deployed, select __Go to resource__.
    ![12](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/03c4db76-7361-4370-b22c-a9c2bd3eb2f3)

> Review the Overview blade and the additional configurations that can be changed. These are global settings for the storage account. Notice the storage account can be used for Blob containers, File shares, Queues, and Tables.

11. In the __Security + Networking__ section, select the __Networking__ blade.
    ![13](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/1d6142ef-04bc-4e39-9603-b1afdeaf4099)

12. I changed the public network access from disabled to __Enabled from selected virtual networks and IP addresses__. In the Firewall section, I checked the box for Add your client IP address and saved my changes.
    ![14](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/a26d2d95-7c31-435e-83c7-0292eb095a65)

> In the Redundancy blade at the Data management section, I Noticed the information about your primary and secondary data center locations. The storage account was replicated in a single datacenter within my region geography.
![15](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/b6a733d3-05f1-4fe5-aee0-8273360a4cf2)

13. In the __Data management section__, select the __Lifecycle management__ blade, and then select __Add a rule__.
    ![16](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/7d740a19-99dd-43c6-beb7-106f479d6c18)

14. On the __details__ tab, input  rule name and leave others as default.
    ![17](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f4e6e6d4-bcd3-4e5e-9b79-41b85098de87)

15. On the __Base Blob__ tab, select _last modified_ and input 30 days in the __if based blobs were__ section and select __Move to cool__ in the __then__ section.
    ![18](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/dd78acbd-99d7-4b20-aaba-014da67cb04b)
> What this does is to move the file to cool storage, if the last time it was modified was 30 days ago. There are 3 tiers of Azure storage; Cool, Hot and Archieve.

### Create a blob container and a time-based retention policy
1. Continue in the Azure portal, working with the already created storage account.
2. In the __Data storage__ section, select __Containers__ blade.
   ![19](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/90b85d4e-87b5-4dc8-856d-452aea77f413)

3. Click __+ Container__ and Create a container. Input a container name and notice that the access level is set to private.
   ![20](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f3e62888-a2db-4623-8eb4-9559e614d13f)

4. On the container, scroll to the ellipsis (…) on the far right, select __Access Policy__.
   ![21](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/37c76a45-6e82-4d6b-93c4-a98f97deaa97)

5. In the Immutable blob storage area, select __Add policy__.
   ![22](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/399803fb-1f91-4e1a-883f-7b945551afd8)

6. I selected __Time based retention__ for policy type and Set retention period for	180 days, then saved.
  ![23](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5f9bb1b3-cdca-4301-974e-17bf4f117b33)

### Manage blob uploads
1. On the __Container__ page, select the just created container.
   ![24](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f75764c2-368b-46bf-9a89-4d70dd65cbce)

2. Select an image from local machine and upload.
   ![25](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/ca530d21-fe78-4e0b-936e-e6cd56a2110d)

3. On the __Upload blob blade__, expand the __Advanced__ section. I choice __Block blob__ as the blob type, selected a block size of __4 MiB__ , chose Hot for the access tier, added an upload folder and selected __Use existing default container scope__ as  the encryption scope.
   ![26](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/d0c20194-12eb-4673-9ebd-e2756fa3cef7)

4. click on __Upload__.
5. Select the uploaded file and review the options including Download, Delete, Change tier, and Acquire lease.
   ![27](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/632cbdf3-97f6-49c8-9ee5-f6554253c664)

6. Copy the blob file url, open an InPrivate browser and paste it. I noticed that i get an error message saying `Public Access Not Permitted`.
    ![28](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/67a78cac-d7c2-4464-a9c7-f349d29f9f95)

> This is expected, since the container you created has the public access level set to Private (no anonymous access).

### Configure limited access to the blob storage
1.  On the container, scroll to the ellipsis (…) on the far right, select __Generate SAS__.
   ![21](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5d931fd0-6a91-4171-b2d9-010b40295362)

2. Select the signing key as __Key 1__, assign a __read__ permission, enter start and expiry dates & time, leave allowed IP addresses blank and click __Generate SAS token and URL__.
   ![29](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5fed533b-87e2-4c85-ab82-b20ef589133c)

3. Copy the __Blob SAS URL__ and paste it in the InPrivate Browser.
> Viola!! the image is now accessible.
  ![30](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/38641852-bea0-4cd3-9ebb-c4a9a5767cd1)

## Task 3: Create and configure an Azure File storage
Create and configure Azure File shares. Storage Browser would be used to manage the file share.

### Create the file share and upload a file
1. In the storage account click on __File shares__ blade in the __data storage__ section and click __+ File Share__.
   ![31](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/1cb9bd98-9c7b-4da4-912a-6214cc6054f5)

2. On the __Basics__ tab I gave the file share a name, and kept everyother settings at default.
   ![32](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5b86607d-1baa-4df4-9a89-aaf3ef73f539)

3. On the __BackUp__ tab, I disabled backup.
   ![33](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/53467ff1-d6d8-405d-be3e-b95be71c826d)

4. Click __Review + Create__, after validation select __Create__.
  ![34](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/7a7772c0-8b31-449a-845b-bab52f84a34c)

### Explore Storage Browser and upload a file
1. Returning to the storage account, select the __Storage Browser__ blade. Select __File shares__ and verify the file share directory that was created the previous section is present and select __Upload__.
   ![35](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f118d91f-cc56-4064-b6c5-e38315e6eabe)
> The Azure Storage Browser is a portal tool that lets you quickly view all the storage services under your account.

2. Chose a file from my local machine and clicked on __upload__.
   ![36](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/8c172cc0-9d60-4b01-8352-30775764e657)

### Restrict network access to the storage account
1. In the portal, search for and select __Virtual networks__ and click on  __+ Create__.
   ![37](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5beebb99-a0ae-48e0-b580-2c3bd5e61c68)

3. On the __Basics__ tab. In the project details section assign a resource group and subscription. In the instance details section, give the virtual network a name in my case `vnet1` and I chose `South Africa North` as my region.
   ![38](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/1285c892-bb4b-4528-a306-bd1a4c654a51)

5. Taking the defaults for other parameters, select __Review + create__, and then __Create__.
   ![39](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/32088dcf-8f90-4bfd-b1af-1e3d27159675)

7. Once the virtual network has been created, select __Go to resource__.
   ![Uploading 40.png…]()

9. In the __Settings__ section, select the __Subnets blade__, select the default subnet. In the Service endpoints section I chose Microsoft.Storage in the Services drop-down and saved.
10. On the __Security + Networking__ section, select the __Networking__ blade and click on __+ Add existing Virtual Network__. select the subscription, the just created virtual network and leave the subnets as default and click __Enable__.
    ![41](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/c0ed19fd-70e9-48f1-aa74-db52f48ca9ce)

12. After it has been enabled click on __Add__.
    ![42](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/b062bb9d-ce81-46ec-88d6-d40fdd97ffae)

14. In the __Firewall__ section, Delete the machine IP address.
    ![43](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/d38ece0f-5309-4c3a-8d06-77e219d746f3)

> Allowed traffic should only come from the virtual network.
9. Click on __Save__.
10. Select the Storage browser and Refresh the page. Navigate to the file share or blob content that was created.
> I received a message not authorized to perform this operation, because i am not connecting from the virtual network. 
![44](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/68e4f874-6c6a-4615-ab6d-d0dc02827c59)
![45](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/83c26eca-2e22-4e81-a263-b6bb70e48458)

