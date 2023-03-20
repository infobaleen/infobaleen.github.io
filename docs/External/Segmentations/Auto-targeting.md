# Auto-targeting
Auto-targeting helps save time while at the same time finding optimal groups of customers to target with what items. In this part we will first shortly go over the process, and then dive deeper into different settings and adjustments you can make.

1. We start with `User Settings` for the user segment and an example of only including customers that has a previous purchase of some sort.
2. Creating two `Advertisements` where we let our AI choose the most appropriate products for our targeted segment
3. `Enabling the AI` to divide the user segment into the most accurate segments for increased potential
Auto-targeting identifies optimal combinations of items and users that helps increase conversion in campaigns through machine learning. 
4. Evaluating and `Exporting` the segments.


<details class="optional-class"><summary>Why use auto-targeting?</summary>
<p>

You can use Sift Labs auto-targering AI to answer the below questions:  
<ul>
  <li>What products should I use in my targeted campaign to a specific customer group?</li>
</ul>

Sift Labs AI ranks the products based on what products are most likely to trigger a purchase given the selected group of customers.

<ul>
  <li>Which customers should I send a campaign with specific products to?</li>
</ul>

Sift Labs AI ranks the users based on who are most probable to make a purchase given the products in your campaign. 
Using this information you can avoid sending email to customers that would consider it spam by only selecting customers that show the highest affinity to the product you want to promote.


</p></details>




## Step-by-step tutorial to create an AI-based auto-targeting campaign
---

### Step 1: Create auto-targeting campaign

1. Choose the **Segmentations** tab
2. Create a new auto-targeting campaign by clicking the + icon in the upper right corner
3. Choose a segment name and select **Auto-targeting** under Segment Type.    
![image](https://user-images.githubusercontent.com/102239423/204833365-0717d94e-5693-4dad-89e7-1e0783da967f.png)

---

### Step 2: Choose recipients (`User Settings`)
After the campaign has been created, now it's time to set the recipients (audience) for the campaign. If you do not add a filter you are targeting your whole user base, as you can see in the example below 520,954 (out of 520,954). If you want to select a specific customer group you can add a filter by pressing the 
![image](https://user-images.githubusercontent.com/102239423/205064839-2c46f643-64e7-4767-b84a-4e54c809ae47.png) **icon** (Add filter group) under **User Settings** (see image below) to create a filter group. 
![image](https://user-images.githubusercontent.com/103515314/206199028-2af76fdd-fd30-44b7-a619-40dc93ec46dc.png)

From the **add filter group** you can chose between **item**, **interaction** and **user** filter.

- The `user filter` lets you filter your userbase based on user metadata such as age, gender, country, region, etc. 

- The `interaction filter` lets you filter your userbase on interaction metadata such as order_id, sales price, discount, tax, store, freight etc. (This means users that has made an interaction at a particular store or discount...)

- The `item filter` lets you filter your userbase on item metadata such as product name, product category, color, size, COGS, etc. (This means users that has purchased an item in a particular color, size, category...)

After adding a filter group you can now select the metadata you want to use. Press the 
![image](https://user-images.githubusercontent.com/102239423/205067080-53e29d68-08bf-4562-acb1-bf61c3b5239d.png) 
**icon** which opens a drop down where you can select the field you want use to create your filter. In the below example we select the field **region**.

![image](https://user-images.githubusercontent.com/102239423/205066679-89a8038b-bd48-4331-9ed3-c80b5712471a.png)
From here you can slice your userbase to only include customers that live for example in Stockholm and Skåne

![image](https://user-images.githubusercontent.com/102239423/205075739-06b4e533-9538-44c7-b710-fb9046f6a8e5.png)

You can add a additional filter groups, 
in the example below we add an additional **item filter**  to only include users that have made a purchase in the category **Hudvård**

![image](https://user-images.githubusercontent.com/102239423/205079344-6eed2b66-39c5-4622-8be0-5d87ff62c161.png)

From these two filter we have sliced our customer base down to 101,168 (out of 520,954) customers.

---

### Step 3: Choose auto-targeting settings (`Auto-targeting Settings`)
These settings allow you to decide how you want to approach the auto-targeting. 

The `tick box` lets you choose if you want to block users from being included in an advertisement including products they already bought.

The `Trend slide` has to do with how much weight trending products should gain, for example if you choose a high trend value, then seasonal trends in sales will have higher weight (e.g. during Christmas more Santa Claus-products are probably sold)

![image](https://user-images.githubusercontent.com/102239423/205098283-6adcf884-7437-49cd-9366-d244d9c02e53.png)

---

### Step 4: Create an `Advertisement` 

To create an advertisement click the ![image](https://user-images.githubusercontent.com/102239423/205064839-2c46f643-64e7-4767-b84a-4e54c809ae47.png) **icon** on the left side below the **User Settings** card section. 

For each advertisement you choose to create, you can use different filters. The filters on each advertisement is unique for that advertisement and allows you to target a sub-segments within the segment you got after step 2, `User Settings` for each different advertisement. 

You can now choose between letting the AI choose products depending on the segments chosen, or add a specific item wanted for whatever reason. A combination of both alternatives is also recommended. The buttons for doing this is `ADD ITEM` + `ADD AUTO ITEM` according to picture below.

![image](https://user-images.githubusercontent.com/103515314/206189430-0874b76a-f2e3-4e17-aa80-07137785da5f.png)

When you have chosen or let the AI choose the product(s), selected wanted filters on users/items you're all set and can let our AI take over, press '`SAVE AND RUN`' 

### Step 5: Evaluating and exporting

The AI has now divided the segment into the best advertisements. You can see the distribution on the right side of the site, along with a graph showing the score distribution. 

The button `EXPORT USERS` allows you to export the users to another data source, or download a file containing the users for each segment.

You can also go back and readjust your advertisements by clicking the pencil on the top right picture below.

![image](https://user-images.githubusercontent.com/103515314/206197310-74b2fdc2-71eb-440b-ba61-889dc049b612.png)




---
## Below is further information about the Auto-targeting.

### Filter Settings
Below is a description of all the different buttons, toggles etc in the segmentation/auto-targeting on the platform.

### Disable Filter
By toggling <b>Enable filter</b> (see figure below) you can disable the whole filter group. This can be used to easier see the effect a filter has on the customer base.

<img width="846" alt="Screenshot 2022-06-28 at 14 41 45" src="https://user-images.githubusercontent.com/102239423/205082010-8a7a44b0-8649-4a2e-bec5-727cda9e35f8.png">


### Exclude
By toggling <b>Exclude</b> (see figure below) you invert the filter. In this example this means we are looking at customers that live in Stockholm or Skåne, that <b>HAS NOT</b> made a purchase in the category Hudvård

We can also chose to exclude on the <b>item</b> level instead of on the <b>interaction</b> level (see below). In this example this means we are looking att customers that live in Stockholm or Skåne that <b>HAS</b> made a purchase in any category <b>Except</b> in the category Hudvård.

<img width="846" alt="Screenshot 2022-06-28 at 14 41 45" src="https://user-images.githubusercontent.com/102239423/205082718-285808b5-fb9c-40dd-90ae-d26b9860119a.png">


### Match Any

By toggling <b>Match</b> Any** (see figure below) you change how the filtergroups interact from <b>AND</b> to <b>OR</b>. when <b>Match Any</b> is not active only the users that fill the criterias of <b>ALL</b> the filter groups are included.
By activating <b>Match Any</b> users that fill the criterias of <b>ANY</b> filter is included

<img width="846" alt="Screenshot 2022-06-28 at 14 41 45" src="https://user-images.githubusercontent.com/102239423/205088668-8a746db4-feda-4e8f-b84a-b61443ed52db.png">

### Filter options for category, number and timestamps

In the datamodel you can assign different roles to a field depending on how it should behave. 

A <b>category</b> behaves like a string (text) this means you can create a filter that include all fields that contains a certain text.

With a <b>Number</b> you can create filters that are larger or smaller than the field. 

With a <b>Timestamp</b> you can use the date format to filter on dates larger than ex. 2022-10-10.

<h4 id="category-options">Category options</h4>
<ul>
<li>Equals </li>
<li>Not equals</li>
<li>In</li>
<li>Not in</li>
<li>Starts with</li>
<li>Not starts with</li>
<li>Is empty</li>
<li>Is not empty</li>
<li>Contains</li>
</ul>
<h4 id="number-options">Number options</h4>
<ul>
<li>Equals</li>
<li>Not Equals</li>
<li>Less than</li>
<li>Greater than</li>
<li>Less than or equals</li>
<li>Greater than or equals</li>
<li>Between</li>
<li>Not between</li>
</ul>
<h4 id="timestamp-options">Timestamp options</h4>
<ul>
<li>Between</li>
<li>Not between</li>
<li>Equals</li>
<li>Not equals</li>
<li>Before</li>
<li>After</li>
</ul>






