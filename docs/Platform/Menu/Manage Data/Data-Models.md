## What is a datamodel? 
A datamodel is made up of of 3 tables (from the sources):

* Interaction table
* User table 
* Item table 

Each line in the interaction table is linked to a user and an item in the item and user table. When we have chosen what sources should be our interaction, item and user tables we can create a datamodel. After this we can start creating additional information through expressions. These can later be used in dashboards (dashboards are based upon a datamodel).
![image](https://user-images.githubusercontent.com/103515314/208437594-113fe10f-acbd-41c5-82ab-6a59e1272618.png)



When a datamodel is used for email analysis, the interaction becomes a specific `email sent to a user`, the user becomes `the one receiving the email`, and the email that was sent is treated as an item.

## Edit a data model
To edit and see the detailed info about a data model, you need to edit it. You can edit it by clicking the "pen" either after clicking the data model, or in the data-models list, see images below.

<img width="988" alt="Screenshot 2022-07-01 at 11 52 24" src="https://user-images.githubusercontent.com/4352260/176871921-4f7f72ce-e6de-453d-b24d-ad035c61e38b.png">
<details class="optional-class"><summary>Show another place to access the edit mode</summary>
<img width="782" alt="Screenshot 2022-07-01 at 11 52 33" src="https://user-images.githubusercontent.com/4352260/176872229-94b65f4b-35b1-447d-aa21-3c8eb40f66d6.png">

</details>

## Interaction Configuration
<details class="optional-class"><summary>Show more information</summary>

The interaction table specifies info about the interaction (a user interacting with an item) that includes a timestamp (ts). An interaction config can look something like below:

<img width="948" alt="Screenshot 2022-07-01 at 11 51 54" src="https://user-images.githubusercontent.com/4352260/176872296-06aea3bd-878a-499c-bc0e-8767dc6796a8.png">



#### Field
<details class="optional-class"><summary>Show more information</summary>

This is the name of the given in the source query (it can not be changed in the data model).  

</details>

#### Alias
<details class="optional-class"><summary>Show more information</summary>

By adding an alias the the field name is replaced by the alias name in the dashboard and segmentation. In Recommendation the field name is always shown even if an alias is added.
</details>


#### Role
<details class="optional-class"><summary>Show more information</summary>

| Name | Description |
| ----------- | ------------------------------------ |
| Categories | `Categories` is used when data is made up of multiple `category`'s. The data format for `categories` has to be [`category1`;`category2`;`category3`;`etc`]  |
| Revenue  | Revenue can only be set on 1 field and should be `sales price (EX VAT)`. The reason you set mark your `sales price (EX VAT)` with the revenue role is to generate suggested revenue related expressions. |
| Quantity | If a user buys multiple items of the same SKU at the same time this will be either represented as **1** interaction row with quantity `x` In this case that field should be set to `Quantity`. for some data souces this will be represented as `x` interaction rows without a quantity row. |
| Timestamp | The timestamp role should only be set to the field that represent the interaction timestamp (when the interaction took place). other timestamps such as `return date` etc. should instead be set to number. The timestamp role is needed to create suggested expressions.  |
| User | The User role is set to the key-field that connects the interaction table to the user table. |
| Item | The Item role is set to the key-field that connects the interaction table to the Item table. |
| Number | The Number role is automatically set to all fields that only contains numbers (you can make toFloat(`field`) without error). The number role lets you interact with a field as a number meaning you can make an calculation expressions such as if(`field` > 100). If you want to make a histogram you can only use fields with role **Number** because you specify the `bin width` wich can only be done if the field is concidered a Number (does not work if the field is a **Category**). |
| Category | All fields that can not be classified as a **Number** are classified as a **Category**. **Category**'s are used in for example [Bar charts](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Analytics/Dashboards.md "Open: Dashboards").  |
| Enum |  |
| EnumCategories | |
</details>

#### Active

The Active toggle button lets you activate/deactivate a field. a deactivated field can not be used in dashboards.

#### Info

Click on the small `i` button to see a preview of how the data looks/is formatted.

</details>

## Item Configuration
<details class="optional-class"><summary>Show more information</summary>

The item table specifies info about the items, i.e. the products.

<img width="976" alt="Screenshot 2022-07-01 at 11 58 21" src="https://user-images.githubusercontent.com/4352260/176872773-89453cc1-56eb-4175-88c1-e5aa6de16019.png">

### Fields
<details class="optional-class"><summary>Show more information</summary>
#### field
This is the name of the given in the source query (it can not be changed in the data model).  
</details>

#### Alias
<details class="optional-class"><summary>Show more information</summary>
By adding an alias the the field name is replaced by the alias name in the dashboard and segmentation. In Recommendation the field name is always shown even if an alias is added.
</details>

#### Role
<details class="optional-class"><summary>Show more information</summary>

| Name | Description |
| ----------- | ------------------------------------ |
| Categories | `Categories` is used when data is made up of multiple `category`'s. The data format for `categories` has to be [`category1`;`category2`;`category3`;`etc`]  |
| Timestamp | The timestamp lets you work with unixtimestamp and shows the result in as a datetime (readable format). |
| Format | The format role represent the name of the item and is what is shown in the [Image grid](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Analytics/Dashboards.md "Open: Dashboards") in the dashboards and in the [Recommendations](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Recommendations/Recommendation-profiles.md "Open: Recommendation profiles") |
| Image | The image role represent what field will be shown as a image in the [Image grid](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Analytics/Dashboards.md "Open: Dashboards") in the dashboards and in the [Recommendations](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Recommendations/Recommendation-profiles.md "Open: Recommendation profiles"). The image field is usually called something with `url`. |
| Number | The Number role is automatically set to all fields that only contains numbers (you can make toFloat(`field`) without error). The number role lets you interact with a field as a number meaning you can make an calculation expressions such as if(`field` > 100). If you want to make a histogram you can only use fields with role **Number** because you specify the `bin width` wich can only be done if the field is concidered a Number (does not work if the field is a **Category**). |
| Category | All fields that can not be classified as a **Number** are classified as a **Category**. **Category**'s are used in for example [Bar charts](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Analytics/Dashboards.md "Open: Dashboards").  |
| Enum |  |
| EnumCategories | |

</details>

#### MLMeta
<details class="optional-class"><summary>Show more information</summary>
The MLMeta toggle button controles what is returned when when you make an API call. This is to give you control what data you want to return to the customer. you dont want to activate MLMeta on all fields because this will result in you return alot of "trash columns" to the customer that they have to filter in turn get the relevant data. [Note that you also have to select the role `Image` and `Format` for the product to show]
(MLMeta is only relevant in the recomendations view)
</details>

#### MLFilter
<details class="optional-class"><summary>Show more information</summary>
The MLFilter lets you write expressions and filter your data in in the [Recommendations](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Recommendations/Recommendation-profiles.md "Open: Recommendation profiles"). You should only activate MLFilter for the fields you actually want to create a filter for, the reason for this is that when you activate **MLFilter** for a field this will store all data in the memory and every time the API calls for a recommendation the datamodel have to itterate through all fields with **MLFilter** resulting in a bad performance on the customers side (when the customer want to load our recomendations on their site the load speed will depend on how many **MLFilters** you have activated.  

<img width="892" alt="Screenshot 2022-06-10 at 08 16 47" src="https://user-images.githubusercontent.com/4352260/173002754-8885b8fa-1b5c-4dad-a74d-732f1d409eda.png">
</details>

#### Active
The Active toggle button lets you activate/deactivate a field. a deactivated field can not be used in dashboards.

#### Info
Click on the small `i` button to see a preview of how the data looks/is formatted.
</details>


## User config
<details class="optional-class"><summary>Show more information</summary>
The user table specifies info about the users, i.e. the customers. 

<img width="968" alt="Screenshot 2022-07-01 at 12 00 26" src="https://user-images.githubusercontent.com/4352260/176873224-8e8d99ba-3f06-48bf-80f7-3b289ab2b266.png">


### Fields


#### Field
<details class="optional-class"><summary>Show more information</summary>
This is the name of the given in the source query (it can not be changed in the data model).  
</details>

#### Alias
<details class="optional-class"><summary>Show more information</summary>
By adding an alias the the field name is replaced by the alias name in the dashboard and segmentation. In Recommendation the field name is always shown even if an alias is added.
</details>

#### Role
<details class="optional-class"><summary>Show more information</summary>

| Name | Description |
| ----------- | ------------------------------------ |
| Categories | `Categories` is used when data is made up of multiple `category`'s. The data format for `categories` has to be [`category1`;`category2`;`category3`;`etc`]  |
| Timestamp | The timestamp lets you work with unixtimestamp and shows the result in as a datetime (readable format). |
| Pll | |
| Email | |
| Number | The Number role is automatically set to all fields that only contains numbers (you can make toFloat(`field`) without error). The number role lets you interact with a field as a number meaning you can make an calculation expressions such as if(`field` > 100). If you want to make a histogram you can only use fields with role **Number** because you specify the `bin width` wich can only be done if the field is concidered a Number (does not work if the field is a **Category**). |
| Category | All fields that can not be classified as a **Number** are classified as a **Category**. **Category**'s are used in for example [Bar charts](https://github.com/infobaleen/customer-success/blob/main/Documentation/Platform/Analytics/Dashboards.md "Open: Dashboards").  |
| Enum |  |
| EnumCategories | |
</details>


#### Persona
<details class="optional-class"><summary>Show more information</summary>

The Persona toggle button controles what columns are used in the recommendations. For example, if we activate the field `gender` as a Persona, the recommendation engine will base the recommendations on what gender the user has. If we active the field `age` it will be used as a dimension in the recommendation, and so on.
</details>

**Note:** Use a maximum of 2 columns to define persona. Alternatively, make sure that the cardinality (number of groups) is less than 1000. (ex gender: 2 different and cities: 500 different, which means `2*500 = 1000` groups)

<img width="883" alt="Screenshot 2022-06-10 at 08 16 38" src="https://user-images.githubusercontent.com/4352260/173002716-64dd3abf-fc87-4b0d-942b-19b46b6e98b7.png">

</details>

## Custom properties
<details class="optional-class"><summary>Show more information</summary>
The Custom properties-section lets you define custom user group based on your data. The feature exploits the aggregated user data that can be found in the menu at `Model->Users`, see the image below.

<img src="../../../../images/Menu/custom_properties2.png" width="921"/>

Using for example `user.agg.first` and `user.agg.orders` as parameters `first` and `orders` it is possible to create, for example, a customer lyfecycle definition as in the image below.  

<img src="../../../../images/Menu/custom_properties.png" width="921"/>
</details>

## Expression syntax (Click house)
<details class="optional-class"><summary>Show more information</summary>

| Function | Description |
| ----------- | ------------------------------------ |
| `SUM()` | Summarize a value, for example SUM(returned_quantity) returns the total amount of returned quantity (over chosen period of time) |
| `uniq()` | counts the amount of unique values, for example uniq(user) returns the amount of unique users. |
| `uniqExact()` | Is almost the same as uniq(), however uniq() may have a very small inaccuracy (that most often doesn't matter at all), but if it's important to have for example 100.002 (correct) instead of 100.000, use uniqExact(). The reason for this is simply that uniq() is less demanding.|
| `countIf()` | this counts +1 for each time an argument is correct on an interaction (row). `Example`: let's say there's 10 interactions (ten rows) in a table with a column that's currency. On 7 of the 10 rows the currency column consists of 'SEK', if we now use countIf(currency = 'SEK') we will get the value 7. |
| `sumIf()` | sumIf(Value that will be summarized when, X = N)  `Example`: sumIf(revenue, currency = 'SEK') |
| `uniqIf()` | multiIf(boolean, result_1, boolean, result_2, ..., boolean, result_n, else_this) multiIf(name = 'red', colour, name = 'big', 'size', 'no data') |
</details>


# Data model expression examples 
Expressions can be used to calculate certain variables, for example the amount of returned items `(SUM(returned_quantity)` or divide certain users into different categories, for example dividing the customer base into customers with or without > 1 purchases. Expressions are made in the edit mode of a datamodel, and later can be found and used in dashboards as parameters and metrics. 

When writing expressions, remember to check and/or modify so that the variables like `revenue`, `ts` (timestamp), `quantity` is correct according to your data. returned quantity can for example be written in different ways (example: `returnedQuantity` / `returned_quantity`)  depending on data source. returnedQuantity, returned_quantity depending on the dataset.

### Interaction expressions
<details class="optional-class"><summary>Show more information</summary>

| Expression | Description |
| ----------- | ------------------------------------ |
| **Days since previous order cohort** | multiIf (agg.daysFromPrev <=30,'1.<30', agg.daysFromPrev <=60,'2.30-60', agg.daysFromPrev <=90,'3.60-90', agg.daysFromPrev <=180,'4.90-180', agg.daysFromPrev <=360,'5.180-360', agg.daysFromPrev <=720,'6. 360-720', agg.daysFromPrev <=4000,'7.>720', '8.New')|
| **Has return** | multiIf(returned_quantity > 0, 'Return', 'No return') |
| **First order (month**  | toStartOfMonth(user.agg.first) |
| **Active week**  | toMonday(ts) |
| **Active month**  | toStartOfMonth(ts) |
| **% discount**  | SUM(full_price-revenue)/SUM(full_price) |
| **Revenue**  | SUM(revenue) |
| **Price per item**  | SUM(revenue)/SUM(quantity) |
| **Revenue per user**  | SUM(revenue)/uniq(user) |
| **Average order value**  | SUM(revenue)/uniq(user,ts) |
| **Sold items**  | SUM(quantity) |
| **Items per order**  | SUM(quantity)/uniq(user,ts) |
| **% returned quantity**  | SUM(returned_quantity)/SUM(quantity)|
| **LTV 30d**  | We usually do 5 different LTV metrics, just remember to change name accordingly to selected amount of days. `sumIf(revenue, ts < user.agg.first + 30 AND addDays(user.agg.first, 30) <= now())/uniqIf(user,addDays(user.agg.first, 30) <= now())`, `sumIf(revenue, ts < user.agg.first + 60 AND addDays(user.agg.first, 60) <= now())/uniqIf(user,addDays(user.agg.first, 60) <= now())`, `sumIf(revenue, ts < user.agg.first + 90 AND addDays(user.agg.first, 90) <= now())/uniqIf(user,addDays(user.agg.first, 90) <= now())`, `sumIf(revenue, ts < user.agg.first + 180 AND addDays(user.agg.first, 180) <= now())/uniqIf(user,addDays(user.agg.first, 180) <= now())`, `sumIf(revenue, ts < user.agg.first + 365 AND addDays(user.agg.first, 365) <= now())/uniqIf(user,addDays(user.agg.first, 365) <= now())` | 
| **Returned quantity** | SUM(returned_quantity) |
| **Returned or not returned**  | multiIf(returned_quantity > 0, 'Return', 'No return') |
</details>

### Item expressions  
<details class="optional-class"><summary>Show more information</summary>

Sold items [item based dashboards] || `(item based dashboards here means that item is chosen as Role when creating the dashboard)`  
SUM(article_number.agg.trans)  

Available quantity [item based dashboards] || `(item based dashboards here means that item is chosen as Role when creating the dashboard)`  
SUM(item.in_stock)  

SUM(full_price-PriceExVatIncDiscSEK)/SUM(full_price)   
SUM(DiscountSEK) / SUM((DiscountSEK + PriceIncVatIncDiscSEK)  
</details>

### User expressions
<details class="optional-class"><summary>Show more information</summary>

 **Users > 1 order**  || uniqIf(user,user.agg.orders>1)/uniq(user) |
</details>