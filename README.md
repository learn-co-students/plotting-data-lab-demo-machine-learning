
# Plotting Data Lab

### Learning Objectives

* Understand the components of a point in a graph, an $x$ value, and a $y$ value 
* Understand how to plot a point on a graph, from a point's $x$ and $y$ value
* Get a sense of how to use a graphing library, like Plotly, to answer questions about our data

### Working again with our travel data

Let's again get our travel data from our excel spreadsheet.


```python
import pandas
file_name = './cities.xlsx'
travel_df = pandas.read_excel(file_name)
cities = travel_df.to_dict('records')
```


```python
cities
```




    [{'Area': 59, 'City': 'Solta', 'Country': 'Croatia', 'Population': 1700},
     {'Area': 68, 'City': 'Greenville', 'Country': 'USA', 'Population': 84554},
     {'Area': 4758,
      'City': 'Buenos Aires',
      'Country': 'Argentina',
      'Population': 13591863},
     {'Area': 3750,
      'City': 'Los Cabos',
      'Country': 'Mexico',
      'Population': 287651},
     {'Area': 33,
      'City': 'Walla Walla Valley',
      'Country': 'USA',
      'Population': 32237},
     {'Area': 200, 'City': 'Marakesh', 'Country': 'Morocco', 'Population': 928850},
     {'Area': 491,
      'City': 'Albuquerque',
      'Country': 'New Mexico',
      'Population': 559277},
     {'Area': 8300,
      'City': 'Archipelago Sea',
      'Country': 'Finland',
      'Population': 60000},
     {'Area': 672,
      'City': 'Iguazu Falls',
      'Country': 'Argentina',
      'Population': 0},
     {'Area': 27, 'City': 'Salina Island', 'Country': 'Italy', 'Population': 4000},
     {'Area': 2731571, 'City': 'Toronto', 'Country': 'Canada', 'Population': 630},
     {'Area': 3194,
      'City': 'Pyeongchang',
      'Country': 'South Korea',
      'Population': 2581000}]



### Visualizing our data with graphs

As we can see, in our list of cities, each city has a population number.  Our first task will be to display the populations of our first three cities in a bar chart.

First we load the plotly library into our notebook, and we initialize this offline mode.


```python
import plotly

plotly.offline.init_notebook_mode(connected=True)
# use offline mode to avoid initial registration
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


Now the next step is to build a trace.  As we know our trace is a dictionary with a key of `x` and a key of `y`.  We have set up a trace to look like the following: `trace_first_three = {'x': x_values, 'y': y_values}`.  

First define `x_values` so that it is a list of the first three cities.  Use what we learned about accessing information from lists and dictionaries to assign `x_values` equal to the first three countries.


```python
x_values = []
```

Now use list and dictionary accessors to set `y_values` equal to the first three populations.


```python
y_values = []
```


```python
x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
```

Now let's plot our data.


```python
trace_first_three_pops = {'x': x_values, 'y': y_values}


plotly.offline.iplot([trace_first_three_pops])
```


<div id="eb38eb80-5d36-476a-88b5-7a5bd42c8d1c" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("eb38eb80-5d36-476a-88b5-7a5bd42c8d1c", [{"x": ["Solta", "Greenville", "Buenos Aires"], "y": [1700, 84554, 13591863]}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Note that by default, plotly sets the type of trace as a line trace.  Let's make our trace a bar trace by setting the key of `'type'` equal to `'bar'`.  We can continue to use the lists of `x_values` and `y_values` that we defined about in our new trace.  Also, we can have the label match the names of the cities, by setting the key of `text` equal to a list of the names of the cities.  Assign a list of our first three cities to the key of `text`.


```python
bar_trace_first_three_pops = {'type': 'scatter'}
```


```python
bar_trace_first_three_pops['type'] # 'bar'
```




    'scatter'




```python
plotly.offline.iplot([bar_trace_first_three_pops])
```


<div id="6787cb3b-4b86-4781-80e7-fe692ab06582" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("6787cb3b-4b86-4781-80e7-fe692ab06582", [{"type": "scatter"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Ok, now let's plot two different traces side by side.  Create another trace called `bar_trace_first_three_areas` that has is like our `bar_trace_first_three_pops` except the values are a list of areas.  We will plot this side by side our `bar_trace_first_three_pops` in the plot below.


```python
trace_first_three_areas = {'type': 'scatter', 'x': [], 'y': [], 'text': []}
```


```python
plotly.offline.iplot([trace_first_three_pops, trace_first_three_areas])
```


<div id="dabc60c3-9383-4118-bd70-b1ee36b5e9f0" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("dabc60c3-9383-4118-bd70-b1ee36b5e9f0", [{"x": ["Solta", "Greenville", "Buenos Aires"], "y": [1700, 84554, 13591863]}, {"type": "scatter", "x": [], "y": [], "text": []}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Summary

In this section, we saw how we use data visualisations to better understand the data.  We do the following.  Import plotly:


    import plotly

    plotly.offline.init_notebook_mode(connected=True)

Then we define a trace, which is a Python dictionary.

    trace = {'x': [], 'y': [], 'text': [], 'type': 'bar'}
    
Finally, we display our trace with a call to the following method:

    plotly.offline.iplot([trace])
    
Easy peasy, quick and easy!
