---
layout: page
title: NER
description: Named Entity Recognition - Gibbon Places Function
---

```python
# redownload spaCy's small model - should see 'requirement already satisfied'
!python -m spacy download en_core_web_sm

import pandas as pd
import spacy
nlp = spacy.load('en_core_web_sm') # good idea to initialize here

import wget
import os
if not os.path.isfile('gibbon_text.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/gibbon_text.csv')
```

    Collecting en-core-web-sm==3.4.1
      Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-3.4.1/en_core_web_sm-3.4.1-py3-none-any.whl (12.8 MB)
    [K     |████████████████████████████████| 12.8 MB 354 kB/s eta 0:00:01
    [?25hRequirement already satisfied: spacy<3.5.0,>=3.4.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from en-core-web-sm==3.4.1) (3.4.2)
    Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.8)
    Requirement already satisfied: typer<0.5.0,>=0.3.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.4.2)
    Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.8)
    Requirement already satisfied: requests<3.0.0,>=2.13.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.27.1)
    Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (4.64.0)
    Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.7)
    Requirement already satisfied: thinc<8.2.0,>=8.1.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (8.1.5)
    Requirement already satisfied: packaging>=20.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (21.3)
    Requirement already satisfied: srsly<3.0.0,>=2.4.3 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.4.5)
    Requirement already satisfied: jinja2 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.11.3)
    Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.0.9)
    Requirement already satisfied: pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.10.2)
    Requirement already satisfied: numpy>=1.15.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.21.5)
    Requirement already satisfied: pathy>=0.3.5 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.6.2)
    Requirement already satisfied: setuptools in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (61.2.0)
    Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.0.3)
    Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.3.0)
    Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.10 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.10)
    Requirement already satisfied: wasabi<1.1.0,>=0.9.1 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.10.1)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from packaging>=20.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.4)
    Requirement already satisfied: smart-open<6.0.0,>=5.2.1 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from pathy>=0.3.5->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (5.2.1)
    Requirement already satisfied: typing-extensions>=4.1.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (4.1.1)
    Requirement already satisfied: idna<4,>=2.5 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2021.10.8)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.26.9)
    Requirement already satisfied: confection<1.0.0,>=0.0.1 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.0.3)
    Requirement already satisfied: blis<0.8.0,>=0.7.8 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.7.9)
    Requirement already satisfied: click<9.0.0,>=7.1.1 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from typer<0.5.0,>=0.3.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (8.0.4)
    Requirement already satisfied: MarkupSafe>=0.23 in /Users/gillislinde/opt/anaconda3/lib/python3.9/site-packages (from jinja2->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.1)
    [38;5;2m✔ Download and installation successful[0m
    You can now load the package via spacy.load('en_core_web_sm')



```python
def find_places(chapter):
    
    gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})
    gibbon_by_chapter

    first_chapter = gibbon_by_chapter['StringText'][chapter]

    # pass the first chapter into spaCy parser
    first_chapter_doc = nlp(first_chapter)

    # putting all of the data into a dictionary
    import collections
    place_freq = collections.defaultdict(int)
    for entity in first_chapter_doc.ents:
        if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
            place_freq[entity.text] += 1 # the utility of defaultdict!
    place_freq = dict(place_freq)

    # dict -> df
    place_freq_df = pd.DataFrame.from_dict(place_freq, orient='index').reset_index().rename(columns={'index':'place_name',0:'frequency'})

    # downloading the Pleiades data we need (also from my gh)
    if not os.path.isfile('places.csv'):
        wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/places.csv')
    if not os.path.isfile('names.csv'):
        wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/names.csv')

    places = pd.read_csv('places.csv')
    names = pd.read_csv('names.csv')

    def get_pleiades_id(term):
        """
        Iterates through all of the possible names in the names.csv file
        Returns None if no matched names
        """
        name_row = names.loc[names['attested_form'] == term]
        if len(name_row) == 1:
            return int(name_row.place_id.iloc[0])
        else:
            name_row = names.loc[names['romanized_form_1'] == term]
            if len(name_row) == 1:
                return int(name_row.place_id.iloc[0])
            else:
                name_row = names.loc[names['romanized_form_2'] == term]
                if len(name_row) == 1:
                    return int(name_row.place_id.iloc[0])
                else:
                    name_row = names.loc[names['romanized_form_3'] == term]
                    if len(name_row) == 1:
                        return int(name_row.place_id.iloc[0])
                    else:
                        return None

    place_freq_df['pleiades_id'] = place_freq_df['place_name'].apply(get_pleiades_id)

    place_freq_final = place_freq_df.dropna().reset_index(drop=True)

    rid = place_freq_final.pleiades_id.iloc[0]
    places.loc[places['id'] == rid]

    # could've just one function here, but not too much trouble to do two
    def get_lat(pl_id):
        places_row = places.loc[places['id'] == pl_id]
        if len(places_row) == 1:
            return places_row.representative_latitude.iloc[0]

    def get_long(pl_id):
        places_row = places.loc[places['id'] == pl_id]
        if len(places_row) == 1:
            return places_row.representative_longitude.iloc[0]

    place_freq_final['lat'] = place_freq_final['pleiades_id'].apply(get_lat)
    place_freq_final['long'] = place_freq_final['pleiades_id'].apply(get_long)

    return place_freq_final
```


```python
find_places(0)
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
      <th>place_name</th>
      <th>frequency</th>
      <th>pleiades_id</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rome</td>
      <td>12</td>
      <td>423025.0</td>
      <td>41.891775</td>
      <td>12.486137</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Euphrates</td>
      <td>6</td>
      <td>912849.0</td>
      <td>35.543310</td>
      <td>39.606018</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arabia</td>
      <td>2</td>
      <td>981506.0</td>
      <td>27.500000</td>
      <td>32.500000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Africa</td>
      <td>7</td>
      <td>775.0</td>
      <td>32.500000</td>
      <td>7.500000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ireland</td>
      <td>1</td>
      <td>20487.0</td>
      <td>53.184028</td>
      <td>-7.717526</td>
    </tr>
    <tr>
      <th>5</th>
      <td>India</td>
      <td>1</td>
      <td>50004.0</td>
      <td>22.500000</td>
      <td>77.500000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Iberia</td>
      <td>1</td>
      <td>863807.0</td>
      <td>41.836468</td>
      <td>44.689138</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Caledonia</td>
      <td>1</td>
      <td>89132.0</td>
      <td>57.500000</td>
      <td>-4.500000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Misenum</td>
      <td>2</td>
      <td>432941.0</td>
      <td>40.786279</td>
      <td>14.084884</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Naples</td>
      <td>3</td>
      <td>433014.0</td>
      <td>40.839995</td>
      <td>14.252870</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Tarragona</td>
      <td>1</td>
      <td>246349.0</td>
      <td>41.116892</td>
      <td>1.258338</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Lugdunum</td>
      <td>1</td>
      <td>167717.0</td>
      <td>45.758866</td>
      <td>4.819482</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Hercules</td>
      <td>2</td>
      <td>266032.0</td>
      <td>37.500000</td>
      <td>-0.500000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Illyricum</td>
      <td>2</td>
      <td>481865.0</td>
      <td>42.427292</td>
      <td>17.965028</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Macedonia</td>
      <td>3</td>
      <td>491656.0</td>
      <td>41.250000</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Augsburg</td>
      <td>1</td>
      <td>118580.0</td>
      <td>48.365463</td>
      <td>10.894765</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Thebes</td>
      <td>1</td>
      <td>541138.0</td>
      <td>38.319156</td>
      <td>23.317577</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Argos</td>
      <td>1</td>
      <td>570106.0</td>
      <td>37.631561</td>
      <td>22.719464</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Sparta</td>
      <td>1</td>
      <td>570685.0</td>
      <td>37.077905</td>
      <td>22.427298</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Athens</td>
      <td>1</td>
      <td>579885.0</td>
      <td>37.972634</td>
      <td>23.722746</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Achaia</td>
      <td>1</td>
      <td>570028.0</td>
      <td>38.102121</td>
      <td>22.224586</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Troy</td>
      <td>1</td>
      <td>550595.0</td>
      <td>39.957433</td>
      <td>26.238459</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Ionia</td>
      <td>1</td>
      <td>550597.0</td>
      <td>38.162194</td>
      <td>27.357498</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Constantinople</td>
      <td>1</td>
      <td>520998.0</td>
      <td>41.006371</td>
      <td>28.965352</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Trebizond</td>
      <td>2</td>
      <td>857359.0</td>
      <td>41.004269</td>
      <td>39.723312</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Nile</td>
      <td>1</td>
      <td>727172.0</td>
      <td>19.211409</td>
      <td>30.567330</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Algiers</td>
      <td>1</td>
      <td>295276.0</td>
      <td>36.768912</td>
      <td>3.053218</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Sardinia</td>
      <td>1</td>
      <td>472014.0</td>
      <td>39.871087</td>
      <td>8.957517</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Sicily</td>
      <td>1</td>
      <td>462492.0</td>
      <td>37.643297</td>
      <td>13.932018</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Malta</td>
      <td>1</td>
      <td>462311.0</td>
      <td>35.908887</td>
      <td>14.408042</td>
    </tr>
  </tbody>
</table>
</div>




```python
find_places(1)
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
      <th>place_name</th>
      <th>frequency</th>
      <th>pleiades_id</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rome</td>
      <td>32</td>
      <td>423025.0</td>
      <td>41.891775</td>
      <td>12.486137</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nile</td>
      <td>4</td>
      <td>727172.0</td>
      <td>19.211409</td>
      <td>30.567330</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Athens</td>
      <td>11</td>
      <td>579885.0</td>
      <td>37.972634</td>
      <td>23.722746</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sparta</td>
      <td>1</td>
      <td>570685.0</td>
      <td>37.077905</td>
      <td>22.427298</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Padua</td>
      <td>2</td>
      <td>393473.0</td>
      <td>45.409561</td>
      <td>11.876975</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arpinum</td>
      <td>1</td>
      <td>432700.0</td>
      <td>41.648422</td>
      <td>13.609876</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Etruria</td>
      <td>1</td>
      <td>413122.0</td>
      <td>42.758127</td>
      <td>11.546721</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Latium</td>
      <td>2</td>
      <td>432900.0</td>
      <td>41.590543</td>
      <td>13.192265</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Alesia</td>
      <td>1</td>
      <td>177434.0</td>
      <td>47.536622</td>
      <td>4.503884</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Africa</td>
      <td>4</td>
      <td>775.0</td>
      <td>32.500000</td>
      <td>7.500000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Euphrates</td>
      <td>1</td>
      <td>912849.0</td>
      <td>35.543310</td>
      <td>39.606018</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Capua</td>
      <td>1</td>
      <td>432754.0</td>
      <td>41.086092</td>
      <td>14.250207</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Verona</td>
      <td>2</td>
      <td>383816.0</td>
      <td>45.442130</td>
      <td>10.995736</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Troas</td>
      <td>1</td>
      <td>550944.0</td>
      <td>39.837052</td>
      <td>26.336944</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Milan</td>
      <td>1</td>
      <td>383706.0</td>
      <td>45.463746</td>
      <td>9.188060</td>
    </tr>
    <tr>
      <th>15</th>
      <td>London</td>
      <td>1</td>
      <td>79574.0</td>
      <td>51.513335</td>
      <td>-0.088949</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Paris</td>
      <td>1</td>
      <td>109126.0</td>
      <td>48.854405</td>
      <td>2.346168</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Arles</td>
      <td>1</td>
      <td>148217.0</td>
      <td>43.677616</td>
      <td>4.630799</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bordeaux</td>
      <td>1</td>
      <td>138248.0</td>
      <td>44.837205</td>
      <td>-0.576533</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Autun</td>
      <td>1</td>
      <td>177460.0</td>
      <td>46.947240</td>
      <td>4.299177</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Vienne</td>
      <td>1</td>
      <td>167719.0</td>
      <td>45.524510</td>
      <td>4.875982</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Hercules</td>
      <td>1</td>
      <td>266032.0</td>
      <td>37.500000</td>
      <td>-0.500000</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Sicily</td>
      <td>1</td>
      <td>462492.0</td>
      <td>37.643297</td>
      <td>13.932018</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Media</td>
      <td>1</td>
      <td>903080.0</td>
      <td>34.500000</td>
      <td>46.500000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Arabia</td>
      <td>2</td>
      <td>981506.0</td>
      <td>27.500000</td>
      <td>32.500000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>India</td>
      <td>2</td>
      <td>50004.0</td>
      <td>22.500000</td>
      <td>77.500000</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
