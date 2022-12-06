---
layout: page
title: Understanding and Using Common Similarity Measures for Text Analysis
description: This lesson introduces three common measures for determining how similar texts are to one another. You will learn the general principles behind similarity, the different advantages of these measures, and how to calculate each of them using the SciPy Python library.
---
## Source

https://programminghistorian.org/en/lessons/common-similarity-measures#samples-and-features

## Reflection

While I’d heard about all three of the common distance/similarity metrics before, I had never learned about their application/usefulness in terms of comparing documents. It was interesting, however, to hear the comparisons in the distance measures and more importantly how to choose which one. For example, it would be a good idea to use cosine distance instead of Euclidean or city block if the documents you were comparing had different lengths (unless you used something like TF-IDF to account for the different lengths beforehand), as cosine doesn’t account for magnitude. Otherwise, I learned how to use python to count words in documents, calculate their distance using SciPy, and analyze the results. 

I was especially interested in this lesson as it has applications to my final project where I am comparing the albums of Kendrick Lamar and how they change overtime. I could use these similarity metrics to compare individual songs to see if songs on his albums are most similar to other songs on the same album or not. I could also simply compile all the songs on an album into one document and compare albums. I will likely run into the magnitude issue so either I find a way to resolve this with FT-IDF or keep that in mind when I get my results and weigh cosine distance more. 

# Counting Words


```python
import glob
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer
from scipy.spatial.distance import pdist, squareform
```


```python
# Use the glob library to create a list of file names
filenames = glob.glob("1666_texts/*.txt")
# Parse those filenames to create a list of file keys (ID numbers)
# You'll use these later on.
filekeys = [f.split('/')[-1].split('.')[0] for f in filenames]

# Create a CountVectorizer instance with the parameters you need
vectorizer = CountVectorizer(input="filename", max_features=1000, max_df=0.7)
# Run the vectorizer on your list of filenames to create your wordcounts
# Use the toarray() function so that SciPy will accept the results
wordcounts = vectorizer.fit_transform(filenames).toarray()
```


```python
metadata = pd.read_csv("1666_metadata.csv", index_col="TCP ID")
```

## Calculating Distance using SciPy


```python
euclidean_distances = pd.DataFrame(squareform(pdist(wordcounts)), index=filekeys, columns=filekeys)
print(euclidean_distances)
```

                 A32566      A26249       A42533       A67572       A32567  \
    A32566     0.000000  284.950873    23.302360   209.864242    13.379088   
    A26249   284.950873    0.000000   276.495931   300.502912   283.933091   
    A42533    23.302360  276.495931     0.000000   204.230262    24.413111   
    A67572   209.864242  300.502912   204.230262     0.000000   209.055017   
    A32567    13.379088  283.933091    24.413111   209.055017     0.000000   
    ...             ...         ...          ...          ...          ...   
    A61867   266.364412  286.421019   263.034218   283.441352   264.210144   
    A30143  1031.073712  994.075450  1027.509611   991.204318  1030.196098   
    A32557    12.845233  283.774558    23.748684   209.389589    14.899664   
    A29017  1086.572593  984.628356  1082.784836  1054.043168  1085.198139   
    A52328   469.846784  466.558678   467.261169   471.494433   469.326113   
    
                A62436       A95690       A91186       A65985      A56381  ...  \
    A32566  356.175519    16.970563  5942.067401   282.757847  391.619713  ...   
    A26249  322.567822   284.733208  5908.028605   293.634126  364.780756  ...   
    A42533  352.122138    26.664583  5940.656024   275.519509  389.529203  ...   
    A67572  343.840079   210.492280  5924.383512   212.011792  382.764941  ...   
    A32567  354.688596    18.894444  5941.815884   281.824413  390.219169  ...   
    ...            ...          ...          ...          ...         ...  ...   
    A61867  302.530990   266.435733  5898.857771   303.186411  325.671614  ...   
    A30143  856.829038  1030.962172  5915.931203   929.963978  972.467480  ...   
    A32557  355.170382    18.248288  5941.425587   282.086866  390.790225  ...   
    A29017  875.886408  1086.551425  5920.496854  1038.559579  947.643393  ...   
    A52328  481.143430   470.561367  5774.891601   486.125498  468.401537  ...   
    
                 A26482       B05591       A47095       B03109       A32581  \
    A32566   773.668534    21.095023   382.864206    21.023796    16.217275   
    A26249   703.182764   284.042250   402.042286   280.967970   283.453700   
    A42533   769.558315    29.427878   376.188782    23.558438    25.219040   
    A67572   748.026737   210.299786   293.758404   208.813314   209.155445   
    A32567   771.672210    22.449944   382.429078    22.561028    16.370706   
    ...             ...          ...          ...          ...          ...   
    A61867   675.700377   265.697196   387.629978   263.840861   263.216641   
    A30143  1088.470487  1030.742451   855.693870  1029.378939  1030.166006   
    A32557   772.415691    21.213203   382.713992    22.068076    16.000000   
    A29017  1093.083254  1086.347550  1058.802626  1083.605094  1084.704107   
    A52328   781.967391   468.703531   550.082721   468.926433   468.071576   
    
                A61867       A30143       A32557       A29017       A52328  
    A32566  266.364412  1031.073712    12.845233  1086.572593   469.846784  
    A26249  286.421019   994.075450   283.774558   984.628356   466.558678  
    A42533  263.034218  1027.509611    23.748684  1082.784836   467.261169  
    A67572  283.441352   991.204318   209.389589  1054.043168   471.494433  
    A32567  264.210144  1030.196098    14.899664  1085.198139   469.326113  
    ...            ...          ...          ...          ...          ...  
    A61867    0.000000   970.593118   265.177299   992.918929   430.620483  
    A30143  970.593118     0.000000  1030.226189  1213.581888  1045.490794  
    A32557  265.177299  1030.226189     0.000000  1085.642206   469.628577  
    A29017  992.918929  1213.581888  1085.642206     0.000000  1033.236662  
    A52328  430.620483  1045.490794   469.628577  1033.236662     0.000000  
    
    [142 rows x 142 columns]



```python
top5_euclidean = euclidean_distances.nsmallest(6, 'A28989')['A28989'][1:]
print(top5_euclidean)
```

    A62436     988.557029
    A43020     988.622274
    A29017    1000.024000
    A56390    1005.630151
    A44061    1012.873141
    Name: A28989, dtype: float64



```python
print(metadata.loc[top5_euclidean.index, ['Author','Title','Keywords']])
```

                                   Author  \
    A62436    Thomson, George, 17th cent.   
    A43020    Harvey, Gideon, 1640?-1700?   
    A29017      Boyle, Robert, 1627-1691.   
    A56390     Parker, Samuel, 1640-1688.   
    A44061  Hodges, Nathaniel, 1629-1688.   
    
                                                        Title  \
    A62436  Loimotomia, or, The pest anatomized in these f...   
    A43020  Morbus anglicus: or, The anatomy of consumptio...   
    A29017  The origine of formes and qualities, (accordin...   
    A56390  A free and impartial censure of the Platonick ...   
    A44061  Vindiciæ medicinæ & medicorum: or An apology f...   
    
                                                     Keywords  
    A62436  Hodges, Nathaniel, 1629-1688. -- Vindiciae med...  
    A43020               Tuberculosis -- Early works to 1800.  
    A29017  Matter -- Constitution -- Early works to 1800....  
    A56390     Platonists. Empiricism -- Early works to 1800.  
    A44061  Medicine -- Early works to 1800. Plague -- Eng...  



```python
cosine_distances = pd.DataFrame(squareform(pdist(wordcounts, metric='cosine')), index=filekeys, columns=filekeys)

top5_cosine = cosine_distances.nsmallest(6, 'A28989')['A28989'][1:]
print(top5_cosine)
```

    A29017    0.432181
    A43020    0.616269
    A62436    0.629395
    A57484    0.633845
    A60482    0.663113
    Name: A28989, dtype: float64



```python
print(metadata.loc[top5_cosine.index, ['Author','Title','Keywords']])
```

                                    Author  \
    A29017       Boyle, Robert, 1627-1691.   
    A43020     Harvey, Gideon, 1640?-1700?   
    A62436     Thomson, George, 17th cent.   
    A57484  Rochefort, César de, b. 1605.   
    A60482         Smith, John, 1630-1679.   
    
                                                        Title  \
    A29017  The origine of formes and qualities, (accordin...   
    A43020  Morbus anglicus: or, The anatomy of consumptio...   
    A62436  Loimotomia, or, The pest anatomized in these f...   
    A57484  The history of the Caribby-islands, viz, Barba...   
    A60482  Gērochomia vasilikē King Solomons portraitur...   
    
                                                     Keywords  
    A29017  Matter -- Constitution -- Early works to 1800....  
    A43020               Tuberculosis -- Early works to 1800.  
    A62436  Hodges, Nathaniel, 1629-1688. -- Vindiciae med...  
    A57484     Natural history -- West Indies. Carib Indians.  
    A60482  Bible. -- O.T. -- Ecclesiastes XII, 1-6 -- Par...  



