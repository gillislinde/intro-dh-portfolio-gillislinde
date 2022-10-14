---
layout: page
title: Exercises Ch. 6
description: Select exercises from Python Crash Course
---

# Python Crash Course Chapter 6

## 6-1. Person
Use a dictionary to store information about a person you know. Store their first name, last name, age, and the city in which they live. You should have keys such as first_name, last_name, age, and city. Print each piece of information stored in your dictionary.


```python
person = {'first_name':'wade','last_name':'perry','age':21,'city':'baltimore'}

print(person['first_name'])
print(person['last_name'])
print(person['age'])
print(person['city'])
```

    wade
    perry
    21
    baltimore


## 6-2. Favorite Numbers
Use a dictionary to store people’s favorite numbers. Think of five names, and use them as keys in your dictionary. Think of a favorite number for each person, and store each as a value in your dictionary. Print each person’s name and their favorite number. For even more fun, poll a few friends and get some actual data for your program.


```python
favorite_numbers = {'person_1':1,'person_2':2, 'person_3':3,'person_4':4,'person_5':5}
for key, value in favorite_numbers.items():
    print(key, value)
```

    person_1 1
    person_2 2
    person_3 3
    person_4 4
    person_5 5


## 6-3. Glossary
A Python dictionary can be used to model an actual dictionary. However, to avoid confusion, let’s call it a glossary.

Think of five programming words you’ve learned about in the previous chapters. Use these words as the keys in your glossary, and store their meanings as values.
Print each word and its meaning as neatly formatted output. You might print the word followed by a colon and then its meaning, or print the word on one line and then print its meaning indented on a second line. Use the newline character (\n) to insert a blank line between each word-meaning pair in your output.


```python
definitions = {'and':'boolean operator that checks the condition of two operands','not':'boolean operator that reverses the condition of the operand','elif':'a conditional execution statement following and if that is short for else-if','print':'will print/export argument',"string":"a sequence of characters treated as text"}
for key, value in definitions.items():
    print(f"{key} : {value}")
```

    and : boolean operator that checks the condition of two operands
    not : boolean operator that reverses the condition of the operand
    elif : a conditional execution statement following and if that is short for else-if
    print : will print/export argument
    string : a sequence of characters treated as text


## 6-4. Glossary 2
Now that you know how to loop through a dictionary, clean up the code from Exercise 6-3 (page 99) by replacing your series of print() calls with a loop that runs through the dictionary’s keys and values. When you’re sure that your loop works, add five more Python terms to your glossary. When you run your program again, these new words and meanings should automatically be included in the output.


```python
## already used for loop

definitions = {'and':'boolean operator that checks the condition of two operands','not':'boolean operator that reverses the condition of the operand','elif':'a conditional execution statement following and if that is short for else-if','print':'will print/export argument',"string":"a sequence of characters treated as text"}
for key, value in definitions.items():
    print(f"{key} : {value}")
```

    and : boolean operator that checks the condition of two operands
    not : boolean operator that reverses the condition of the operand
    elif : a conditional execution statement following and if that is short for else-if
    print : will print/export argument
    string : a sequence of characters treated as text



```python
definitions = {'and':'boolean operator that checks the condition of two operands','not':'boolean operator that reverses the condition of the operand','elif':'a conditional execution statement following and if that is short for else-if','print':'will print/export argument','string':'a sequence of characters treated as text','is':'compares the value/identity of two objects','for':'iterate through and object, often lists','true':'boolean true','false':'boolean false','floats':'decimal numbers'}
for key, value in definitions.items():
    print(f"{key} : {value}")
```

    and : boolean operator that checks the condition of two operands
    not : boolean operator that reverses the condition of the operand
    elif : a conditional execution statement following and if that is short for else-if
    print : will print/export argument
    string : a sequence of characters treated as text
    is : compares the value/identity of two objects
    for : iterate through and object, often lists
    true : boolean true
    false : boolean false
    floats : decimal numbers


## 6-5. Rivers
Make a dictionary containing three major rivers and the country each river runs through. One key-value pair might be 'nile': 'egypt'.

Use a loop to print a sentence about each river, such as The Nile runs through Egypt.
Use a loop to print the name of each river included in the dictionary.
Use a loop to print the name of each country included in the dictionary.


```python
rivers = {'nile':'egypt','mystic river':'the united states of america','congo':'congo'}
for key, value in rivers.items():
    print(f"The {key.title()} is in the country {value.title()}!")
```

    The Nile is in the country Egypt!
    The Mystic River is in the country The United States Of America!
    The Congo is in the country Congo!


## 6-7. People
Start with the program you wrote for Exercise 6-1 (page 99). Make two new dictionaries representing different people, and store all three 
dictionaries in a list called people. Loop through your list of people. As you loop through the list, print everything you know about each person.


```python


person_1 = {'first_name':'wade','last_name':'perry','age':21,'city':'baltimore'}
person_2 = {'first_name':'allen','last_name':'terman','age':22,'city':'chicago'}
person_3 = {'first_name':'hayden','last_name':'virtue','age':22,'city':'hawaii'}

people = [person_1,person_2,person_3]


for person in people:
    print(f"{person['first_name'].title()} {person['last_name'].title()} is {person['age']} years old and is from {person['city'].title()}!")


```

    Wade Perry is 21 years old and is from Baltimore!
    Allen Terman is 22 years old and is from Chicago!
    Hayden Virtue is 22 years old and is from Hawaii!


## 6-8. Pets
Make several dictionaries, where each dictionary represents a different pet. In each dictionary, include the kind of animal and the owner’s name. Store these dictionaries in a list called pets. Next, loop through your list and as you do, print everything you know about each pet.


```python
pet_1 = {'animal':'cat','owners_name':'wade'}
pet_2 = {'animal':'dog','owners_name':'allen'}
pet_3 = {'animal':'fish','owners_name':'hayden'}

pets = [pet_1,pet_2,pet_3]


for pet in pets:
    print(f"{pet['owners_name'].title()} owns a {pet['animal']}!")


```

    Wade owns a cat!
    Allen owns a dog!
    Hayden owns a fish!


## 6-9. Favorite Places
Make a dictionary called favorite_places. Think of three names to use as keys in the dictionary, and store one to three favorite places for each person. To make this exercise a bit more interesting, ask some friends to name a few of their favorite places. Loop through the dictionary, and print each person’s name and their favorite places.


```python
favorite_places = {'wade':'trenton','allen':'bed','hayden':'island'}

for key, value in favorite_places.items():
    print(f"{key.title()}'s favorite place is {value.title()}!")
```

    Wade's favorite place is Trenton!
    Allen's favorite place is Bed!
    Hayden's favorite place is Island!


## 6-11. Cities
Make a dictionary called cities. Use the names of three cities as keys in your dictionary. Create a dictionary of information about each city and include the country that the city is in, its approximate population, and one fact about that city. The keys for each city’s dictionary should be something like country, population, and fact. Print the name of each city and all of the information you have stored about it.


```python
cities = {
    'Los Angeles': {
        'country': 'The United States of America',
        'population':3898747,
        'fact':'LA is the only North American city to host the Olympics twice.'
        },
    'Boston': {
        'country': 'The United States of America',
        'population':675647,
        'fact':"Boston is home to America's oldest populic park, the Boston Common."
        },
    'Chicago': {
        'country': 'The United States of America',
        'population':2746388,
        'fact':"Chicago's nickname is The Windy City."
        }
    }
    

for city, city_info in cities.items():
    country = city_info['country']
    population = city_info['population']
    fact = city_info['fact']
    print("\n" + city.title() + " is in " + country + ".")
    print("It has a population of about " + str(population) + ".")
    print(fact)
```

    
    Los Angeles is in The United States of America.
    It has a population of about 3898747.
    LA is the only North American city to host the Olympics twice.
    
    Boston is in The United States of America.
    It has a population of about 675647.
    Boston is home to America's oldest populic park, the Boston Common.
    
    Chicago is in The United States of America.
    It has a population of about 2746388.
    Chicago's nickname is The Windy City.



```python

```
