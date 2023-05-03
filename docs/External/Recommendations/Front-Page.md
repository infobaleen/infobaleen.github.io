## Front page

#### Search for items
Items added in the search items window are counted as items given to the platform through the API call. This means they dont not affected by `boughtArticleGroup` but affects `basketArticleGroup`. 


#### Profile
Here you choose what profile to view and edit, all your previous profiles as well as their `id` is shown here. 


#### Refresh
The refresh button simply runs the API call again which would give you different results if you have randomness included in your profile


#### Clear user and items
Removes selected items and user


#### Bench
Shows how fast the recommendation are returend when making an API call. (if your datamodel has MLFilter active for many fields the recommendations will be slower).


#### Add random item
Same as **search for items** but adds a random item.


#### Add random user
Selects a random user and shows what items this user has previously bought and the returned recommended items based on this. 


#### Recommendation output
The output is what the API returns to the customer. All fields active in the **Columns** section are returnerd. 
![image](https://user-images.githubusercontent.com/102239423/235849549-535e76ad-1eba-472c-a95b-aa96ae3ca0f5.png)
You can toggle between table and grid view 
![image](https://user-images.githubusercontent.com/102239423/235849957-64e568c2-7272-4b49-88b5-7d98e15e424c.png)
![image](https://user-images.githubusercontent.com/102239423/235850047-70108258-7c6d-42c1-a06b-3b63d8e422b6.png)

You can click on **Show rank and score** to show what rank the recommended products have (1 is the best). and also the machine learning score for that product. In the purchase history you can see at what date that purchase was made


