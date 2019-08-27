
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




    [{'City': 'Buenos Aires',
      'Country': 'Argentina',
      'Population': 2891082,
      'Area': 203},
     {'City': 'Toronto', 'Country': 'Canada', 'Population': 2731571, 'Area': 630},
     {'City': 'Pyeongchang',
      'Country': 'South Korea',
      'Population': 43666,
      'Area': 1464},
     {'City': 'Marakesh', 'Country': 'Morocco', 'Population': 928850, 'Area': 230},
     {'City': 'Albuquerque', 'Country': 'USA', 'Population': 558545, 'Area': 491},
     {'City': 'Los Cabos',
      'Country': 'Mexico',
      'Population': 287671,
      'Area': 3751},
     {'City': 'Greenville', 'Country': 'USA', 'Population': 93137, 'Area': 68},
     {'City': 'Archipelago Sea',
      'Country': 'Finland',
      'Population': 60000,
      'Area': 2000},
     {'City': 'Walla Walla Valley',
      'Country': 'USA',
      'Population': 32986,
      'Area': 35},
     {'City': 'Salina Island', 'Country': 'Italy', 'Population': 2598, 'Area': 26},
     {'City': 'Solta', 'Country': 'Croatia', 'Population': 1700, 'Area': 59},
     {'City': 'Iguazu Falls',
      'Country': 'Argentina',
      'Population': 0,
      'Area': 2396}]




```python
# __SOLUTION__ 
cities
```




    [{'City': 'Buenos Aires',
      'Country': 'Argentina',
      'Population': 2891082,
      'Area': 203},
     {'City': 'Toronto', 'Country': 'Canada', 'Population': 2731571, 'Area': 630},
     {'City': 'Pyeongchang',
      'Country': 'South Korea',
      'Population': 43666,
      'Area': 1464},
     {'City': 'Marakesh', 'Country': 'Morocco', 'Population': 928850, 'Area': 230},
     {'City': 'Albuquerque', 'Country': 'USA', 'Population': 558545, 'Area': 491},
     {'City': 'Los Cabos',
      'Country': 'Mexico',
      'Population': 287671,
      'Area': 3751},
     {'City': 'Greenville', 'Country': 'USA', 'Population': 93137, 'Area': 68},
     {'City': 'Archipelago Sea',
      'Country': 'Finland',
      'Population': 60000,
      'Area': 2000},
     {'City': 'Walla Walla Valley',
      'Country': 'USA',
      'Population': 32986,
      'Area': 35},
     {'City': 'Salina Island', 'Country': 'Italy', 'Population': 2598, 'Area': 26},
     {'City': 'Solta', 'Country': 'Croatia', 'Population': 1700, 'Area': 59},
     {'City': 'Iguazu Falls',
      'Country': 'Argentina',
      'Population': 0,
      'Area': 2396}]



### Plotting our first graph

As we can see, in our list of cities, each city has a population number.  Our first task will be to display the populations of our first three cities in a bar chart.

First we load the plotly library into our notebook, and we initialize this in offline mode.


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


<div id="2e7f526f-7693-401a-99f8-b79659bd6207" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("2e7f526f-7693-401a-99f8-b79659bd6207", [{"x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [2891082, 2731571, 43666], "type": "scatter", "uid": "d364c10c-c90e-11e9-b7db-3af9d3ad3e0b"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


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
# __SOLUTION__ 
text_values =  ["Buenos Aires", "Toronto", "Pyeongchang"]
bar_trace_first_three_pops = {'type': 'bar', 'x': x_values, 'y': y_values, 'text': text_values}
```


```python
bar_trace_first_three_pops['type'] # 'bar'
```


```python
# __SOLUTION__ 
bar_trace_first_three_pops['type'] # 'bar'
```




    'bar'




```python
plotly.offline.iplot([bar_trace_first_three_pops])
```


```python
# __SOLUTION__ 
plotly.offline.iplot([bar_trace_first_three_pops])
```


<div id="4ec42543-3f36-425e-a019-1494413b383f" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("4ec42543-3f36-425e-a019-1494413b383f", [{"text": ["Buenos Aires", "Toronto", "Pyeongchang"], "x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [2891082, 2731571, 43666], "type": "bar", "uid": "efedb9a8-c90e-11e9-9215-3af9d3ad3e0b"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Adding a second trace to plot side by side

Ok, now let's plot two different traces side by side.  First, create another trace called `bar_trace_first_three_areas` that is like our `bar_trace_first_three_pops` except the values are a list of areas.  We will display this side by side along our `bar_trace_first_three_pops` in the plot below.


```python
area_values = None
bar_trace_first_three_areas = {'type': 'bar', 'x': [], 'y': [], 'text': []}
bar_trace_first_three_pops = {'type': 'bar', 'x': [], 'y': [], 'text': []}
```


```python
# __SOLUTION__ 
area_values = [cities[0]['Area'], cities[1]['Area'],cities[2]['Area']]
bar_trace_first_three_areas = {'type': 'bar', 'x': x_values,'y': area_values, 'text': text_values}
bar_trace_first_three_pops = {'type': 'bar', 'x': x_values, 'y': y_values, 'text': text_values}
```


```python
plotly.offline.iplot([bar_trace_first_three_pops, bar_trace_first_three_areas])
```


```python
# __SOLUTION__ 
plotly.offline.iplot([bar_trace_first_three_pops, bar_trace_first_three_areas])
```


<div id="9d6d77a0-6f96-4944-8a18-42c078f136d5" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("9d6d77a0-6f96-4944-8a18-42c078f136d5", [{"text": ["Buenos Aires", "Toronto", "Pyeongchang"], "x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [2891082, 2731571, 43666], "type": "bar", "uid": "fead30c6-c90e-11e9-9274-3af9d3ad3e0b"}, {"text": ["Buenos Aires", "Toronto", "Pyeongchang"], "x": ["Buenos Aires", "Toronto", "Pyeongchang"], "y": [203, 630, 1464], "type": "bar", "uid": "fead31fa-c90e-11e9-8c1f-3af9d3ad3e0b"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Summary

In this section, we saw how we use data visualizations to better understand the data.  We do the following.  Import plotly:


    import plotly

    plotly.offline.init_notebook_mode(connected=True)

Then we define a trace, which is a Python dictionary.

    trace = {'x': [], 'y': [], 'text': [], 'type': 'bar'}
    
Finally, we display our trace with a call to the following method:

    plotly.offline.iplot([trace])
    
Easy peasy, quick and easy!
