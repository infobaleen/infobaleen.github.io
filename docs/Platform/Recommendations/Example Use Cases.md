## Example Recommendation Profiles

#### On-site

<details class="optional-class"><summary>Show examples of on-site profiles</summary>

---


Similar products recommendation: Similar
Recommend products from the same category
Purpose: High recognition factor

---


Inspiration recommendation: Inspiration
Recommend products in categories that the customer has not purchased from before / selected product
Purpose: Inspire purchases in the most relevant categories that have not yet been purchased from / the product is not in

---


Check-out recommendation: Check-out
Recommend cheaper products based on what the customer has placed in their shopping cart
Purpose: Increase AOV with a relevant product in the lower price segment
Expression: tofloat(Price) < tofloat(last(basketArticlePrice))*0.8

---


On sale recommendations: On sale
Recommend products that are on sale
Purpose: Increase the sale percentage by showing relevant products on sale.

</details>

#### E-mail profiles
<details class="optional-class"><summary>Show examples of e-mail profiles</summary>

---

Standard recommendation: Standard
Recommend the most likely next purchase (medium trend)
Purpose: High likelihood of conversion

---


Win-back recommendation: Win-back
Recommend the most likely products a customer will purchase based on historical purchasing behavior
Purpose: Present the products that a churned customer is most likely to buy

---


Thanks for the last order recommendation: Last purchase
Recommend the most likely products based on the customer's last order
Purpose: Increase the number of customers who make another purchase

---


On sale recommendations: On sale
Recommend products that are on sale
Purpose: Increase the sale percentage by showing relevant products on sale.

</details>

### Recommendations in emails
<details class="optional-class"><summary>Show more information about e-mail profiles</summary>

We can supply personalized recommendations in automated email flows. The technical integration varies between partners, but the main difference compared to segments is that we supply an individually customized set of products per user.

### Partners
Here we specify how the process works between us and specified partners

#### Voyado
Voyado has an ftp server to which we push a file of the form
```
ContactId,Skus,ExpiryDate
00000000-0000-0000-0000-000000000000,"Item692,Item165,Item835,Item166,Item836,Item838,Item277,Item504,Item332,Item218,Item608,Item528",9999-12-31T00:00:00.000+0000
0001394c-9e71-43d6-86f3-ada901fc4c10,"Item218,Item411,Item135,Item504,Item692,Item202,Item1035,Item835,Item412,Item277,Item610,Item515",9999-12-31T00:00:00.000+0000
00021b19-db3d-4d26-84ce-ad56g0f028e3,"Item165,Item702,Item701,Item146,Item166,Item835,Item1035,Item610,Item836,Item135,Item218,Item150",9999-12-31T00:00:00.000+0000
```
The list of `Skus` is generated from our recommendation engine for the user specified under `ContactId`, where the 0 line is the fallback recommendation.

-- Insert how to setup Voyado Export here --

Once the recommendation flow is set up and an initial export has been sent, the recommendations can be previewed in Voyado. This is done by us selecting a few contactIds from the platform for them to check. Then the customer triggers a support ticket by sending an email to support@revide.se (revide is the old name, this may be updated) with the contactIds and requests checking the preview.

**Note:** Historically there has been some issues due to contacts being labeled as "Contact" instead of "Member". This should be resolved as of April 2022, but to be safe, it could be a good idea to locate and include a user labeled "Contact" that has a purchase history. 
