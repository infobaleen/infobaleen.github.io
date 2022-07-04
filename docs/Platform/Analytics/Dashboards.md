## Dashboards 

You can customize dashboards to visualize various information and results based on your data.

Dashboards can be created by clicking the + icon in the dropdown menu, or by clicking the purple plus sign in the upper right corner of the dashboard card.

<img width="479" alt="Screenshot 2022-06-28 at 14 39 01" src="https://user-images.githubusercontent.com/4352260/176860359-ec0b5ec4-a1f3-48f0-91cb-0be050ada8fd.png">
<img width="825" alt="Screenshot 2022-06-28 at 14 39 42" src="https://user-images.githubusercontent.com/4352260/176860364-e988c2c1-d539-4da2-bdf4-3b498c883bc2.png">

When you create a dashboard your are asked for the below fieds:

* `Name`: The name you want to give to your dashboard. You can change this name later. 
* `Select Role`: One of `interaction`, `user`, and `item`. Defines what data the dashboard should be based on, and in most cases it should be `interaction`.
* `Select number of columns`: Specifies the number of columns used in the grid system to fit dashboards. The default value is used in most cases. 
* `Import config`: This field can be used if you want to copy or export a dashboard from another platform. It is left blank in most cases.

<img width="846" alt="Screenshot 2022-06-28 at 14 41 45" src="https://user-images.githubusercontent.com/4352260/176181082-ec55c555-6a8c-4731-afbd-e7b345f2e235.png">

Click `Create` to create the dashboard. You are now ready to add elements!

**Note!** After adding elements or editing the dashboard, remember to click `Save` in the top right corner.

<img width="863" alt="Screenshot 2022-06-28 at 14 47 35" src="https://user-images.githubusercontent.com/4352260/176182387-0007cbff-e150-42e1-8946-302f8718fe88.png">


## Add element



### Metric
A metric is a single number, wich means that you can not show a field in a metric element (a field is an array of metrics). you can convert a field into a metric by writing an expression ex. SUM(field) this returns a metric.  
![image](https://user-images.githubusercontent.com/103515314/169268739-3bfe1569-0bc7-4bf6-b02b-2fe887f7c84e.png)



### Bar Chart
A bar chart shows `categorical data` with rectangular bars indicating the `distributions of the data`, in the picture below, we for example see amount of `unique customers per country`, the bar charts can be used to adapt the dashboard to show only data from one specific country. Simply press the country you want to see information about, and the dashboard will update accordingly.

![image](https://user-images.githubusercontent.com/103515314/169268249-5b36de6b-d749-4950-bae0-d777b15afd6f.png)



### Line Chart
A line chart plots a graph with data points connected to a chosen metric, example below for example shows revenue over time.  
Hovering over the line chart data points, the revenue for that time will show.  
![image](https://user-images.githubusercontent.com/103515314/169269164-27b0ddf6-1a72-4641-b929-7e2ac5f72377.png)



#### Default (line chart)
Under default you can choose what values you want to include in your line chart, you can also select if you want the view to be from day to week, month etc. The `Format` selection lets you choose how many decimals you want, if you want the values to be shown as a percentage (%). The `Limit` lets you decide how many data points you want to show (the dots marked on the line). 



#### Style (line chart)
Here you can change the appearance of the linechart in the dashboards, feel free to test how the different margin settings affect the look of the line chart! By changing the `Title` or the `Sub title` no values will be changed, by changing it the chosen values only gets an alias.  



#### Advanced (line chart)
In the advanced tab you can select a `Group key`, you can read what that means [here](https://github.com/infobaleen/customer-success/wiki/Manage-Data#centra-queries)



##### Select group key
By addining a field in the select group key the line chart will show multiple lines where each line represents a category in the selected field.
This function should be combined with a bar chart where you can create a filter for the selected field. by filtering out categories in the barchart the line chart will show the remaning categories.  
![image](https://user-images.githubusercontent.com/103515314/169793194-e95c40cc-f767-44f3-8b51-b93325029023.png)

By filtering out a category in the barchart the line representing this category is removed from the line chart.
![image](https://user-images.githubusercontent.com/103515314/169793357-46fd7c3b-1413-4b51-8713-1330b07b155e.png)



### Histogram
A histogram is a graphical representation that shows data in specified ranges as vertical bins. It's similar to a bar chart.  
![image](https://user-images.githubusercontent.com/103515314/169790400-89b40628-b7b3-4bd9-b98d-0795c974f512.png)



### Date filter
The `Date filter` lets you adapt your dashboards to only show data for a chosen period of time, there are some premade limits, for example last week, last year etc. These can be found and chosen on the top of the date filter box after pressing it, you can also select a specified range of days by using the calendar.  
![image](https://user-images.githubusercontent.com/103515314/169789844-0fc3eb0c-c776-4623-b016-f473464ffbda.png)



### Range filter
`Range filter` allows you to only show data in the dashboards where a chosen value is within the chosen limit, for example if you only want to show data for items with prices between 100sek to 200sek.  



### Filter
Filter can be used to only show one category of chosen metric, and update the dashboard accordingly.  
![image](https://user-images.githubusercontent.com/103515314/169792451-0d7d5128-fc8f-4a3a-ac7d-320ff9e54a65.png)



### Metric selector
In the different `elements` added to your dashboard, for example a bar chart or line chart, there's the opportunity to select `*metric*`, if you then add a `Metric selector` and choose a metric, all the elements where `*metric*` has been chosen, will be updated to match the chosen metric in the `Metric selector`. Using this will allow quicker changes of the data shown, as you can use the metric selector instead of manually changing the other elements.  
![image](https://user-images.githubusercontent.com/103515314/169789635-791ba427-1f84-474f-bad4-8ae9019a5461.png)
 



### Alluvial Chart
An alluvial chart can be described as a flow diagram that represents changes in structures over time, for us this is mostly used to represent how segments of customers are changed over time, going from new, to lapsed (lost) customers.  
  
(There's a `Color scale` option under `Style` where the colors can be changed to blue/green/yellow/red instead of different shades of blue) 
Example of alluvial chart shown below.
![image](https://user-images.githubusercontent.com/103515314/169789543-fcdca3ef-b325-459b-b381-206caf973f3c.png)



### Markov Chart



### Table
This element adds a table to the dashboard, if the table gets to wide there's a scroll bar furthest down in the table allowing horizontal scrolling. The table can be `sorted` by pressing on the value/text you want to sort by. Under `Style` in the edit screen of a table, there's an opportunity to add a `Backround bar` which visualize how large/small the different values in the table are in comparison to the others. 



### Pivot
A pivot table is used to visualize patterns and trends in large amounts of data, it can for example be used to show amount of lapsed customers per order cohort shown in the example below. 
![image](https://user-images.githubusercontent.com/103515314/169789394-1f691c1e-f189-4fab-bc3b-b01d13ecb467.png)



### Image grid
The image grid shows pictures of products in a dashboard.  
![image](https://user-images.githubusercontent.com/103515314/169791317-67fc1463-e9ea-4d7f-b077-5fb0d4d2282d.png)



### Segments
Lets you show data for only a chosen segment, these segments can be created under the `Segmentations` part of the platform.



### Categories
Similar to barchart, categories let's you choose what category to show data for, when the data is several categories in one cell, for example Color = `[red;blue]` where red and blue are not correlated.  



### Text Content
The text content element is the most used element, it's basically just text that can be adapted through markdown language, for example # = header1 (largest) ## = header2, ### header3 etc.  
![image](https://user-images.githubusercontent.com/103515314/169791387-54ccec3b-5099-44aa-90e6-303bde780b7d.png)


