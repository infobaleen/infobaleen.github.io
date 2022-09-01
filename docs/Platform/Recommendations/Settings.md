## Settings

Here we explain the different settings fields that can be seen after clicing the cog wheel.

<img width="1019" alt="Screenshot 2022-07-01 at 11 12 12" src="https://user-images.githubusercontent.com/4352260/176864507-439bac1e-4029-4aa3-800e-d4c14e8423e0.png">


### Search


### Columns

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


### InteractionFilter


### Trend
Trend limits the time interval for the data that the recomendations are based on. `Max trend` uses a short time interval resulting in the machine-learning model only recommending products that are trending last few weeks.

### Limit
Limit decides how many recomended items are returned. For example, Limit 4 = Four recommended items. Limit 12 = 12 recommended items.

### Max orders
Number of orders that are taken into concideration when recommending products. `Max orders = 1` means only the items included in the latest order are used as purchase history for that user. `Max orders = 2` means the items in the two latest orders are taken into account.

### Max interactions
Number of items that are taken into concideration when recommending products. `Max items = 1` means only the latest purchased item is used as purchase history for that user. `Max items = 2` means the two latest items are taken into account.

### Allow items from history
Sets a filter so that all items the user have bought cannot be recommended. 

### Shuffled
If Limit is set to 10 the items are recomended in order (most likly next purchase is at the top).  
by enabling `shuffled` it still recommends the top 10 items but the order of the top 10 items are shuffled. 


### Advanced
Create an advanced filter. 

* Name: is the variable name.
* Field: the field wich you are taking data from
* Option: "all" means all items in the users purchase history. "items" means all items sent in through the API by the customer. When the customer makes an API call for the recommendation they can include items in the API call. for example items in the basket, the item you are currently looking at etc.

See some example advanced filters below:

#### Rotation parameters recommendations
| Parameter | Description |
| --- | --- | 
| RotateLength (float 0-1) | RotateLength bestämmer hur stor andel av alla kandidater vi tillåter rekommenderas, så 0.9 => 90% av produkterna. |
| RotateSeed (int) | Med RotateSeed > 0 slumpas ordningen av kandidaterna. En och samma seed ger en viss ordning och är unikt per användare. Vi kommer alltså inte ignorera samma 50% av produktutbudet vid RotateLength=0.5 för alla användare. Ex `"RotateSeed":"now()"`|
| RotateOffset (float 0-1): | Anger från vilken andel av kandidaterna vi börjar göra urvalet. RotateOffset tillsammans med RotateLength skapar möjlighet att “paginera” urvalet. Man kan ex skapa 4 separata set av slumpade produkter som man roterar på genom att använda RotateLength:0.25 och anropa APIi:t med RotateOffset: 0, 0.25, 0.5, 0.75.|

Man bör komma ihåg att inte använda för små set om man vet att man har få produkter att röra sig med i profilen, ex om man har många filter. Det kan sluta med att vi inte kan uppfylla den Limit man vill ha.

#### Example of advanced quey
```
{"Context":[{"Name":"bought_phone_model","Field":"phone_model","Option":"all"}]}
```
*Filter expression:*
```
hasAny(split(bought_phone_model,","),makeArray(phone_model))
```
`split(bought_phone_model,",")` returns an array of your purchase history `("Field":"phone_model"): ['bought_phone_model_1','bought_phone_model_2','bought_phone_model_3','bought_phone_model_4']`

`makeArray(phone_model)` returns an array of all `phone_model`: ['phone_model_1','phone_model_2','phone_model_3','phone_model_n']  

`hasAny` checks if elements in `array 1` is contained in `array 2`  

in this case the customers purchase history includes `iPhone 12/Pro MagSafe` and `iPhone 12/Pro`
The expression `hasAny(split(bought_phone_model,","),makeArray(phone_model))` will thus return `true` for all pruducts where `phone_model` = `iPhone 12/Pro MagSafe` or `iPhone 12/Pro` and `false` for all other products. Thus only products with the same `phone_model` will be recommended.

If you change the expression to `hasAny(split(bought_phone_model,","),makeArray(phone_model)) = FALSE` everything will be inverted thus only recomending products where the `phone_model` **!=** `iPhone 12/Pro MagSafe` or `iPhone 12/Pro`.

![image](https://user-images.githubusercontent.com/102239423/171135517-3d3eaeeb-7785-460e-a242-2a6e3cfaceb4.png)
![image](https://user-images.githubusercontent.com/102239423/171135706-fcc4ad7f-7066-441a-8e4d-c4162cacebec.png)

[NOTE! when adding an item to in the `Search for items` you **DO NOT** add this item to your purchase history, these items are sent in from the API meaning they will only be affected by a filter expression if you use the option `item` instead of `all`]  

See example:
![image](https://user-images.githubusercontent.com/102239423/171145795-877fb7b8-6e02-4bf0-857b-985deafe6efd.png)


### Add field limit 
Field limit lets you set a filter on how many of each category should be recommended. This is usually used on product category where you only want to include ex. max 2 of each product category.

### Save as new profile
Saves the current configuration as a profile new

### Save profile
Overrides the current profile with the current configuration.

### Delete profile
Delets selected profile.
