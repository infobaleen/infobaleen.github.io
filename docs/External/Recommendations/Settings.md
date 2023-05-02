## Recommendation Profiles

Here we explain the different settings fields that can be seen after clicking the cog wheel, as well as what data you find and can use.

<img width="1019" alt="Screenshot 2022-07-01 at 11 12 12" src="https://user-images.githubusercontent.com/4352260/176864507-439bac1e-4029-4aa3-800e-d4c14e8423e0.png">


<h4>Search</h4>
Items added in the search items window are counted as items given to the platform through the API call. This means they dont not affected by `boughtArticleGroup` but affects `basketArticleGroup`. 

<h4>Profile</h4>
Saved profiles
<br>

<h4>Refresh</h4>
<br>

<h4>Clear user and items</h4>
Removes selected items and user
<br>

<h4>Bench</h4>
Shows how fast the recommendation are returend when making an API call. (if your datamodel has MLFilter active for many fields the recommendations will be slower).
<br>

<h4>Add random item</h4>
Same as **search for items** but adds a random item.
<br>

<h4>Add random user</h4>
Selects a random user and shows what items this user has previously bought and the returned recommended items based on this. 
<br>

## Data available in recommendations

<h4>MlMeta</h4>
To show an image and name on your recomendations page you have to choose a format field in the data model edit mode, as well as an image field under items (also in the data model edit mode), and lastly activate the ml meta for these fields wanted.
<br>

<h4>MlFilter</h4>
To write filter expressions based on fields you have to activate ml filter for these fields, this is done in the edit mode of the data model.
</details>

</details>

## Filters And Customization Options

#### Search
Here you can search on all the items included in the machine learning (for example only items sold > X times). If you select an item you will see the recommendations provided by the platform for that specific product(s).


#### Columns

Columns are the data columns that can be used to create filters and rules. These are activated in the data model with the `MlFilter` toggle (MlFilter = Machine Learning Filter), see the image below. 

<img width="890" alt="Screenshot 2022-07-01 at 11 01 15" src="https://user-images.githubusercontent.com/4352260/176862636-6659b5fd-594f-4049-a349-45e774c39201.png">


### Filter expression
Here you can write an expression that creates a filter for your recommendation profile. Some example configurations:

#### Recommend products in a specific category
To recommend prodcuts in a specific category you can use something like `category = 'Kaffe & Te'`, or `price` > `100`

If the expression is `True` the product will be included in the recommendation, and it the expression is `False` the product will be filtered. In the case of `price` > `100`, the expression will return `True` for all products with a price larger than 100 thus removing all items with a price lower than 100 from the recommendations.

#### Recommend products with specific names or characters
To recommended products that does not contain either `HOOK`, `TAPE` nor `AA`, you can configure the filter according to: 
```
(contains(articleName, 'HOOK') OR contains(articleName, 'TAPE') OR contains(articleName, 'AA')) = false
```


### Boost expression
Each item has a "relevence rank" for each user, the products with the highest relevance rank are the products that get recommended. Uf you set a limit of 4 products the 4 products with the highest relevance rank are shown.  You can affect the relevance rank by applying a boost expression.   


Your boost expression is multiplied with the relevance rank. So if you for for example set boost expression: `2`, this means that you are multiplying all ranks with 2, thus not changing anything in the relative order for recommendations since all ranks are multiplied.  

If you instead create the boost expression: `1+1.0*(product_group = 'bags')`, all ranks are multiplied by `1` but products in the product_group `bags` are multiplied by `2` thus increasing their rank relative to other products by 100%. 

if you change the expression to: `1+0.5*(product_group = 'bags')` the rank for bags relative to other products are increased by 50%  


### InteractionFilter
This allows you to filter on purchase history, for example if you send in a user who has bought 2 items, and you have a filter removing 1 of the item types, the products returned will be based only on the item not filtered out.


### Trend
Trend limits the time interval for the data that the recomendations are based on. `Max trend` uses a short time interval resulting in the machine-learning model only recommending products that are trending last few weeks.


### Limit
Limit decides how many recomended items are returned. For example, Limit 4 = Four recommended items. Limit 12 = 12 recommended items.

### Max orders
Number of orders that are taken into concideration when recommending products. `Max orders = 1` means only the items included in the latest order are used as purchase history for that user. `Max orders = 2` means the items in the two latest orders are taken into account.

To see what the orders included contains, the items excluded from the customers purchase history are marked with a red dot, as seen below:
![image](https://user-images.githubusercontent.com/103515314/235160364-6a05deb5-3b17-4a57-ab36-d70014ab13dc.png){: style width="400px"}


### Max interactions
Number of items that are taken into concideration when recommending products. `Max items = 1` means only the latest purchased item is used as purchase history for that user. `Max items = 2` means the two latest items are taken into account.</details>

### Allow items from history
Sets a filter so that all items the user have bought cannot be recommended. 


### Shuffled
If Limit is set to 10 the items are recomended in order (most likly next purchase is at the top).  
by enabling `shuffled` it still recommends the top 10 items but the order of the top 10 items are shuffled. </details>


### Advanced
Create an advanced filter. 

* Name: is the variable name.
* Field: the field wich you are taking data from
* Option: "all" means all items in the users purchase history. "items" means all items sent in through the API by the customer. When the customer makes an API call for the recommendation they can include items in the API call. for example items in the basket, the item you are currently looking at etc.

See some example advanced filters below:
#### Example 1: Rotation parameter recommendations</summary>

| Parameter | Description |
| --- | --- | 
| RotateLength (float 0-1) | RotateLength bestämmer hur stor andel av alla kandidater vi tillåter rekommenderas, så 0.9 => 90% av produkterna. |
| RotateSeed (int) | Med RotateSeed > 0 slumpas ordningen av kandidaterna. En och samma seed ger en viss ordning och är unikt per användare. Vi kommer alltså inte ignorera samma 50% av produktutbudet vid RotateLength=0.5 för alla användare. Ex `"RotateSeed":"now()"`|
| RotateOffset (float 0-1): | Anger från vilken andel av kandidaterna vi börjar göra urvalet. RotateOffset tillsammans med RotateLength skapar möjlighet att “paginera” urvalet. Man kan ex skapa 4 separata set av slumpade produkter som man roterar på genom att använda RotateLength:0.25 och anropa APIi:t med RotateOffset: 0, 0.25, 0.5, 0.75.|


#### Example 2: Advanced query

```
{"Context":[{"Name":"bought_phone_model","Field":"phone_model","Option":"all"}]}
```
*Filter expression:*
```
hasAny(split(bought_phone_model,","),makeArray(phone_model))
```
`split(bought_phone_model,",")` returns an array of your purchase history `("Field":"phone_model"): ['bought_phone_model_1','bought_phone_model_2','bought_phone_model_3','bought_phone_model_4']`

`makeArray(phone_model)` returns an array of all `phone_model`: `['phone_model_1','phone_model_2','phone_model_3','phone_model_n']`

`hasAny` checks if elements in `array 1` is contained in `array 2`  

in this case the customers purchase history includes `iPhone 12/Pro MagSafe` and `iPhone 12/Pro`
The expression `hasAny(split(bought_phone_model,","),makeArray(phone_model))` will thus return `true` for all pruducts where `phone_model` = `iPhone 12/Pro MagSafe` or `iPhone 12/Pro` and `false` for all other products. Thus only products with the same `phone_model` will be recommended.

If you change the expression to `hasAny(split(bought_phone_model,","),makeArray(phone_model)) = FALSE` everything will be inverted thus only recomending products where the `phone_model` **!=** `iPhone 12/Pro MagSafe` or `iPhone 12/Pro`.

![image](https://user-images.githubusercontent.com/102239423/171135517-3d3eaeeb-7785-460e-a242-2a6e3cfaceb4.png)
![image](https://user-images.githubusercontent.com/102239423/171135706-fcc4ad7f-7066-441a-8e4d-c4162cacebec.png)

[NOTE! when adding an item to in the `Search for items` you **DO NOT** add this item to your purchase history, these items are sent in from the API meaning they will only be affected by a filter expression if you use the option `item` instead of `all`]  

See example:
![image](https://user-images.githubusercontent.com/102239423/171145795-877fb7b8-6e02-4bf0-857b-985deafe6efd.png)



---


#### Add field limit 
Field limit lets you set a filter on how many of each category should be recommended. This is usually used on product category where you only want to include ex. max 2 of each product category.


---


## Other Actions

#### Save as new profile
Saves the current configuration as a profile new

---


#### Save profile
Overrides the current profile with the current configuration.

---


#### Delete profile
Delets selected profile.
