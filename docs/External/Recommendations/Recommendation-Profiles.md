### On-site recommendations

<b>Bestseller Recommendations</b>

* Best Sellers and Trending Products, or simply "Top Lists," is a recommendation type that relies on comprehensive trend data and popularity metrics. It presents items that are currently deemed "hot and popular" in the store, reflecting the prevailing trends and customer preferences.
* Purpose: Push main trending products

<b>Bundled Recommendations</b>

* Dynamic Bundles serve as a method to curate sub-collections of items within Sift Lab that complement each other seamlessly. Common applications include presenting "Frequently Bought Together" or "Get the Look" inspirational content, which is then showcased through Onsite Product Recommendations.
*  Purpose: Display "shop the look", a pre-defined set of products that should be bought together

<b>Cherry-Pick Recommendations</b>

* Manual merchandising involves consistently showcasing specific products based on their product IDs and the predetermined order of those IDs. It's essential to ensure that the selected products are currently in stock, as the Cherry-Pick method for manual merchandising aligns with the availability status of the items.
* Hand pick products you would like to showcase

<b>Check-out recommendations</b>

* Recommend cheaper products based on what the customer has placed in their shopping cart
* Purpose: Increase AOV with a relevant product in the lower price segment
* Expression: tofloat(Price) < tofloat(last(basketArticlePrice))&times;0.8

<b>Color & Size affinity Recommendations</b>

* If the customer has a preferred size, color etc, Sift Lab can alter the recommendations shown to follow the chosen preference of the customer. Ensure to show i.e Size M for customers who are a size M and show Red items for customers who prefer color red. 
* Purpose: Align recommendations with the preferred choice of the customer
* What is needed: Return the picked color/size to Sift Lab in the API call 

<b>Cross-sell recommendations</b>

* This feature presents product recommendations associated with the specific product that the visitor is currently viewing, known as "Customers Who Viewed This Also Viewed." It incorporates cross-selling and up-selling functionalities with include and exclude rules, enabling the filtering of recommended products. These rules allow for precise control over the type of products displayed in the recommendations, offering the ability to tailor whether the recommendations showcase alternatives, supplementary items, or other specified product categories. 
* Purpose: Recommend products from other categories than what you're currently looking at

<b>Order Related Recommendations</b>

* Recommend the most likely products based on the customer's last order
* Purpose: Increase the number of customers who make another purchase

<b>Free Shipping Recommendations</b>

* The Free Shipping Recommendation is based on the total cart value. It allows for tailored suggestions based on the total value of items in the shopping cart, providing an incentive for customers to qualify for free shipping.
* Purpose: Improve AOV and make the customer reach free shipping limit
* Requirement: Return basket value and shipping limit in the API call.

<b>Inspiration recommendations</b>

* Recommend products in categories that the customer has not purchased from before / selected product
* Purpose: Inspire purchases in the most relevant categories that have not yet been purchased from / the product is not in

<b>Landing Page Recommendations</b>

* The Free Shipping Recommendation is based on the total cart value. It allows for tailored suggestions based on the total value of items in the shopping cart, providing an incentive for customers to qualify for free shipping.
* Purpose: Tailor the recommendations based on the external source of the customer
* Requirement: Return UTM-tag in the API call

<b>On sale recommendations</b>

* Recommend products that are on sale
* Purpose: Increase the sale percentage by showing relevant products on sale.

<b>Personalized Recommendations</b>

* The customer will be displayed with the products which whom is most likley to purchase. This is a default set-up in Sift Lab and optimized for revenue and transaciton. 
* Purpose: Go with a high-performing out of the box setup

<b>Random Products Recommendations</b>

* This functionality displays a completely random set of products. It can be used for testing or the live environment.

<b>Replenish Recommendations</b>

* You can exclude products to be shown during a set period of time to eliminate customers receiving unwanted products.
* Purpose: Occasionally bought products can be optimzed, i.e Toothpaste, Socks, Shampoo etc

<b>Similar products recommendation</b>

* Recommend products from the same category
* Purpose: High recognition factor

### Email recommendations

<b>Standard recommendation</b>

* Recommend the most likely next purchase (medium trend)
* Purpose: High likelihood of conversion

<b>Win-back recommendation</b>

* Recommend the most likely products a customer will purchase based on historical purchasing behavior
* Purpose: Present the products that a churned customer is most likely to buy

<b>Thanks for the last order recommendation</b>

* Recommend the most likely products based on the customer's last order
* Purpose: Increase the number of customers who make another purchase

<b>On sale recommendations</b>

* Recommend products that are on sale
* Purpose: Increase the sale percentage by showing relevant products on sale.

