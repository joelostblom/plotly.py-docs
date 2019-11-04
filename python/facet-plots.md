---
jupyter:
  jupytext:
    notebook_metadata_filter: all
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.1.1
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.7.3
  plotly:
    description: How to make Facet and Trellis Plots in Python with Plotly.
    display_as: statistical
    has_thumbnail: true
    language: python
    layout: base
    name: Facet and Trellis Plots
    order: 10.2
    page_type: u-guide
    permalink: python/facet-plots/
    redirect_from: python/trellis-plots/
    thumbnail: thumbnail/facet-trellis-thumbnail.jpg
---


### Facet and Trellis Plots

Facet plots, also known as trellis plots or small multiples, are figures made up of multiple subplots which have the same set of axes, where each subplot shows a subset of the data. While it is straightforward to use `plotly`'s 
[subplot capabilities](/python/subplots/) to make such figures, it's far easier to use the built-in `facet_row` and `facet_col` arguments in the various [Plotly Express](/python/plotly-express/) functions.

### Scatter Plot Column Facets

```python
import plotly.express as px
tips = px.data.tips()
fig = px.scatter(tips, x="total_bill", y="tip", color="smoker", facet_col="sex")
fig.show()
```

### Bar Chart Row Facets

```python
import plotly.express as px
tips = px.data.tips()
fig = px.bar(tips, x="size", y="total_bill", color="sex", facet_row="smoker")
fig.show()
```

### Wrapping Column Facets

When the facet dimension has a large number of unique values, it is possible to wrap columns using the `facet_col_wrap` argument. 

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.scatter(df, x='gdpPercap', y='lifeExp', color='continent', size='pop',
                facet_col='year', facet_col_wrap=4)
fig.show()
```

### Histogram Facet Grids

```python
import plotly.express as px
tips = px.data.tips()
fig = px.histogram(tips, x="total_bill", y="tip", color="sex", facet_row="time", facet_col="day",
       category_orders={"day": ["Thur", "Fri", "Sat", "Sun"], "time": ["Lunch", "Dinner"]})
fig.show()
```

### Facets with independent axes

By default, facet axes are linked together: zooming inside one of the facets will also zoom in the other facets. You can disable this behaviour as follows. 

```python
import plotly.express as px
df = px.data.tips()
fig = px.scatter(df, x="total_bill", y="tip", color='sex', 
                 facet_row="day", facet_col='time')
# No match between subplot axes
fig.update_xaxes(matches=None)
fig.update_yaxes(matches=None)
# Show ticks for each axis since they are now independent
fig.update_xaxes(showticklabels=True)
fig.show()
```
