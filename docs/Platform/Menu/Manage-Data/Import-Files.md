# Import data to the platform

There are various ways to import data to the platform, here we present the most common use cases.

---

## Uploading files to the platform (CSV for example)
<details class="optional-class"><summary>Show more information</summary>
Go to the platform and then to `Manage data -> Import files` (can be found at the top right menu by clicking the three dots, see example image below). 

Drag the file to the drop-box in order to upload it to the platform

Uploaded files are available from the "imports (csv-fs)" database connection when creating new sources (see next step).

<img width="1216" alt="Screenshot 2022-05-10 at 10 31 52" src="https://user-images.githubusercontent.com/4352260/167585247-b7f840a9-a43a-4a7d-bf76-1757e4f688cb.png">
</details>

## Using a feed (Google Feed for example)

<details class="optional-class"><summary>Show more information</summary>

A feed is a file that contains a list of products that often is used to advertise through Google Merchant Center. Often these feeds are updated with latest information which means Sift Lab can use the feed to add relevant product details to the platform, such as image link data.

Feeds are most often published as a public URL in format `.xml`.
</details>

<h3> Adding a feed as a data source </h3>

<details class="optional-class"><summary>Show more information</summary>

1. Get the public URL of the feed
2. Add a new `source`, often it is a good idea to add a "Merge Filter" to avoid fetching too much data (you can for example add `now() < toFloat(last_seen) + 7*24*3600`)
3. Add a query similar to below and also add `decoder=head` in the field `Preprocessor directives` to show the file structure. Note that you have to write `url:` before `https://`, see example below
```
SELECT
    *
FROM `url:https://exampleurl.com/plugin-export/shoppingfeed/se`  
```

[Note that you have to write url: before https://]  


<h3> Preprocessor directives </h3>


Start by writing `decoder=xml` (or `=feed`) to show the file structure, it will in the preview window show the content.


decoder: describes what file format, xml, csv, json etc.  
root: navigates the file and shows where you want to read data.  
rowtag: selects the object.  
pluck: inside your rowtag you can have multiple data columns, pluck lets you choose wich you want to get.  

Below is an example of what to write in the preprocessor to fetch feed data correctly:
`decoder=xml`  
`root=rss.channel`  
`rowtag=item`  
`pluck=google_product_category,price`  

You can then run `EXECUTE PREVIEW QUERY` to see the result.

<h4> JSON Files </h4>
<details class="optional-class"><summary>Show more information</summary>
An example json file could look like:
```
[
    {
        "id": "",
        "user_id": "",
        "username": ""
    },
    {
        "id": "",
        "user_id": ""
        "username": ""
    }
]

SELECT * FROM `url:https://...json`  


<h3> preprocessing directive for json </h3>

`decoder=json`  
`json_prefix=[0]`

</details>
</details>

---

## Using a database connection

First, make sure you know the origin files to fetch. If files are fetched from 

Go to the platform and then to `Admin -> Configuration` (can be found at the top right menu by clicking the three dots, see example image below).



#### Set up a configuration
Add a database and name the `Database` based on the what system they use (centra, voyado, etc), and choose the matching `Driver`. In the `Config` field, check the standard URL provided by the corresponding ecommerce platform. 

**Note:** A key or token is most often needed to access databases. This key can be added under `Admin -> Secrets`. 

#### Make arbitrary query 
<details class="optional-class"><summary>Show more information</summary>

Create a source and make an arbitrary query similar to SELECT * FROM `users.gz` for Centra. You can list possible paths by using SELECT * FROM `*` . 

This will trigger a proxy sync, and in the case of a Centra customer as in the example image below, the `.gz` files will appear once completed. This normally takes 1-5 hours.


</details>


#### How to verify that the sync works
<details class="optional-class"><summary>Show more information</summary>

Choose the source you created and press the pen to edit it. Go to the `ADD QUERY` tab and choose SELECT * FROM `*`. 
<br>

If the sync is ready, you will see a list of files to choose from, for example, `users.gz`, `items.gz`, `interactions.gz`, see image below. If you see the files imported you are now ready to [create sources!](https://github.com/Sift Lab/customer-success/blob/main/Documentation/Platform/Menu/Manage%20Data/Sources.md)

<img width="954" alt="Screenshot 2022-05-10 at 14 59 33" src="https://user-images.githubusercontent.com/4352260/167635009-bee5c795-271c-49f9-a92c-840a415f120f.png">

</details>

---


