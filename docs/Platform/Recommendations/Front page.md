## Front page

#### Search for items
Items added in the search items window are counted as items given to the platform through the API call. This means they dont not affected by `boughtArticleGroup` but affects `basketArticleGroup`. 

---

#### Profile
Here you choose what profile to view and edit, all your previous profiles as well as their `id` is shown here. 

---

#### Refresh
The refresh button simply refreshes the

---

#### Clear user and items
Removes selected items and user

---

#### Bench
Shows how fast the recommendation are returend when making an API call. (if your datamodel has MLFilter active for many fields the recommendations will be slower).

---

#### Add random item
Same as **search for items** but adds a random item.

---

#### Add random user
Selects a random user and shows what items this user has previously bought and the returned recommended items based on this. 

---

#### Recommendation output
The output is what the API returns to the customer. All fields active in the **Columns** section are returnerd. if the `image` is active the output will only show the image and format. by disabling the image you can see all other fields that are returned.  
With image active:
![image](https://user-images.githubusercontent.com/102239423/170311295-0a3f1097-cc4f-4829-a4fb-8962b3b5d5e7.png)
With image inactive:
![image](https://user-images.githubusercontent.com/102239423/170311416-cd596ff0-02d8-44b8-91d9-483ddcccb075.png)