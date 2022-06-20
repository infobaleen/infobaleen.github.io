# Table of Contents
1. [Data Models](#data-models)
    1. [Data model expressions (Click house)](#data-model-expressions-click-house)
1. [Sources](#sources)
    1. [Centra Queries](#centra-queries)
        1. [Procedure](#procedure)
        1. [Interactions  ](#interactions)
        1. [Items](#items)
        1. [Users](#users)
        1. [Variant model ](#variant-model)
            1. [Interactions ](#interactions)
                1. [Id columns ](#id-columns)
            1. [Items](#items)
                1. [Id columns ](#id-columns)
            1. [Users](#users)
                1. [Id columns ](#id-columns)
        1. [No size model ](#no-size-model)
        1. [Example rows with explanation](#example-rows-with-explanation)
    1. [Voyado Queries](#voyado-queries)
        1. [Procedure](#procedure)
        1. [Interactions](#interactions)
                1. [Id columns ](#id-columns)
        1. [Stores](#stores)
                1. [Id column](#id-column)
        1. [Contacts](#contacts)
                1. [Id column](#id-column)
    1. [Query expressions](#query-expressions)
1. [Results](#results)
    1. [dummy1](#dummy1)
    1. [dummy2](#dummy2)
1. [Import Files](#import-files)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Data Models

[*Back to top*](#table-of-contents)

## Data model expressions (Click house)
`SUM()` Summarize a value, for example SUM(returned_quantity) returns the total amount of returned quantity (over chosen period of time) 

`uniq()` counts the amount of unique values, for example uniq(user) returns the amount of unique users.  

`uniqExact()` Is almost the same as uniq(), however uniq() may have a very small inaccuracy (that most often doesn't matter at all), but if it's important to have for example 100.002 (correct) instead of 100.000, use uniqExact(). The reason for this is simply that uniq() is less demanding.

`countIf()` this counts +1 for each time an argument is correct on an interaction (row). `Example`: let's say there's 10 interactions (ten rows) in a table with a column that's currency. On 7 of the 10 rows the currency column consists of 'SEK', if we now use countIf(currency = 'SEK') we will get the value 7.  

`sumIf()`  
sumIf(Value that will be summarized when, X = N)  `Example`: sumIf(revenue, currency = 'SEK')  

`uniqIf()`

multiIf(boolean, result_1, boolean, result_2, ..., boolean, result_n, else_this)  
multiIf(name = 'red', colour, name = 'big', 'size', 'no data')

etc...

[*Back to top*](#table-of-contents)

# Sources
If you are looking for information about how sources gets set up, how they work and what they are, click [here](https://github.com/infobaleen/customer-success/blob/main/Documentation/Internal%20procedures/Workflows/Platform-setup-(import-files,-sources-and-datamodel).md#2-create-sources)  

[*Back to top*](#table-of-contents)

## Centra Queries
_____________________________________________________________________________________________________________________
Procedure	1

Interactions	1

Items	2

Users	3

_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### Procedure
Setup config
Make arbitrary query toward centra
This will trigger proxy sync, the .gz files will appear once completed, duration 1-5h
_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### Interactions  
Id columns: id i import / user,id i model source

```
SELECT  
  `line.Id` AS id,
  `order.Customer.Id` AS user,
  unixTimestamp(`order.OrderDate`, '2006-01-02T15:04:05-0700') AS ts,  
  concat(`line.ProductVariant.Id`,'_',`line.ProductSize.Size.Id`) AS item,  
  toFloat(`line.LineValue.FormattedValue`)*toFloat(`order.CurrencyBaseRate`) AS revenue,  
  round(`line.Quantity`*`order.CurrencyBaseRate`*`line.UnitOriginalPrice.FormattedValue`,2) AS full_price,  
  `line.ProductVariant.Id` AS variant_id,  
  `line.ProductVariant.Product.Id` AS product_id,  
  `line.ProductVariant.VariantNumber` AS variant_number,  
  `line.ProductSize.Id` AS product_size,  
  `line.ProductSize.SKU` AS size_sku,  
  `line.ProductSize.SizeNumber` AS size_number,  
  `line.ProductSize.GTIN` AS size_gtin,  
  `line.ProductSize.Size.Id` AS size_id,  
  `line.ProductSize.Size.Name` AS size_name,  
  toFloat(`line.LineValue.FormattedValue`) AS Non_converted_value,  
  `line.UnitPrice.FormattedValue` AS Unitprice_formatted_value,  
  `line.UnitOriginalPrice.FormattedValue` AS Unit_original_price_formatted_value,  
  `line.Quantity` AS quantity,  
  `line.ReturnedQuantity` AS returned_quantity,  
  `line.CancelledQuantity` AS cancelled_quantity,  
  `line.ProductNumber` AS product_number,  
  `line.TypeName` AS type,  
  round(`line.DiscountPercent`,0) AS discount_percent,  
  `line.TaxPercent` AS tax_percent,  
  `order.Id` AS order_id,  
  `order.Number` AS order_number,  
  unixTimestamp(`order.CreatedAt`, '2006-01-02T15:04:05-0700') AS order_created_at,  
  `order.Status` AS order_status,  
  `order.GrandTotal.FormattedValue` AS total order value inc VAT,  
  `order.Shipments[0].CarrierInformation.ServiceName` AS carrier_service_name,  
  `order.Shipments[0].CarrierInformation.CarrierName` AS carrier_name,  
  `order.Market.Name` AS order_market,  
  `order.Store.Name` AS store,  
  `order.Country.Name` AS country,  
  `order.PaymentMethod.Name` AS order_payment_method,  
  `order.Totals.LineValues` AS order_totals_values,  
  `order.Totals.Shipping` AS order_total_shipping,  
  `order.Totals.Discounts` AS order_total_discounts,  
  `order.Totals.Handling` AS order_totals_handling,  
  `order.CurrencyBaseRate` AS order_currency_base_rate,  
  `order.Discounts` AS order_discounts,  
  `order.Discounts.Len` AS order_discounts_len,  
  `order.DiscountsApplied.Name` AS discount_name,  
  `order.DiscountsApplied.Method` AS order_discounts_applied_method,  
  `order.DiscountsApplied.Value` AS order_discounts_applied_value,  
  `order.DiscountsApplied.Discount.Codes` discount_codes,  
  Currency AS currency,  
  CurrencyOK AS currency_ok  
FROM`interactions.gz`  
```
_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### Items
Id columns : item
```
SELECT
	concat(`variant.Id`,'_',`variant.productSize.Size.Id`) AS item, 
	`prod.Name` AS prod_name,  
	`variant.MediaURL` AS variant_media_url,  
	`variant.Id` AS id,  
	`variant.Name` AS variant_name,  
	`variant.Status` AS variant_status,  
	`variant.StockOffset` AS variant_stock_offset,  
	`variant.InternalName` AS variant_internal_name,  
	`variant.variantNumber` AS variant_variant_number,  
	`variant.UnitCost.FormattedValue` AS variant_unit_cost_formatted_value,  
	`variant.productSize.Id` AS variant_product_size_id,  
	`variant.productSize.GTIN` AS variant_product_size_gtin,  
	`variant.productSize.SizeNumber` AS variant_product_size_number,  
	`variant.productSize.SKU` AS variant_product_size_sku,  
	`variant.productSize.Size.Id` AS variant_product_size_size_id,  
	`variant.productSize.Size.Name` AS variant_product_size_size_name,  
	`prod.Id` AS prod_id,  
	`prod.ProductNumber` AS prod_product_number,  
	`prod.Brand.Name` AS prod_brand_name,  
	`prod.CountryOfOrigin.Name` AS prod_country_of_origin_name,  
	`prod.Collection.Name` AS prod_collection_name,  
	`prod.Status` AS prod_status,  
	`prod.HarmonizedCommodityCode` AS prod_harmonized_commodity_code,  
	`prod.Folder.Name` AS prod_folder_name,  
	`display.Store.Name` AS display_store_name,  
	`display.Status` AS display_status,  
	`display.Name` AS display_name,  
	`display.DisplayItem.Id` AS display_item_id,  
	`display.Categories` AS display_categories,  
	`display.Category1` AS display_category_1,  
	`display.Category2` AS display_category_2,  
	`display.Category3` AS display_category_3,  
	`display.CategoryUri` AS display_category_uri,  
	`display.Uri` AS display_uri,  
	`variant.productSize.Size.AvailableNowQuantity` AS variant_available_now_quantity,  
	`variant.Price` AS variant_price,  
	`variant.Currency` AS variant_currency,  
	`variant.Campaign_DiscountPercent` AS variant_campaign_discount_percent,  
	`variant.Campaign_FixedPrice` AS variant_campaign_fixed_price,  
	`variant.Campaign_FixedPrice_Currency` AS variant_campaign_fixed_price_currency,  
	market AS market,  
    
      concat(`prod.Brand.Name`, ', ', `prod.Name`,   
         if(`variant.Name` != '' OR `variant.productSize.Size.Name` != '', ' ', ''),  
         if(`variant.Name` != '', concat('[',`variant.Name`, ']'),''),  
         if(`variant.productSize.Size.Name` != '', concat('[',`variant.productSize.Size.Name`,']'), '')   
         ) format
FROM `items.gz`
```
_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### Users
Id columns : user
```
SELECT  
`customer.Id` AS user,  
	`customer.IsAnonymized` AS anonymized,  
	`customer.TotalOrders` AS total_orders,  
	unixTimestamp(`customer.CreatedAt`, '2006-01-02T15:04:05-0700') AS created_at,  
	unixTimestamp(`customer.UpdatedAt`, '2006-01-02T15:04:05-0700') AS updated_at,  
	`customer.Store.Name` AS store,  
	`customer.Email` AS email,  
	`customer.CellPhoneNumber` AS phone  
FROM `users.gz`  
```
_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### Variant model 

[*Back to top*](#table-of-contents)

#### Interactions 

[*Back to top*](#table-of-contents)

##### Id columns 
`user,id`

```
SELECT  
  `order.Customer.Id` AS user,
  `line.Id` AS id,
  unixTimestamp(`order.OrderDate`, '2006-01-02T15:04:05-07:00') AS ts,  
  `line.ProductVariant.Id` AS item,  
  toFloat(`line.LineValue.FormattedValue`)*toFloat(`order.CurrencyBaseRate`) AS revenue,  
  round(`line.Quantity`*`order.CurrencyBaseRate`*`line.UnitOriginalPrice.FormattedValue`,2) AS full_price,  
  `line.ProductVariant.Id` AS variant_id,  
  `line.ProductVariant.Product.Id` AS product_id,  
  `line.ProductVariant.VariantNumber` AS variant_number,  
  `line.ProductSize.Id` AS product_size,  
  `line.ProductSize.SKU` AS size_sku,  
  `line.ProductSize.SizeNumber` AS size_number,  
  `line.ProductSize.GTIN` AS size_gtin,  
  `line.ProductSize.Size.Id` AS size_id,  
  `line.ProductSize.Size.Name` AS size_name,  
  toFloat(`line.LineValue.FormattedValue`) AS Non_converted_value,  
  `line.UnitPrice.FormattedValue` AS Unitprice_formatted_value,  
  `line.UnitOriginalPrice.FormattedValue` AS Unit_original_price_formatted_value,  
  `line.Quantity` AS quantity,  
  `line.ReturnedQuantity` AS returned_quantity,  
  `line.CancelledQuantity` AS cancelled_quantity,  
  `line.ProductNumber` AS product_number,  
  `line.TypeName` AS type,  
  round(`line.DiscountPercent`,0) AS discount_percent,  
  `line.TaxPercent` AS tax_percent,  
  `order.Id` AS order_id,  
  `order.Number` AS order_number,  
  unixTimestamp(`order.CreatedAt`, '2006-01-02T15:04:05-0700') AS order_created_at,  
  `order.Status` AS order_status,  
  `order.GrandTotal.FormattedValue` AS total_order_value_inc_VAT,  
  `order.Shipments[0].CarrierInformation.ServiceName` AS carrier_service_name,  
  `order.Shipments[0].CarrierInformation.CarrierName` AS carrier_name,  
  `order.Market.Name` AS order_market,  
  `order.Store.Name` AS store,  
  `order.Country.Name` AS country,  
  `order.PaymentMethod.Name` AS order_payment_method,  
  `order.Totals.LineValues` AS order_totals_values,  
  `order.Totals.Shipping` AS order_total_shipping,  
  `order.Totals.Discounts` AS order_total_discounts,  
  `order.Totals.Handling` AS order_totals_handling,  
  `order.CurrencyBaseRate` AS order_currency_base_rate,  
  `order.Discounts` AS order_discounts,  
  `order.Discounts.Len` AS order_discounts_len,  
  `order.DiscountsApplied.Name` AS discount_name,  
  `order.DiscountsApplied.Method` AS discounts_applied_method,  
  `order.DiscountsApplied.Value` AS discounts_applied_value,  
  `order.DiscountsApplied.Discount.Codes` AS discount_codes,  
  Currency AS currency,  
  CurrencyOK AS currency_ok  
FROM `interactions.gz`
```

[*Back to top*](#table-of-contents)

#### Items

[*Back to top*](#table-of-contents)

##### Id columns 
`item`

```
SELECT
	`variant.Id` AS item, 
	`prod.Name` AS prod_name,  
	`variant.MediaURL` AS variant_media_url,  
	`variant.Id` AS variant_id,  
	`variant.Name` AS variant_name, 
    --`variant.productSize.SKU` AS variant_product_size_sku,   
	`variant.Status` AS variant_status,  
	`variant.StockOffset` AS variant_stock_offset,  
	`variant.InternalName` AS variant_internal_name,  
	`variant.variantNumber` AS variant_variant_number,  
	`variant.UnitCost.FormattedValue` AS variant_unit_cost_formatted_value,  
	--`variant.productSize.Id` AS variant_product_size_id,  
	--`variant.productSize.GTIN` AS variant_product_size_gtin,  
	--`variant.productSize.SizeNumber` AS variant_product_size_size_number,  
	--`variant.productSize.Size.Id` AS variant_product_size_size_id,  
	--`variant.productSize.Size.Name` AS variant_product_size_size_name,  
	`prod.Id` AS prod_id,  
	`prod.ProductNumber` AS prod_product_number,  
	`prod.Brand.Name` AS prod_brand_name,  
	`prod.CountryOfOrigin.Name` AS prod_country_of_origin_name,  
	`prod.Collection.Name` AS prod_collection_name,  
	`prod.Status` AS prod_status,  
	`prod.HarmonizedCommodityCode` AS prod_harmonized_commodity_code,  
	`prod.Folder.Name` AS prod_folder_name,  
	`display.Store.Name` AS display_store_name,  
	`display.Status` AS display_status,  
	`display.Name` AS display_name,  
	`display.DisplayItem.Id` AS display_display_item_id,  
	`display.Categories` AS display_categories,  
	`display.Category1` AS display_category_1,  
	`display.Category2` AS display_category_2,  
	`display.Category3` AS display_category_3,  
	`display.CategoryUri` AS display_category_uri,  
	`display.Uri` AS display_uri,  
	--`variant.productSize.Size.AvailableNowQuantity` AS available_now_quantity,  
	`variant.Price` AS variant_price,  
	`variant.Currency` AS variant_currency,  
	`variant.Campaign_DiscountPercent` AS variant_campaign_discount_percent,  
	`variant.Campaign_FixedPrice` AS variant_campaign_fixed_price,  
	`variant.Campaign_FixedPrice_Currency` AS variant_campaign_fixed_price_currency,  
	market AS market,  
    
      concat(`prod.Brand.Name`, ', ', `prod.Name`,
         if(`variant.Name` != '', concat(' [',`variant.Name`, ']'),'')  
         ) format
FROM `items.gz`
```

[*Back to top*](#table-of-contents)

#### Users

[*Back to top*](#table-of-contents)

##### Id columns 
`user`

```
SELECT  
	`customer.Id` AS user,  
	`customer.IsAnonymized` AS anonymized,  
	`customer.TotalOrders` AS total_orders,  
	unixTimestamp(`customer.CreatedAt`, '2006-01-02T15:04:05-0700') AS created_at,  
	unixTimestamp(`customer.UpdatedAt`, '2006-01-02T15:04:05-0700') AS updated_at,  
	`customer.Store.Name` AS store,  
	`customer.Email` AS email,  
	`customer.CellPhoneNumber` AS phone  
FROM `users.gz` 
```

_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### No size model 
for Item source called ‘no size model - items’
```
SELECT 
	variantId AS id,  
    groupcoalesce(format) AS format,  
	groupcoalesce(productName) AS product_name,  
    groupcoalesce(variantName) AS variant_name,  
	groupcoalesce(variantStatus) AS variant_status,  
    groupcoalesce(brand) AS brand,  
    groupcoalesce(`prod.Folder.Name`) AS prod_folder_name,  
    groupcoalesce(collection) AS collection,  
    groupcoalesce(productNumber) AS product_number,  
    groupcoalesce(price) AS price,  
    groupcoalesce(availableNowQuantity) AS available_now_quantity,  
    groupcoalesce(countryOfOrigin) AS country_of_origin,  
    groupcoalesce(mediaURL) AS media_url,  
    groupcoalesce(unitCost) AS unit_cost,  
    groupcoalesce(productStatus) AS product_status,  
    groupcoalesce(variantInternalName) AS variant_internal_name,  
    groupcoalesce(displayCategory1) AS display_category_1,  
    groupcoalesce(displayCategory2) AS display_category_2,  
    groupcoalesce(displayCategory3) AS display_category_3,  
    groupcoalesce(displayItemId) AS display_item_id  
 
FROM `centra_products_import`  

GROUP BY variantId  
```
_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

### Example rows with explanation

Coalesce (`display.Name`, `prod.Name`, `variant.Id`) AS format 
Explanation: Choose display.Name if it exists, otherwise check prod.Name, and lastly variant.Id.  

Concat (`line.ProductVariant.Id`,'_',`line.ProductSize.Size.Id`) AS item 
Explanation: This will merge the two lines, for example Concat (Hello, '_', you) would concat to Hello_you 

unixTimestamp (`order.CreatedAt`, '2006-01-02T15:04:05-0700') AS order_created_at, 
	Explanation: This will convert a date into number form 
_____________________________________________________________________________________________________________________

[*Back to top*](#table-of-contents)

## Voyado Queries
[Back to top](#table-of-contents)
___
Procedure	1

Items	2  

Users	3

Interactions	4  
___

[*Back to top*](#table-of-contents)

### Procedure
Setup config
___

[*Back to top*](#table-of-contents)

### Interactions

From `RAW - receiptItems` + `RAW - stores`

[*Back to top*](#table-of-contents)

##### Id columns 
`id,user`

```
SELECT 
  user,
  t.id id,
  unix_timestamp(transactionDateTime, '2006-01-02T15:05:05Z') ts,
  articleNumber item,
  receiptItemId,
  receiptId,
  t.type type,
  quantity,
  grossPaidPrice price,
  awardsBonus,
  stores.name store,
  stores.city store_city,
  stores.country store_country,
  stores.externalId butikskod,
  stores.type store_type
FROM `RAW - receiptItems` t
LEFT JOIN `RAW - store` stores on t.storeId = stores.id
WHERE user != ''
```
___

[*Back to top*](#table-of-contents)

### Stores

[*Back to top*](#table-of-contents)

##### Id column
`id`

```
SELECT
	storeId id,
    name,
    isDeleted,
    city,
    country,
    zipCode,
    street,
    region,
    externalId,
    type,
    active,
    changeType

FROM `store/byExportDate/*/*/*/*.csv`

-- WHERE unix_timestamp(implode(slice(split(path(),'/'), 2,5), '/'), '2006/01/02') >= now()-7*24*60*60
```
___

[*Back to top*](#table-of-contents)

### Contacts

[*Back to top*](#table-of-contents)

##### Id column
`id`

```
SELECT 
  contactId id,
  contactType,
  isApproved,
  isDeleted,
  gender,
  age,
  zipCode,
  city,
  countryCode,
  acceptsEmail,
  acceptsSms,
  acceptsPostal,
  statusEmail,
  statusSms,
  statusPostal,
  rfm,
  recency,
  frequency,
  monetary,
  latestNpsGrade,
  latestNpsDateTime,
  registrationDateTime,
  lastModifiedDateTime,
  deletedDateTime,
  deletedReason,
  recruitedStoreId,
  currentStoreId,
  changeType
FROM `allContacts/byExportDate/*/*/*/*.csv`
WHERE unix_timestamp(implode(slice(split(path(),'/'), 2,5), '/'), '2006/01/02') >= now()-7*24*60*60
```
___

[*Back to top*](#table-of-contents)

## Query expressions
you need to enclose variable names that contain other characters than letters and numbers with `backticks` ``,  
this includes whitespace ' ', dot '.', etc...

SELECT * 

LEFT JOIN

coalese

toFloat()

unixTimestamp()

split()

slice()

etc...

[*Back to top*](#table-of-contents)

# Results

[*Back to top*](#table-of-contents)

## dummy1

[*Back to top*](#table-of-contents)

## dummy2

[*Back to top*](#table-of-contents)

# Import Files

[*Back to top*](#table-of-contents)
