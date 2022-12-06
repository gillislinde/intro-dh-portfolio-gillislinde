---
layout: page
title: Visualizing Data with Bokeh and Pandas
description: In this lesson you will learn how to visualy explore and present data in Python by using the Bokeh and Pandas libraries.
---

## Source

https://programminghistorian.org/en/lessons/visualizing-with-bokeh

# The Basics of Bokeh

## Your First PLot


```python
from bokeh.plotting import figure, output_notebook, show
from bokeh.models.tools import LassoSelectTool, CrosshairTool, HoverTool
output_notebook()

x = [1, 3, 5, 7]
y = [2, 4, 6, 8]

p = figure()

p.circle(x, y, size=10, color='red', legend='circle')
p.line(x, y, color='blue', legend='line')
p.triangle(y, x, color='yellow', size=10, legend='triangle')

p.legend.click_policy='hide'

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1383">Loading BokehJS ...</span>
</div>




    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="3e9fba8d-3083-4432-8cb2-ebaf16622ab7" data-root-id="1384"></div>





# Bokeh and Pandas: Exploring the WWII THOR Dataset

## Loading Data in Pandas


```python
#loading_data.py
import pandas as pd

df = pd.read_csv('thor_wwii.csv')
print(df)
```

               MSNDATE      THEATER COUNTRY_FLYING_MISSION    NAF   UNIT_ID  \
    0       03/30/1941          ETO          GREAT BRITAIN    RAF   84 SQDN   
    1       11/24/1940          ETO          GREAT BRITAIN    RAF  211 SQDN   
    2       12/04/1940          ETO          GREAT BRITAIN    RAF  211 SQDN   
    3       12/31/1940          ETO          GREAT BRITAIN    RAF  211 SQDN   
    4       01/06/1941          ETO          GREAT BRITAIN    RAF  211 SQDN   
    ...            ...          ...                    ...    ...       ...   
    178276  08/01/1945          PTO                    USA  20 AF     73 BW   
    178277  07/22/1942          MTO          GREAT BRITAIN    RAF       NaN   
    178278  08/17/1940  EAST AFRICA          GREAT BRITAIN    RAF   47 SQDN   
    178279  08/06/1945          PTO                    USA  20 AF    509 CG   
    178280  08/09/1945          PTO                    USA  20 AF    509 CG   
    
           AIRCRAFT_NAME  AC_ATTACKING TAKEOFF_BASE TAKEOFF_COUNTRY  \
    0           BLENHEIM          10.0          NaN             NaN   
    1           BLENHEIM           9.0          NaN             NaN   
    2           BLENHEIM           9.0          NaN             NaN   
    3           BLENHEIM           9.0          NaN             NaN   
    4           BLENHEIM           9.0          NaN             NaN   
    ...              ...           ...          ...             ...   
    178276           B29          99.0          NaN             NaN   
    178277      BLENHEIM           NaN          NaN             NaN   
    178278     WELLESLEY           6.0      ERKOWIT           SUDAN   
    178279           B29           1.0          NaN             NaN   
    178280           B29           1.0          NaN             NaN   
    
            TAKEOFF_LATITUDE  TAKEOFF_LONGITUDE TGT_COUNTRY  TGT_LOCATION  \
    0                    NaN                NaN     ALBANIA       ELBASAN   
    1                    NaN                NaN     ALBANIA       DURAZZO   
    2                    NaN                NaN     ALBANIA      TEPELENE   
    3                    NaN                NaN     ALBANIA        VALONA   
    4                    NaN                NaN     ALBANIA        VALONA   
    ...                  ...                ...         ...           ...   
    178276               NaN                NaN       JAPAN        TOYAMA   
    178277               NaN                NaN       EGYPT  MERSA MATRUH   
    178278             18.75               37.0       SUDAN       KASSALA   
    178279               NaN                NaN       JAPAN     HIROSHIMA   
    178280               NaN                NaN       JAPAN      NAGASAKI   
    
            TGT_LATITUDE  TGT_LONGITUDE  TONS_HE  TONS_IC  TONS_FRAG  TOTAL_TONS  
    0          41.100000      20.070000      0.0      0.0        0.0         0.0  
    1          41.320000      19.450000      0.0      0.0        0.0         0.0  
    2          40.300000      20.020000      0.0      0.0        0.0         0.0  
    3          40.470000      19.490000      0.0      0.0        0.0         0.0  
    4          40.470000      19.490000      0.0      0.0        0.0         0.0  
    ...              ...            ...      ...      ...        ...         ...  
    178276     36.700000     137.216667      0.0    999.0        0.0       999.0  
    178277     31.330000      27.200000      0.0      0.0        0.0      1300.0  
    178278     15.450000      36.400000   4750.0      0.0        0.0      4750.0  
    178279     34.400000     132.466667  15000.0      0.0        0.0     15000.0  
    178280     32.733333     129.866667  20000.0      0.0        0.0     20000.0  
    
    [178281 rows x 19 columns]



```python
df.columns.tolist()
```




    ['MSNDATE',
     'THEATER',
     'COUNTRY_FLYING_MISSION',
     'NAF',
     'UNIT_ID',
     'AIRCRAFT_NAME',
     'AC_ATTACKING',
     'TAKEOFF_BASE',
     'TAKEOFF_COUNTRY',
     'TAKEOFF_LATITUDE',
     'TAKEOFF_LONGITUDE',
     'TGT_COUNTRY',
     'TGT_LOCATION',
     'TGT_LATITUDE',
     'TGT_LONGITUDE',
     'TONS_HE',
     'TONS_IC',
     'TONS_FRAG',
     'TOTAL_TONS']



## The Bokeh ColumnDataSource


```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool
output_notebook()

df = pd.read_csv('thor_wwii.csv')

sample = df.sample(50)
source = ColumnDataSource(sample)

p = figure()
p.circle(x='TOTAL_TONS', y='AC_ATTACKING', 
         source=source, 
         size=10, color='green')

p.title.text = 'Attacking Aircraft and Munitions Dropped'
p.xaxis.axis_label = 'Tons of Munitions Dropped'
p.yaxis.axis_label = 'Number of Attacking Aircraft'

hover = HoverTool()
hover.tooltips=[
    ('Attack Date', '@MSNDATE'),
    ('Attacking Aircraft', '@AC_ATTACKING'),
    ('Tons of Munitions', '@TOTAL_TONS'),
    ('Type of Aircraft', '@AIRCRAFT_NAME')
]

p.add_tools(hover)

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1597">Loading BokehJS ...</span>
</div>











<div class="bk-root" id="4edef6b8-3b43-4188-a995-5ed5b6759786" data-root-id="1599"></div>





# Categorical Data and Bar Charts: Munitions Dropped by Country


```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool

from bokeh.palettes import Spectral5
from bokeh.transform import factor_cmap
output_notebook()

df = pd.read_csv('thor_wwii.csv')

grouped = df.groupby('COUNTRY_FLYING_MISSION')['TOTAL_TONS', 'TONS_HE', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped / 1000

source = ColumnDataSource(grouped)
countries = source.data['COUNTRY_FLYING_MISSION'].tolist()
p = figure(x_range=countries)

color_map = factor_cmap(field_name='COUNTRY_FLYING_MISSION', 
                    palette=Spectral5, factors=countries)

p.vbar(x='COUNTRY_FLYING_MISSION', top='TOTAL_TONS', source=source, width=0.70, color=color_map)

p.title.text ='Munitions Dropped by Allied Country'
p.xaxis.axis_label = 'Country'
p.yaxis.axis_label = 'Kilotons of Munitions'

hover = HoverTool()
hover.tooltips = [
    ("Totals", "@TONS_HE High Explosive / @TONS_IC Incendiary / @TONS_FRAG 	Fragmentation")]

hover.mode = 'vline'

p.add_tools(hover)

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1750">Loading BokehJS ...</span>
</div>




    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/2481473550.py:12: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby('COUNTRY_FLYING_MISSION')['TOTAL_TONS', 'TONS_HE', 'TONS_IC', 'TONS_FRAG'].sum()









<div class="bk-root" id="20353379-5c01-4dfc-8431-25a359f5c2aa" data-root-id="1752"></div>





# Stacked bar Charts and Sub-Sampling Data: Types of Muntitions Dropped by Country


```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3
output_notebook()

df = pd.read_csv('thor_wwii.csv')

filter = df['COUNTRY_FLYING_MISSION'].isin(('USA','GREAT BRITAIN'))
df = df[filter]

grouped = df.groupby('COUNTRY_FLYING_MISSION')['TONS_IC', 'TONS_FRAG', 'TONS_HE'].sum()
grouped = grouped / 1000

source = ColumnDataSource(grouped)
countries = source.data['COUNTRY_FLYING_MISSION'].tolist()
p = figure(x_range=countries)

p.vbar_stack(stackers=['TONS_HE', 'TONS_FRAG', 'TONS_IC'], 
             x='COUNTRY_FLYING_MISSION', source=source, 
             legend = ['High Explosive', 'Fragmentation', 'Incendiary'],
             width=0.5, color=Spectral3)

p.title.text ='Types of Munitions Dropped by Allied Country'
p.legend.location = 'top_left'

p.xaxis.axis_label = 'Country'
p.xgrid.grid_line_color = None	#remove the x grid lines

p.yaxis.axis_label = 'Kilotons of Munitions'

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1914">Loading BokehJS ...</span>
</div>




    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/3729838741.py:12: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby('COUNTRY_FLYING_MISSION')['TONS_IC', 'TONS_FRAG', 'TONS_HE'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="5bc05338-08f5-4a67-9524-520e9d27f573" data-root-id="1916"></div>





# Time-Series, Annotations, and Multiple Plots: Bombing Operations over Time


```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3
output_notebook()

df = pd.read_csv('thor_wwii.csv')

#make sure MSNDATE is a datetime format
df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')

grouped = df.groupby('MSNDATE')['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type='datetime')

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="2141">Loading BokehJS ...</span>
</div>




    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/2320859557.py:12: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby('MSNDATE')['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="b8cf9ab5-af6e-40f2-8ae2-22a87b499bab" data-root-id="2143"></div>





## Resampling Time-Series Data


```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3
output_notebook()

df = pd.read_csv('thor_wwii.csv')

#make sure MSNDATE is a datetime format
df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')

grouped = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type='datetime')

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="2481">Loading BokehJS ...</span>
</div>




    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/888983062.py:12: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="72b05487-7688-44b6-b28e-28d18d2abe33" data-root-id="2483"></div>





## Annotating Trends in Plots


```python
import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from datetime import datetime
from bokeh.palettes import Spectral3
output_file('eto_operations.html')

df = pd.read_csv('thor_wwii.csv')

#filter for the European Theater of Operations
filter = df['THEATER']=='ETO'
df = df[filter]

df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')
group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
group = group / 1000

source = ColumnDataSource(group)

p = figure(x_axis_type="datetime")

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.title.text = 'European Theater of Operations'

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)
```

    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/103407780.py:15: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="d2f56db3-95a5-487c-a084-621795652e54" data-root-id="2845"></div>






```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource
from bokeh.models import BoxAnnotation, Label
from datetime import datetime
from bokeh.palettes import Spectral3
output_notebook()

df = pd.read_csv('thor_wwii.csv')

#filter for the European Theater of Operations
filter = df['THEATER']=='ETO'
df = df[filter]

df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')
group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
group = group / 1000

source = ColumnDataSource(group)

p = figure(x_axis_type="datetime")

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.title.text = 'European Theater of Operations'

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

box_left = pd.to_datetime('6-6-1944')
box_right = pd.to_datetime('16-12-1944')

box = BoxAnnotation(left=box_left, right=box_right,
                    line_width=1, line_color='black', line_dash='dashed',
                    fill_alpha=0.2, fill_color='orange')

p.add_layout(box)
show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="3553">Loading BokehJS ...</span>
</div>




    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/2689645321.py:16: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    /var/folders/14/mcqlhbk97px82zc8dmhdc86m0000gn/T/ipykernel_47566/2689645321.py:32: UserWarning: Parsing '16-12-1944' in DD/MM/YYYY format. Provide format or specify infer_datetime_format=True for consistent parsing.
      box_right = pd.to_datetime('16-12-1944')









<div class="bk-root" id="1eab83a8-e12f-473b-a7fd-1f4f781a09ec" data-root-id="3555"></div>





# Spatial Data: Mapping Target Locations


```python
import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource, Range1d
from bokeh.layouts import layout
from bokeh.palettes import Spectral3
from bokeh.tile_providers import CARTODBPOSITRON
from pyproj import Proj, transform
from bokeh.models.tools import HoverTool

def LongLat_to_EN(long, lat):
    try:
      easting, northing = transform(
        Proj(init='epsg:4326'), Proj(init='epsg:3857'), long, lat)
      return easting, northing
    except:
      return None, None

df = pd.read_csv('thor_wwii.csv')
#convert all lat/long to webmercator and store in new column
df['E'], df['N'] = zip(*df.apply(lambda x: LongLat_to_EN(x['TGT_LONGITUDE'], x['TGT_LATITUDE']), axis=1))

grouped = df.groupby(['E', 'N'])['TONS_FRAG', 'TONS_IC'].sum().reset_index()

filter = grouped['TONS_FRAG']!=0
grouped = grouped[filter]

source = ColumnDataSource(grouped)

left = -2150000
right = 18000000
bottom = -5300000
top = 11000000

p = figure(x_range=Range1d(left, right), y_range=Range1d(bottom, top))
p.add_tile(CARTODBPOSITRON)

p.circle(x='E', y='N', source=source, line_color='grey', fill_color=Spectral3[1])

p.axis.visible = False

hover = HoverTool(tooltips=[
    ("Fragmentation Bombs", "@TONS_FRAG tons")
])

p.add_tools(hover)


output_notebook()
show(p)
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Input In [21], in <cell line: 7>()
          5 from bokeh.palettes import Spectral3
          6 from bokeh.tile_providers import CARTODBPOSITRON
    ----> 7 from pyproj import Proj, transform
          8 from bokeh.models.tools import HoverTool
         10 def LongLat_to_EN(long, lat):


    ModuleNotFoundError: No module named 'pyproj'



```python

```
