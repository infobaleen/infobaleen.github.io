# Table of Contents
1. [Platform setup ](#platform-setup)
    1. [1. Import data to platform](#1-import-data-to-platform)
        1. [Using a database connection (for Centra, Voyado, etc)](#using-a-database-connection-for-centra-voyado-etc)
            1. [Set up a configuration](#set-up-a-configuration)
            1. [Make arbitrary query [What does this mean, and where to do it???]](#make-arbitrary-query-what-does-this-mean-and-where-to-do-it???)
            1. [How to verify that the sync works?](#how-to-verify-that-the-sync-works?)
        1. [Using a file](#using-a-file)
    1. [2. Create sources](#2-create-sources)
    1. [3. Create data model](#3-create-data-model)
    1. [4. Create dashboards](#4-create-dashboards)
        1. [Add expressions](#add-expressions)
        1. [Tip: Copy a dashboard to another data model](#tip-copy-a-dashboard-to-another-data-model)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Platform setup 

In order to create dashboards we need to complete three steps: 

1. Import data to the platform
2. Create sources that contain data from one or more imported files
3. Create a data model based upon the sources
4. Create dashboards

Testing can be done at [d15.infobaleen.com](https://d15.infobaleen.com/) that consists of testdata created by us. 

[*Back to top*](#table-of-contents)

## 1. Import data to platform

[*Back to top*](#table-of-contents)

### Using a database connection (for Centra, Voyado, etc)

Go to the platform and then to `Admin -> Configuration` (can be found at the top right menu by clicking the three dots, see example image below).

[*Back to top*](#table-of-contents)

#### Set up a configuration
Add a database and name the `Database` based on the system they use (centra, voyado, etc), and choose the matching `Driver`. In the `Config` field, check the standard URL provided by the corresponding ecommerce platform. 

**Notes:**
* A key or token is needed to access the databases. This key is listed under `Admin -> Secrets`. 
* For Centra customers there are fields that need to be specified:
    * `"Limit":100000` : This is a limit so that we do not overload Centra servers when fetching data
    * `"Store":1,"Market":3,"PriceList":19,"Warehouses":[2,3]`: These are specifications to fetch the correct data, the customer seldom knows this but Centra should have the information. 
* There is an option also to `Add Integration`. This part can be skipped, it is only used when we send data to customers. 

[*Back to top*](#table-of-contents)

#### Make arbitrary query [What does this mean, and where to do it???]
Create a source and make an arbitrary query similar to ``` SELECT * FROM `users.gz` ```. 

This will trigger a proxy sync, and the `.gz` files will appear once completed. This normally takes 1-5 hours.

<img width="1198" alt="Screenshot 2022-05-10 at 10 31 03" src="https://user-images.githubusercontent.com/4352260/167585099-4bbcfd77-008e-455d-93bf-89e257d6b306.png">

[*Back to top*](#table-of-contents)

#### How to verify that the sync works?

Choose the source you created and press the pen to edit it. Go to the `ADD QUERY` tab and choose ```“SELECT * FROM `*`”```. 

If the sync is ready, you will see a list of files to choose from, for example, `users.gz`, `items.gz`, `interactions.gz`, see image below. If you see the files imported you are now ready to create sources!

<img width="954" alt="Screenshot 2022-05-10 at 14 59 33" src="https://user-images.githubusercontent.com/4352260/167635009-bee5c795-271c-49f9-a92c-840a415f120f.png">

[*Back to top*](#table-of-contents)

### Using a file
Go to the platform and then to `Manage data -> Import files` (can be found at the top right menu by clicking the three dots, see example image below). 

If the customer sent their data in a csv-file, drag it to the drop box for importing files.

Uploaded files are available from the "imports (csv-fs)" database connection when creating new sources (see next step).

<img width="1216" alt="Screenshot 2022-05-10 at 10 31 52" src="https://user-images.githubusercontent.com/4352260/167585247-b7f840a9-a43a-4a7d-bf76-1757e4f688cb.png">

[*Back to top*](#table-of-contents)

## 2. Create sources
When the data is imported, go to `Manage Data -> Sources` and create a new source by clicking the purple plus sign as seen in the below image. 

1. Name the source `import_[source of data]_[type of data]` where `[source of data]` specifies where the data comes from (centra, voyado, etc), and the `[type of data]` specifies the data type (items, users, interactions, etc). 

<img width="1050" alt="Screenshot 2022-05-10 at 10 53 48" src="https://user-images.githubusercontent.com/4352260/167589964-27e4a8fe-d3d0-4382-a696-21d759331cd9.png">

2. Choose an identifier for the source using the `Id columns` field.  If the source you’re creating is for:
    * **interactions**: we want to identify each interaction through a user, an item and the time of the purchase, therefore choose user,ts,item under id columns and then press create.
    * **items**: we want to identify each item by using an item id (often sku or variant). 
    * **users**: we want to identify each user by using a user id. 

The fields `Comment` and `Merge Filter` can be left empty, and you can press `CREATE`. 

3. Choose database connection and create a `QUERY` 
If it’s a centra/voyado customer choose that option, if the files were uploaded manually, choose imports.

You can now see the query stage, as standard ```“SELECT * FROM `*`”``` will show, if you press “EXECUTE PREVIEW SUMMARY” you will see all the imported files you can choose to gather data from. Copy the filename you want to use and enter that name in the query above, like `SELECT * FROM [ENTER FILENAME HERE]`.

Copy the queries (depending on what system the customer has) from here:

* [Centra queries](https://github.com/infobaleen/customer-success/wiki/Manage-Data#centra-queries)
* [Voyado queries](https://github.com/infobaleen/customer-success/wiki/Manage-Data#voyado-queries)

The import file is now done, press sync and save to exit. 

4. Now repeat the "Create source"-step 2 but name the file `model_[source of data]_[type of data]` (the use same identifier as in the import file). 
    * In the `Choose database connection` now choose `source` instead, and press `execute preview summary`, now choose the import source file and edit the query to select from that, like "`SELECT * FROM ENTER_SOURCENAME_HERE`" and then press `Save and sync`.

[*Back to top*](#table-of-contents)

## 3. Create data model
The next step is to create a data model using the sources we just created. Go to the three dots on the top right corner of the screen and select `Manage Data -> Data models`. 

Create a new data model (the purple plus sign on the right side) and choose a representative data model name.
 * If it’s a Centra customer you can, for example, name the data model “Centra”
 * If it’s a customer with manually added files you can, for example, name the data model “Customer name” 

Select the correct source in the data model for interactions, users and items and press `Save`.

[*Back to top*](#table-of-contents)

## 4. Create dashboards
To create a dashboard, press the `Analytics` button in the top left corner and then press the `+` icon. Note that each data model have different dashboards, on the top right side of the screen you can select what data model the dashboards should use.

* `Name`: The name of the dashboard. Preferred is to use Title Case, i.e. not "Customer purchases" but "Customer Purchases" for naming. 
* `Select Role`:
  * **interactions**: If the dashboard shows data of interactions between for example a user, an item and the time of the purchase
  * **user**: If the dashboard shows data about users
  * **item**:  If the dashboard shows data about items
* `Select number of columns`: This specifies the grid size of the dashboard. The grid is used when you move dashboard elements and they "snap" to the grid.

<img width="941" alt="Screenshot 2022-05-10 at 14 03 54" src="https://user-images.githubusercontent.com/4352260/167624147-1a3adf8e-6c9f-4552-bd42-56a54422b690.png">

To create richer dashboards, there is often a need to create expressions based on the data. To do this, see the info in the section below.

[*Back to top*](#table-of-contents)

### Add expressions
Open the data model and press `Edit` (the pen in the right top corner). Now press `Add suggested expressions` located under each segment for interactions/users/items.

* [Example of Data model expressions](https://github.com/infobaleen/customer-success/wiki/Expressions)

When you have created standard expressions based on the data used, scroll down and save. 

[*Back to top*](#table-of-contents)

### Tip: Copy a dashboard to another data model

After you have set up your dashboard, do the following:

1. Go to the dashboard overview and create a copy of your dashboard, see below image.

<img width="1014" alt="Screenshot 2022-05-11 at 11 14 04" src="https://user-images.githubusercontent.com/4352260/167815562-d7e0ed47-7827-4b46-ab79-abe9ea9af0ad.png">

2. Edit your newly created dashboard, click `Dashboard Settings`, and change the data model. If all expressions exists in the other model, the dashboard will be copied. Remember to `SAVE` the dashboard after the changes.

<img width="1015" alt="Screenshot 2022-05-11 at 11 15 33" src="https://user-images.githubusercontent.com/4352260/167815065-9a1f0580-e86d-4b49-a6c7-e5facb76e241.png">
<img width="1043" alt="Screenshot 2022-05-11 at 11 16 12" src="https://user-images.githubusercontent.com/4352260/167815073-b1af1b0f-8d4b-48cd-a944-9c6345d3d216.png">
<img width="1074" alt="Screenshot 2022-05-11 at 11 16 17" src="https://user-images.githubusercontent.com/4352260/167815392-c2a11126-c4d7-4bf1-91a8-f010ca29b446.png">

[*Back to top*](#table-of-contents)
