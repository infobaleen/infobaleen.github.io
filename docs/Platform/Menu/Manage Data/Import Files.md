# Table of Contents
1. [Import data to the platform](#import-data-to-the-platform)
    1. [Using a database connection (for Centra, Voyado, etc)](#using-a-database-connection-for-centra-voyado-etc)
        1. [Set up a configuration](#set-up-a-configuration)
        1. [Make arbitrary query ](#make-arbitrary-query)
        1. [How to verify that the sync works?](#how-to-verify-that-the-sync-works?)
    1. [Using a file](#using-a-file)

[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Import data to the platform

[*Back to top*](#table-of-contents)

## Using a database connection (for Centra, Voyado, etc)

First, make sure you know the origin files to fetch
* [For Voyado ](#find-voyado-files-to-import)

Go to the platform and then to `Admin -> Configuration` (can be found at the top right menu by clicking the three dots, see example image below).

[*Back to top*](#table-of-contents)

### Set up a configuration
Add a database and name the `Database` based on the what system they use (centra, voyado, etc), and choose the matching `Driver`. In the `Config` field, check the standard URL provided by the corresponding ecommerce platform. 

**Notes:**
* A key or token is needed to access the databases. This key is listed under `Admin -> Secrets`. 
* For **Centra** customers there are fields that need to be specified:
    * `"Limit":100000` : This is a limit so that we do not overload Centra servers when fetching data
    * `"Store":1,"Market":3,"PriceList":19,"Warehouses":[2,3]`: These are specifications to fetch the correct data, the customer seldom knows this but Centra should have the information. 
* For **Voyado** customers there are fields that need to be specified:
    * `"Directories"`: These are the directories that can be found in the [Azure data lake]((#find-voyado-files-to-import))
    * There are defauly directories that will be accessible without specifying them, these are `store/`, `receiptItems/`, `article/` and `allContacts/`
* There is an option also to `Add Integration`. This part can be skipped, it is only used when we send data to customers. 

[*Back to top*](#table-of-contents)

### Make arbitrary query 
Create a source and make an arbitrary query similar to ``` SELECT * FROM `users.gz` ``` for Centra. You can list possible paths by using ``` SELECT * FROM `*` ```. 

This will trigger a proxy sync, and if a Centra customer the `.gz` files will appear once completed. This normally takes 1-5 hours.

<img width="1198" alt="Screenshot 2022-05-10 at 10 31 03" src="https://user-images.githubusercontent.com/4352260/167585099-4bbcfd77-008e-455d-93bf-89e257d6b306.png">

[*Back to top*](#table-of-contents)

### How to verify that the sync works?

Choose the source you created and press the pen to edit it. Go to the `ADD QUERY` tab and choose ```“SELECT * FROM `*`”```. 

If the sync is ready, you will see a list of files to choose from, for example, `users.gz`, `items.gz`, `interactions.gz`, see image below. If you see the files imported you are now ready to [create sources!](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Menu/Manage%20Data/Sources.md)

<img width="954" alt="Screenshot 2022-05-10 at 14 59 33" src="https://user-images.githubusercontent.com/4352260/167635009-bee5c795-271c-49f9-a92c-840a415f120f.png">

[*Back to top*](#table-of-contents)

## Using a file
Go to the platform and then to `Manage data -> Import files` (can be found at the top right menu by clicking the three dots, see example image below). 

If the customer sent their data in a csv-file, drag it to the drop box for importing files.

Uploaded files are available from the "imports (csv-fs)" database connection when creating new sources (see next step).

<img width="1216" alt="Screenshot 2022-05-10 at 10 31 52" src="https://user-images.githubusercontent.com/4352260/167585247-b7f840a9-a43a-4a7d-bf76-1757e4f688cb.png">

[*Back to top*](#table-of-contents)

