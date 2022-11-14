---
layout: page
title: APIs
description: Chronicling America
---

# Chronicling America API Assignment
In this assignment, you are tasked with:
* searching Chronicling America's API for a key word of your choice
* parsing your results from a dictionary to a `DataFrame` with headings "title", "city", 'date", and "raw_text"
* processing the raw text by removing "\n" characters, stopwords, and then lemmatizing the raw text before adding it to a new column called "lemmas."
* saving your `DataFrame` to a csv file

If you need any help with this assignment please email micah.saxton@tufts.edu



```python
# imports
import requests
import json
import math
import pandas as pd
import spacy
```


```python
# initial search
url = 'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1=1939&date2=1963&proxtext=atomic+bomb&x=16&y=8&dateFilterType=yearRange&rows=20&searchType=basic&format=json'
response = requests.get(url)  # returns a 'object' representing the webpage
raw = response.text  # the text attribute contains the text from the web page as a string
results = json.loads(raw)  # the loads method from the json library transforms the string into a dict
```


```python
results.keys()
```




    dict_keys(['totalItems', 'endIndex', 'startIndex', 'itemsPerPage', 'items'])




```python
# find total amount of pages
total_pages = math.ceil(results['totalItems'] / results['itemsPerPage'])
total_pages
```




    1127




```python
# query the api and save to dict 
data = []
start_date = '1939'
end_date = '1963'
search_term = 'atomic+bomb'
for i in range(1, 50): 
    url = (f'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1={start_date}'
           f'&date2={end_date}&proxtext={search_term}&x=16&y=8&dateFilterType=yearRange&rows=20'
           f'&searchType=basic&format=json&page={i}') 
    response = requests.get(url)
    raw = response.text
    print(i, response.status_code)  # Micah added i to check how many ran succesfully
    results = json.loads(raw)
    items_ = results['items']
    for item_ in items_:
        temp_dict = {}
        temp_dict['title'] = item_['title_normal']
        temp_dict['city'] = item_['city']
        temp_dict['date'] = item_['date']
        temp_dict['raw_text'] = item_['ocr_eng']
        data.append(temp_dict)
```

    1 200
    2 200
    3 200
    4 200
    5 200
    6 200
    7 200
    8 200
    9 200
    10 200
    11 200
    12 200
    13 200
    14 200
    15 200
    16 200
    17 200
    18 200
    19 200
    20 200
    21 200
    22 200
    23 200
    24 200
    25 200
    26 200
    27 200
    28 200
    29 200
    30 200
    31 200
    32 200
    33 200
    34 200
    35 200
    36 200
    37 200
    38 200
    39 200
    40 200
    41 200
    42 200
    43 200
    44 200
    45 200
    46 200
    47 200
    48 200
    49 200



```python
# convert dict to dataframe
df = pd.DataFrame.from_dict(data)
```


```python
#santiy check
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>city</th>
      <th>date</th>
      <th>raw_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>19450902</td>
      <td>ft Took Only Two Atomic Bombs to Cause All Thi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>kodiak mirror.</td>
      <td>[Kodiak]</td>
      <td>19450818</td>
      <td>Lert k\nClouds of smoke at the fs«|\nthe tower...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>19630324</td>
      <td>K E ? UMfffcfc 1 -\nl\nO&gt; aHV;\n+ b\n9 M\naHßt...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>detroit evening times.</td>
      <td>[Detroit]</td>
      <td>19450916</td>
      <td>■» ■ - - -\n1 ‘‘ f\nW| \ Jrk i\n-&gt; ... . « .;....</td>
    </tr>
    <tr>
      <th>4</th>
      <td>detroit evening times.</td>
      <td>[Detroit]</td>
      <td>19450819</td>
      <td>( \i ' *y» Yjg*. aXMA l&gt; \ T -"** a **^r :: y ...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# convert date column from string to date-time object
df['date'] = pd.to_datetime(df['date'])
```


```python
# sort by date
sorted_df = df.sort_values(by='date')
```


```python
# sanity check
sorted_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>city</th>
      <th>date</th>
      <th>raw_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>109</th>
      <td>scandinavian american.</td>
      <td>[Seattle]</td>
      <td>1945-08-01</td>
      <td>8\nEDITOBIAL PAGES of the\nScandinavians Helpe...</td>
    </tr>
    <tr>
      <th>158</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1945-08-06</td>
      <td>Weather Forecast\nShowers, thunderstorms, humi...</td>
    </tr>
    <tr>
      <th>680</th>
      <td>daily alaska empire.</td>
      <td>[Juneau]</td>
      <td>1945-08-06</td>
      <td>THE DAILY ALASKA\n“ALL THE HEWS All THE TIME"\...</td>
    </tr>
    <tr>
      <th>152</th>
      <td>nome nugget.</td>
      <td>[Nome]</td>
      <td>1945-08-06</td>
      <td>Atomic War\nOn Japs {\n(Continued from Page On...</td>
    </tr>
    <tr>
      <th>823</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1945-08-06</td>
      <td>Provisional Assembly\nDissolved by France\nAft...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# write fuction to process text
nlp = spacy.load("en_core_web_sm")
nlp.disable_pipes('ner', 'parser')  

def process_text(text):
    """Remove new line characters and lemmatize text. Returns string of lemmas"""
    text = text.replace('\n', ' ')
    doc = nlp(text)
    tokens = [token for token in doc]
    no_stops = [token for token in tokens if not token.is_stop]
    no_punct = [token for token in no_stops if token.is_alpha]
    lemmas = [token.lemma_ for token in no_punct]
    lemmas_lower = [lemma.lower() for lemma in lemmas]
    lemmas_string = ' '.join(lemmas_lower)
    return lemmas_string
```


```python
# apply process_text function to raw_text column
sorted_df['lemmas'] = sorted_df['raw_text'].apply(process_text)
```


```python
# sanity check
sorted_df.head()
```


```python
# save to csv
sorted_df.to_csv(f'../data/{search_term}{start_date}-{end_date}.csv', index=False)
```


```python

```
