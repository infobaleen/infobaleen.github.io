# Table of Contents
1. [How to create an API key and URL to fetch product recommendations](#how-to-create-an-api-key-and-url-to-fetch-product-recommendations)
1. [Steps to integrate with Rule](#steps-to-integrate-with-rule)
1. [Integrate with Rule](#integrate-with-rule)
    1. [What’s needed](#what’s-needed)
        1. [Export segments](#export-segments)
        1. [Personalized product recommendations](#personalized-product-recommendations)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# How to create an API key and URL to fetch product recommendations

**Note!** The key is only visible for 1 hour after creation. 

1. Go to the three dots on the top right corner of the screen and select "API keys"
2. Create a API key by pressing the purple plus sign on the right side
3. Name your API key and select `ItemToItems`, `UserToItems`, and `ItemData`
4. Press "Save"
5. Copy the API key
6. Use Bitwarden to send the API key to the customer email. Remember to remove the password protection
7. After the API key has been sent, email the customer the URL

**christian note:** _We need to standardize how we communicate the tokens. Email is NOT a secure medium. If possible, let the customer setup the API keys in the platform.
Bitwarden can be used with PASSWORD protection._ 

[*Back to top*](#table-of-contents)

# Steps to integrate with Rule
1. Under **data model** > **User config** the field `email` must be set to the role `Email`
![image](https://user-images.githubusercontent.com/102239423/171419337-eb122526-59b4-4344-9613-542fa24f8a1e.png)

2. edit the item source used in the data model and add where `< >` means inputs you need to edit.

```
concat('https://myplatform.infobaleen.com/token/<RULE_API_KEY>/api/v1/data-models/<ID>/item-data?format=og&id=', items.id) og_url,  
 ```
![image](https://user-images.githubusercontent.com/102239423/171423278-18d58beb-2084-4db7-b02a-61762dcd192c.png)

3. go to the data model and activate `Active` and `MlMeta` for `og_url`
![image](https://user-images.githubusercontent.com/102239423/171424929-50b87293-dd85-4619-8145-440e3b951f6d.png)

[*Back to top*](#table-of-contents)

# Integrate with Rule
Take your marketing efforts in Rule to a new level by combining our powerful features of segmentation and personalization with your Rule account. Export segments from your Infobaleen platform directly to Rule as tags and target them in your marketing. Use personalized product recommendations directly in your emails meaning personalized content for each and every recipient.

Here is a summary of how to enable our recommendations and segmentation in Rule.

[*Back to top*](#table-of-contents)

## What’s needed
The two features requires different actions

[*Back to top*](#table-of-contents)

### Export segments
1. Provide us with an **API key** from your Rule account. The key is generated under Settings /  Developer in the Rule platform. 
2. The user identifier used in Rule must be present as user meta data in the Infobaleen platform. The standard identifier in Rule is **email**. Provide us with information if you use a custom identifier.

Once in place, you have a new export target available, “rule”, when exporting a segment from your platform. Exported segments will appear as **tags** in Rule where you can target them with relevant content. 

You will also have the ability to **filter users on unsubscribe status from Rule** when creating segments in your Infobaleen platform. These are the available fields.They have either the value 1 (unsubscribed) or 0 (not unsubscribed).

* rule_email_campaign_unsub
* rule_email_transactional_unsub
* rule_sms_campaign_unsub
* rule_sms_transactional_unsub

[*Back to top*](#table-of-contents)

### Personalized product recommendations
1. **Make sure your user data in Rule includes the user identifier used in Infobaleen**. If not already present, make sure to include it in your exports to Rule. Rule will use this id to fetch recommendations from the Infobaleen platform.
2. Select what product meta data Rule will have access to. Rule uses OG-tags present on web pages as product data for recommendations. Either we supply OG-tags from product pages on your website or from your product meta data in the Infobaleen platform. Provide us with the option you prefer.
    * **Option 1: Use product pages from your site**. Requires **product URLs** to be present in the Infobaleen platform. This has the benefit of you having greater control over  what product data is available in Rule, ex easier to add new product meta data if needed, and the data Rule uses will always be up to date. Else, as data is synchronized once a day in the Infobaleen platform, there will be a delay between a change on your side and the data being updated in the Infobaleen platform and   what's available to Rule.   
    * **Option 2: Use product meta data available in the Infobaleen platform**. Contact us and we will configure your platform.
3. **Create an API profile** in your Infobaleen platform. This will allow you to configure the recommendations used by Rule directly from the platform. 
4. **Create an API key** in your Infobaleen platform with access to the api-profile created in the previous step. This is done under the settings menu / Account / API Keys.
5. Contact Rule for **a custom email template** that uses personalized recommendations, and provide them with a link to the profile with recommendations from your platform in the form: https://myplatform.infobaleen.com/token/<RULE_API_KEY>/api/v1/api-profiles/{ID}/recommendations/user-to-items?User={USERID}&Limit={LIMIT}
Note, USERID and LIMIT are variables that Rule will replace. RULE_API_KEY are from the previous step.

Once all is in place, you can send personalized emails that are dynamically populated with configurable product recommendations from Infobaleen at sending time.

Having multiple templates for personalized recommendations can be a step to take it even further. Create multiple profiles with specific business rules and have Rule create a template for each. Add categorized blocks with personalized recommendations in your content where you filter recommendations on specific category data. As an example one block with “Your recommendations in travel” and another with “Your recommendations from our latest products”. Note that all profiles can use the same API key.

[*Back to top*](#table-of-contents)
