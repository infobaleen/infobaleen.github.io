# Table of Contents
1. [Solution Methods With Use Cases](#solution-methods-with-use-cases)
    1. [Year-on-Year analysis](#year-on-year-analysis)
        1. [Prepare Sources](#prepare-sources)
        1. [Prepare Expressions](#prepare-expressions)
        1. [Setup Dashboard ](#setup-dashboard)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Solution Methods With Use Cases

[*Back to top*](#table-of-contents)

## Year-on-Year analysis

Most customers want to see comparisons of sales agains last year's numbers. This is a solution I did to show that with the tools we had at the time.

Noted by Felix 2022-05-18

[*Back to top*](#table-of-contents)

### Prepare Sources

To produce the data needed, I added the columns `yoy_ts` and `yoy_year` to the interaction source with the following logic based on `ts` being the timestamp of the interaction:

    if(ts < now - 2 years, 'Older', if(ts < now - 1 year, 'Last year', 'This year')) AS yoy_year

    if(ts < now - 2 years, '', if(ts < now - 1 year, ts + 1 year, ts)) AS yoy_ts

The logic is that interactions older than 2 years are labeled *Older*, between 1-2 year are labeled *Last year* and newer than 1 year are labeled *This year*. Then to calculate the timestamp, interactions older than 2 years by are removed, interactions between 1-2 years ago get a date 1 year later, and interactions within 1 year keep their date. 

[*Back to top*](#table-of-contents)

### Prepare Expressions

I added the new fields to the data model, with `yoy_year` as Category and `yoy_ts` as Number. To use the new field as a Timestamp, I added a *Year-on-Year Date* as this expression

    toStartOfDay(toDate(toUnixTimestamp(yoy_ts)))

Then to compare revenue between the years I added *YoY Revenue (This year)* and *YoY Revenue (Last year)* by

    sumIf(revenue, yoy_year = 'This year')
    sumIf(revenue, yoy_year = 'Last year')

This can be applied to count unique orders, sold units etc.

[*Back to top*](#table-of-contents)

### Setup Dashboard 

These elements can be included anywhere, but I first tried these in a new dashboard.

**Line Chart**: I created a Line Chart with xValue as *Year-on-Year Date*. The yValue can be anything like Revenue, Unique Orders and so on. Then under Advanced I selected yoy_year as group key.

**Date Filter**: I added a date filter on *Year-on-Year Date* to be able to adjust the time scale.

**Metric with Comparison**: To show metrics with change from last year I created a metric with *YoY Revenue (This year)* as main metric and *YoY Revenue (Last year)* as secondary metric.

**Bar Chart with Comparison**: I also tried Bar Charts with *YoY Revenue (This year)* as main metric and *YoY Revenue (Last year)* as secondary metric that could show differnces in sales for each item category and so on.

[*Back to top*](#table-of-contents)
