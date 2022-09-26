---
layout: page
title: Variables, Strings, and Numbers
description: This notebook has code aboutu variables, strings, and numbers
---

# Heading 1
## Heading 2
This is plain text. 
* item one
* item two

[This is a link to google](google.com)

# Variables


```python
greeting = "Hello world!"
```


```python
print(greeting)
```

    Hello world!



```python
greeting
```




    'Hello world!'




```python
farewell = "Goodbye world!"
```


```python
print(farewell)
```

    Goodbye world!



```python
farewell = "Farewell world!"
print(farewell)
```

    Farewell world!



```python
#1 Strings
```

# 1 Strings


```python
ex_1 "This is a string"
print(ex_1)
```


      Input In [10]
        ex_1 "This is a string"
             ^
    SyntaxError: invalid syntax




```python
ex_1 = "This is a string"
print(ex_1)
```

    This is a string



```python
ex_2 = 'This is also a string'
```


```python
print(ex_2)
```

    This is also a string



```python
ex_3 = "Here is a string."
print(ex_3)
```

    Here is a string.



```python
ex_4 = 'I asked the question, "When should I use single quotes."'
print(ex_4)
```

    I asked the question, "When should I use single quotes."



```python
historian = "edward gibbon"
print(historian)
```

    edward gibbon



```python
print(historian.title())
```

    Edward Gibbon



```python
novelist = "Becky Chambers"
print(novelist.lower())
```

    becky chambers



```python
"becky" == "becky"
```




    True




```python
"becky" == "Becky"
```




    False




```python
first_name = "ada"
last_name = "lovelace"
```


```python
full_name = first_name + " " + last_name
print(full_name)
```

    ada lovelace



```python
greeting = f" Hello, {first_name} {last_name}"
print(greeting.title())
```

     Hello, Ada Lovelace


## Whitespace


```python
print("tab")
```

    tab



```python
print("\ttab")
```

    	tab



```python
print("Langauges: \nGreeek\nLatin\nEnglish")
```

    Langauges: 
    Greeek
    Latin
    English



```python
str_rspace = "string     "
print(str_rspace)
```

    string     



```python
print(str_rspace.rstrip())
```

    string



```python
example = str_rspace + "."
print(example)
```

    string     .



```python
example_2 = str_rspace.rstrip() + "."
print(example_2)
```

    string.


## Numbers


```python
# integers
238 + 4834
```




    5072




```python
19 - 7 
```




    12




```python
54 * 4
```




    216




```python
num = 45
```


```python
num
```




    45




```python
num + 5
```




    50




```python
type(num)
```




    int




```python
30 / 10
```




    3.0




```python
f = 30 / 7
```


```python
f
```




    4.285714285714286




```python
type(f)
```




    float




```python
3 ** 3
```




    27



## Lists


```python
subjects = ['classics', 'history', 'philosophy']
```


```python
print(subjects)
```

    ['classics', 'history', 'philosophy']



```python
print(subjects[1])
```

    history



```python
print(subjects[0])
```

    classics



```python
print(subjects[2])
```

    philosophy



```python
print(subjects[-1])
```

    philosophy



```python
message = f"My most difficult subject is {subjects[1].title()}."
print(message)
```

    My most difficult subject is History.



```python
# How to modify a list
print(subjects)
```

    ['classics', 'history', 'philosophy']



```python
subjects[1] = 'sociology'
```


```python
print(subjects)
```

    ['classics', 'sociology', 'philosophy']



```python
# append
subjects.append('history')
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history']



```python
subjects.append('mathamatics')
```


```python
subjects.append("computer science")
```


```python
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history', 'mathamatics', 'computer science']



```python
subjects[4] = 'mathematics'
```


```python
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history', 'mathematics', 'computer science']



```python
# insert
subjects.insert(0, 'religion')
```


```python
print(subjects)
```

    ['religion', 'classics', 'sociology', 'philosophy', 'history', 'mathematics', 'computer science']



```python
subjects.insert(2, 'HERE')
print(subjects)
```

    ['religion', 'classics', 'HERE', 'sociology', 'philosophy', 'history', 'mathematics', 'computer science']



```python
# delete item
del subjects[2]
print(subjects)
```

    ['religion', 'classics', 'sociology', 'philosophy', 'history', 'mathematics', 'computer science']



```python
# pop method
popped_subject = subjects.pop(0)
print(popped_subject)
print(subjects)
```

    religion
    ['classics', 'sociology', 'philosophy', 'history', 'mathematics', 'computer science']



```python
# remove
subjects.remove('sociology')
print(subjects)
```

    ['classics', 'philosophy', 'history', 'mathematics', 'computer science']



```python

```
