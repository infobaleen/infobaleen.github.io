# Recommendations - API Documentation

## Authorization

Requests are authenticated and authorized with API Keys. API keys can be managed from the application menu _Account /
Api keys_. When sending a request, the API key is provided using the _Authorization_ header.

## Recommendations

Item recommendations from a data model are provided by the API in two ways, given a user (/user-to-items) or from a list
of items (/items-to-items).

### User recommendations (user-to-items)

__User-to-items__ recommendations can be used to generate content for user landing pages, email marketing and similar.
Given a user id, a list of recommended items is returned.

``` POST /api/v1/data-models/<id>/recommendations/user-to-items ```

__Request parameters__ (JSON body)

#### Input parameters

| Parameter                  | Type              | Description                                                                                                                                                                                          |
|----------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| User                       | string            | User id to fetch item recommendations for                                                                                                                                                            |
| Items                      | array of strings  | Item IDs to build the recommendations from                                                                                                                                                           |
| MinInteractionTs           | int               | Min timestamp for interactions to base the recommendations on                                                                                                                                        |
| MaxInteractions            | int               | Pick orders until `MaxInteractions` interactions are included                                                                                                                                        |
| MaxOrders                  | int               | Pick orders until `MaxOrders` orders are included                                                                                                                                                    |
| InteractionFilter          | SQL               | To select from history based on SQL query                                                                                                                                                            |
| Persona                    | Object            | `{"gender": "Female", "country_code": "SE"}`                                                                                                                                                         |

#### Logical parameters

| Parameter                  | Type              | Description                                                                                                                                                                                          |
|----------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TrendFactor                | float             | Value between 0 and 1. 0 is used to base recommendations on similarity only, and 1 weights the recommendations on the current trend/popularity. Default is 1.                                        | 
| Recurring                  | boolean           | Allow recommending items already consumed by the user. Default is false.                                                                                                                             |
| AllowedItems               | array of item ids | Only items in `AllowedItems` is returned in the response                                                                                                                                             |
| ForcedItems                | array of item ids | All items in `ForcedItems` is returned in the response                                                                                                                                               | 
| BlockedItems               | array of item ids | No items in the `BlockedItems` is returned in the response                                                                                                                                           |
| Candidates                 | int               | number of items to consider. Default to all available items. Can be used for faster calculations.                                                                                                    |
| ItemFilterExpression       | SQL               | `"price>100"`                                                                                                                                                                                        |
| ItemBoostExpression        | SQL               | `"toFloat(margin)"`                                                                                                                                                                                  |
| Search                     | string            | Experimental Full-text-search. Filter and boost based on search string.                                                                                                                              | 
| FieldLimits                | array of objects  | Ex: `[{"Field":"name", "Limit": 2}]` makes sure to not return more than 2 items of the same color.                                                                                                   |
| Context                    | See example       | `[{"Name":"ageLimit", "FloatValue":11},{"Name": "genres", "ArrayValues": "action,thriller"}, {"Name": "gender", "StringValue": "female"},{"Name": "ages", "Field": "AgeLimitSv", "Option": "last"}]` | 

#### Output parameters

| Parameter                  | Type             | Description                                                           |
|:---------------------------|------------------|-----------------------------------------------------------------------|
| Shuffled                   | bool             | shuffle recommendations                                               |
| StrictAfterFieldLimitCheck | bool             | Return error if we can not find `Limit` valid items after FieldLimits |
| BestEffort                 | bool             | Return all valid items even if it is less than `Limit`                |
| Format                     | string           | Response format/encoding, available options: `json`, `og`             |
| Columns                    | array of strings | Meta data columns to include in the response                          |
| Limit                      | integer          | Maximum number of items returned, default=0                           |
| Offset                     | integer          | Items to skip                                                         |

__cURL__ example

```
curl -X POST ${IB_API_URL}/api/v1/data-models/<id>/recommendations/user-to-items \
-H "Authorization: ${IB_API_KEY}" \
-d '{"User": "123", "Limit": 10, "Recurring": false}'
```

__Response__
The response contains the top recommended items ordered according to the relevance score. The item object contains `Id`
and all meta-data fields that is specified in the data-model configuration.

```
[
    {"Id":"7942856970334767135", ...},
    {"Id":"9136495236170061780", ...},
    ...
]
```
