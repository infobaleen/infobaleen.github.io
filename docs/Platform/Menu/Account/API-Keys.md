# API Keys
API keys are primarily used for accessing the recommendation API to fetch product recommendations to your website or your email campaigns. 

#" Test your API request
* Create a new API key
* Open ubuntu
* Copy from your  API key 
```
  curl 'https://`PLATFORM`.infobaleen.com/api/v1/api-profiles/`473`/recommendations/user-to-items' -d '{"Limit":3,"User":"`X`"}' -H 'Authorization: `KEY`'
```

* Use **Rex** in the user table under Model > Users and replace X in the curl to verify you get the same results as the recommendations for that user

**NOTE:** If you try to use the curl command in Windows it will not work note the difference from the curl above with `\` and `.exe` 
```
curl`.exe` 'https://PLATFORM.infobaleen.com/api/v1/api-profiles/473/recommendations/user-to-items' -d '{`\`"Limit`\`":3,`\`"User`\`":`\`"X`\`"}' -H 'Authorization: KEY'
```

 
