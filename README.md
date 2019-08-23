
# Plotting Data Lab

### Learning Objectives

* Understand the components of a point in a graph, an $x$ value, and a $y$ value 
* Understand how to plot a point on a graph, from a point's $x$ and $y$ value
* Get a sense of how to use a graphing library, like Plotly, to answer questions about our data

### Working again with our travel data

Let's again get our travel data from our excel spreadsheet.  If we do not already have `pandas` and `xlrd` for retrieving data from excel, we should install it now.


```python
!pip install pandas
!pip install xlrd
```


```python
import pandas
file_name = './cities.xlsx'
travel_df = pandas.read_excel(file_name)
cities = travel_df.to_dict('records')
```


```python
# __SOLUTION__ 
!pip install pandas
!pip install xlrd
```

    Requirement already satisfied: pandas in /Users/lore.dirick/anaconda3/lib/python3.6/site-packages (0.22.0)
    Requirement already satisfied: python-dateutil>=2 in /Users/lore.dirick/anaconda3/lib/python3.6/site-packages (from pandas) (2.6.1)
    Requirement already satisfied: pytz>=2011k in /Users/lore.dirick/anaconda3/lib/python3.6/site-packages (from pandas) (2017.3)
    Requirement already satisfied: numpy>=1.9.0 in /Users/lore.dirick/anaconda3/lib/python3.6/site-packages (from pandas) (1.14.3)
    Requirement already satisfied: six>=1.5 in /Users/lore.dirick/anaconda3/lib/python3.6/site-packages (from python-dateutil>=2->pandas) (1.11.0)
    [33mYou are using pip version 18.1, however version 19.0.2 is available.
    You should consider upgrading via the 'pip install --upgrade pip' command.[0m
    Requirement already satisfied: xlrd in /Users/lore.dirick/anaconda3/lib/python3.6/site-packages (1.1.0)
    [33mYou are using pip version 18.1, however version 19.0.2 is available.
    You should consider upgrading via the 'pip install --upgrade pip' command.[0m



```python
# __SOLUTION__ 
import pandas
file_name = './cities.xlsx'
travel_df = pandas.read_excel(file_name)
cities = travel_df.to_dict('records')
```

> Press shift + enter to run the code above.


```python
cities
```


```python
# __SOLUTION__ 
cities
```




    [{'Area': 4758,
      'City': 'Buenos Aires',
      'Country': 'Argentina',
      'Population': 2891000},
     {'Area': 2731571,
      'City': 'Toronto',
      'Country': 'Canada',
      'Population': 2800000},
     {'Area': 3194,
      'City': 'Pyeongchang',
      'Country': 'South Korea',
      'Population': 2581000},
     {'Area': 200, 'City': 'Marakesh', 'Country': 'Morocco', 'Population': 928850},
     {'Area': 491,
      'City': 'Albuquerque',
      'Country': 'New Mexico',
      'Population': 559277},
     {'Area': 3750,
      'City': 'Los Cabos',
      'Country': 'Mexico',
      'Population': 287651},
     {'Area': 68, 'City': 'Greenville', 'Country': 'USA', 'Population': 84554},
     {'Area': 8300,
      'City': 'Archipelago Sea',
      'Country': 'Finland',
      'Population': 60000},
     {'Area': 33,
      'City': 'Walla Walla Valley',
      'Country': 'USA',
      'Population': 32237},
     {'Area': 27, 'City': 'Salina Island', 'Country': 'Italy', 'Population': 4000},
     {'Area': 59, 'City': 'Solta', 'Country': 'Croatia', 'Population': 1700},
     {'Area': 672,
      'City': 'Iguazu Falls',
      'Country': 'Argentina',
      'Population': 0}]



### Plotting our first graph

As we can see, in our list of cities, each city has a population number.  Our first task will be to display the populations of our first three cities in a bar chart.

First we load the plotly library into our notebook, and we initialize this offline mode.


```python
import plotly

plotly.offline.init_notebook_mode(connected=True)
# use offline mode to avoid initial registration
```


```python
# __SOLUTION__ 
import plotly

plotly.offline.init_notebook_mode(connected=True)
# use offline mode to avoid initial registration
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


Now the next step is to build a trace.  As we know our trace is a dictionary with a key of `x` and a key of `y`.  We have set up a trace to look like the following: `trace_first_three = {'x': x_values, 'y': y_values}`.  

First define `x_values` so that it is a list of names of the first three cities.  Use what we learned about accessing information from lists and dictionaries to assign `x_values` equal to the first three cities.


```python
x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
```


```python
# __SOLUTION__ 
x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
```

Now use list and dictionary accessors to set `y_values` equal to the first three populations.


```python
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
```


```python
# __SOLUTION__ 
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
```

Now let's plot our data.


```python
trace_first_three_pops = {'x': x_values, 'y': y_values}


plotly.offline.iplot([trace_first_three_pops])
```


```python
# __SOLUTION__ 
trace_first_three_pops = {'x': x_values, 'y': y_values}


plotly.offline.iplot([trace_first_three_pops])
```


<div id="eec07355-8301-45ab-af9b-fde5a143e19c" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("eec07355-8301-45ab-af9b-fde5a143e19c", [{"x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [2891000, 2800000, 2581000], "type": "scatter", "uid": "33ace388-30a7-11e9-90f4-88e9fe4c5d44"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Modifying our first trace

Note that by default, plotly sets the type of trace as a line trace.  In the next example, let's make our trace a bar trace by setting the `'type'` key equal to `'bar'`.  We can continue to use our lists of `x_values` and `y_values` that we defined above and used in our previous trace. To make our new trace more informative, we can assign labels to our data when we plot it. Normally, when we see a bar graph, there are labels along the x-axis for specific values. Understanding that we are plotting data about different cities, our labels would sensibly be a list of corresponding city names. 

We can designate these corresponding city names in our trace dictionary by assigning a list of strings to the `text` key:

```python
example_trace = {'type': 'bar', 'x': x_values, 'y': y_values, 'text': ["label_1", "label_2", "label_3"]}
```

Assign the variable `text_values` equal to a list of names for the first three cities. Then we pass this information to our trace dictionary and assign it as the value for its `text` key.


```python
text_values = []
bar_trace_first_three_pops = {'type': 'scatter', 'text': text_values}
```


```python
bar_trace_first_three_pops['type'] # 'bar'
```


```python
plotly.offline.iplot([bar_trace_first_three_pops])
```


```python
# __SOLUTION__ 
text_values =  ["Buenos Aires", "Toronto", "Pyeongchang"]
bar_trace_first_three_pops = {'type': 'bar', 'x': x_values, 'y': y_values, 'text': text_values}
```


```python
# __SOLUTION__ 
bar_trace_first_three_pops['type'] # 'bar'
```




    'bar'




```python
# __SOLUTION__ 
plotly.offline.iplot([bar_trace_first_three_pops])
```


<div id="e83c1085-8c8d-4d1a-b336-f68a58ad076d" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("e83c1085-8c8d-4d1a-b336-f68a58ad076d", [{"text": ["Buenos Aires", "Toronto", "Pyeongchang"], "x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [2891000, 2800000, 2581000], "type": "bar", "uid": "33c2570c-30a7-11e9-8b73-88e9fe4c5d44"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Adding a second trace to plot side by side

Ok, now let's plot two different traces side by side.  First, create another trace called `bar_trace_first_three_areas` that is like our `bar_trace_first_three_pops` except the values are a list of areas.  We will display this side by side along our `bar_trace_first_three_pops` in the plot below.


```python
bar_trace_first_three_areas = {'type': 'scatter', 'x': [], 'y': [], 'text': []}
bar_trace_first_three_pops = {'type': 'scatter', 'x': [], 'y': [], 'text': []}
```


```python
plotly.offline.iplot([bar_trace_first_three_pops, bar_trace_first_three_areas])
```


```python
# __SOLUTION__ 
area_values = [cities[0]['Area'], cities[1]['Area'],cities[2]['Area']]
bar_trace_first_three_areas = {'type': 'bar', 'x': x_values,'y': area_values, 'text': text_values}
bar_trace_first_three_pops = {'type': 'bar', 'x': x_values, 'y': y_values, 'text': text_values}
```


```python
# __SOLUTION__ 
plotly.offline.iplot([bar_trace_first_three_pops, bar_trace_first_three_areas])
```


<div id="0f652d53-876a-4e5f-8b9f-b34f1f415179" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("0f652d53-876a-4e5f-8b9f-b34f1f415179", [{"text": ["Buenos Aires", "Toronto", "Pyeongchang"], "x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [2891000, 2800000, 2581000], "type": "bar", "uid": "33cdc3dc-30a7-11e9-94cb-88e9fe4c5d44"}, {"text": ["Buenos Aires", "Toronto", "Pyeongchang"], "x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [4758, 2731571, 3194], "type": "bar", "uid": "33cdc546-30a7-11e9-ba67-88e9fe4c5d44"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Summary

In this section, we saw how we use data visualizations to better understand the data.  We do the following.  Import plotly:


    import plotly

    plotly.offline.init_notebook_mode(connected=True)

Then we define a trace, which is a Python dictionary.

    trace = {'x': [], 'y': [], 'text': [], 'type': 'bar'}
    
Finally, we display our trace with a call to the following method:

    plotly.offline.iplot([trace])
    
Easy peasy, quick and easy!
