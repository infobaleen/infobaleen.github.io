# Agent: Filesystem query helper functions

The agent supports a powerful query language for CSV files. Below are available helper
functions and some practical examples that might be useful when setting up your sources.

## Operators and Functions
* `x LIKE format`
* `x IN(a,b,...)`
* `a OR b`
* `a AND b`
* `a = b`
* `a < b`
* `a > b`
* `a <= b`
* `a >= b`
* `a <> b`
* `multiIf(cond1,val1,...,defaultVal)` Ex: `multiIf(a > 1, 'a>1', 'a<=1')`
* `sleep(millisec)`

### Numerical
* `abs(x)`
* `floor(x)`
* `ceil(x)`
* `round(x)`
* `least(a,b)`
* `greatest(a,b)`

### Time (uses go's time formatting: eg. 2006-01-02 15:04:05)
* `unixTimestamp(x [,format])` Ex: `unixTimestamp('2015-01-01', '2006-01-02')` => `1420070400`
* `fromUnixtime(x [,format])` Ex: `fromUnixTime(1420070400, '2006-01-02')` => `2015-01-01`
* `now()` Ex: `now()` => `1571038684`

### String
* `sluggify(x)` Ex: `sluggify('HelloWorld')` => `hello-world`
* `queryescape(x)` QueryEscape escapes the string so it can be safely placed inside a URL query.
* `match(pattern,name)` (uses go's `path.Match`)
* `slice(x, start, stop, delimiter)` Ex: `slice('a-b-c', 0, 1, '-')` => `a`
* `sort(x,delimiter)` Ex: `sort('c-a-b')` => `a-b-c`
* `reverse(x, delimiter)` Ex: `reverse('abc', '')` => `cba`, `reverse('a-b-c')` => `c-b-a`
* `concatWs(delimiter,xs...)` Ex: `concatWs('-', 'a', 'b')` => `a-b`
* `coalesce(xs...)` Ex: `coalesce('', 'fallback')` => `fallback`
* `concat(xs...)`  Ex: `concat('a', 'b')` => `ab`
* `replace(x,old,new)` Ex: `replace('foobar', 'bar', 'baz')` => `foobaz` 
* `lower(x)`
* `upper(x)`
* `length(x)`

### JSON
* `pickJson(x, fields...)` Ex: `pickJson('{"foo":1, "bar":2, "baz":3}', 'foo', 'bar')` => `{"foo":1, "bar":2}`

### Hash/rand
* `rand()`
* `randInt()`
* `randInt(x)`
* `md5(x)`
* `xxHash63(x)`
* `xxHash64(x)`
* `identity(x)` Ex: `identity('a')` => `a`

### File Details 
* `size()`
* `path()`
* `modifiedAt()`
* `depth()`

### Special
* `analyse()` Anlayse column data. Ex: `select analyse(price) from ...` => `{"CountNum":431359,"CountEmpty":0,"CountString":0,"Sum":555691303,"Average":1288.2339364285353,"Min":1,"Max":618993.5625}`

## Join
Inner joins are supported, but limited to only one joined table. The join must be written in the following format.
Note that joins must load the secondary table data into RAM, so use this feature wisely. 
```
SELECT *, u.* from `transaction.csv` t JOIN `users.csv` u ON t.user_id = u.id
```
Note that when referring to the joined table in the `select`, you must use an alias, but not for the `from` file.

## Sub queries
Support for sub queries.
Since the join support is limited, this is the typical use case for using sub queries 
```
SELECT * from `transactions.csv` WHERE user_id IN (SELECT id FROM `users.csv`) t
```

## Practical Examples

### Convert date to unix timestamp
Uploaded interaction data requires a column with unix timestamp data, making this function useful.
See different examples below depending on date format (go date format). See [https://yourbasic.org/golang/format-parse-string-time-date-example/]
```
unix_timestamp(ts_string,<FORMAT>)
unix_timestamp(ts_string,"2006-01-02 15:04:05")
unix_timestamp(ts_string,"2006-01-02T15:04:05Z")
```

#### Example: Age from time string
```
round((now() - unix_timestamp(birth_year,"2006-01-02")) / (60 * 60 * 24 * 365)) as age
```

### String concatenation
```
concat(title, '(', author, ', ', year, ')') as displayName
```

#### Example: Building image urls
```3
concat('/api/v1/image?w=300&h=200&label=', queryEscape(english_title)) as dummy_image
```

### Multi if

#### Example: Build filter variables
For item id's that you want to exclude, build a variable and then filter on it
in the data model setup.
```
multiIf(_id IN (123, 456, 789) OR category_4='Candy', 1, 0) as is_irrelevant
```

#### Example: Name from id
```
multiIf(
    store_id = "b92a0b68-3b4b-4fba-8711-a69100e940e9","Umeå",
    store_id = "48292bda-f26c-428e-8de5-a69100e940e9","Göteborg",
    store_id = "8d46721c-2368-480b-913a-a69100e940e9","Stockholm",
'unknown_store') as store,
```
