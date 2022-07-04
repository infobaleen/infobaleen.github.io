# Import data to the platform

There are various ways to import data to the platform, here we present the most common use cases.


## Using a database connection (for Centra, Voyado, etc)

First, make sure you know the origin files to fetch. If files are fetched from 

Go to the platform and then to `Admin -> Configuration` (can be found at the top right menu by clicking the three dots, see example image below).



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



### Make arbitrary query 
Create a source and make an arbitrary query similar to ``` SELECT * FROM `users.gz` ``` for Centra. You can list possible paths by using ``` SELECT * FROM `*` ```. 

This will trigger a proxy sync, and if a Centra customer the `.gz` files will appear once completed. This normally takes 1-5 hours.

<img width="1198" alt="Screenshot 2022-05-10 at 10 31 03" src="https://user-images.githubusercontent.com/4352260/167585099-4bbcfd77-008e-455d-93bf-89e257d6b306.png">



### How to verify that the sync works?

Choose the source you created and press the pen to edit it. Go to the `ADD QUERY` tab and choose ```“SELECT * FROM `*`”```. 

If the sync is ready, you will see a list of files to choose from, for example, `users.gz`, `items.gz`, `interactions.gz`, see image below. If you see the files imported you are now ready to [create sources!](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Menu/Manage%20Data/Sources.md)

<img width="954" alt="Screenshot 2022-05-10 at 14 59 33" src="https://user-images.githubusercontent.com/4352260/167635009-bee5c795-271c-49f9-a92c-840a415f120f.png">



## Using a file
Go to the platform and then to `Manage data -> Import files` (can be found at the top right menu by clicking the three dots, see example image below). 

If the customer sent their data in a csv-file, drag it to the drop box for importing files.

Uploaded files are available from the "imports (csv-fs)" database connection when creating new sources (see next step).

<img width="1216" alt="Screenshot 2022-05-10 at 10 31 52" src="https://user-images.githubusercontent.com/4352260/167585247-b7f840a9-a43a-4a7d-bf76-1757e4f688cb.png">


## Using a feed

A feed is a file that contains a list of products that often is used to advertise through Google Merchant Center. Often these feeds are updated with latest information which means Infobaleen can use the feed to add relevant product details to the platform, such as image link data.

Feeds are most often published as a public URL in format `.xml`, see below an example:

<img width="842" alt="Screenshot 2022-06-03 at 15 59 39" src="https://user-images.githubusercontent.com/4352260/171869182-84200505-15de-48e9-a099-d5ed04c8bdca.png">

### Adding a feed as a data source

1. Get the public URL of the feed
2. Add a new `source`, often it is a good idea to add a "Merge Filter" to avoid fetching too much data (you can for example add `now() < toFloat(last_seen) + 7*24*3600`)
3. Add a query similar to below and also add `decoder=head` in the field `Preprocessor directives` to show the file structure. Note that you have to write `url:` before `https://`, see example below
```
SELECT
    *
FROM `url:https://shop.com/plugin-export/shoppingfeed/se`  
```

[Note that you have to write **url:** before https://]  

### Preprocessor directives
Start by writing `decoder=xml` (or `=feed`)

to show the file structure, in this case it looks like this.

![image](https://user-images.githubusercontent.com/102239423/169991270-10e97b4e-b5fd-4df8-968c-320119f9ee71.png)

**decoder:** describes what file format, xml, csv, json etc.  
**root:** navigates the file and shows where you want to read data.  
**rowtag:** selects the object.  
**pluck:** inside your rowtag you can have multiple data columns, pluck lets you choose wich you want to get.  

Below is one example with `root=feed.channel` and one example with `root=rss.channel`:

<img width="543" alt="Screenshot 2022-06-10 at 08 26 05" src="https://user-images.githubusercontent.com/4352260/173004337-734dcc11-992c-4920-975b-3d87f5ad362d.png">
<img width="549" alt="Screenshot 2022-06-10 at 08 26 46" src="https://user-images.githubusercontent.com/4352260/173004348-827d98b1-e609-4d09-aa5f-63ce9034443e.png">

In the first image example, the resulting preprocessing directives to fetch the feed are:  

`decoder=xml`  
`root=rss.channel`  
`rowtag=item`  
`pluck=google_product_category,price`  
resulting in this outcome
![image](https://user-images.githubusercontent.com/102239423/169994099-991016fc-cdb8-4e63-a60a-83726a1f7e87.png)

