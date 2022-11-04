---
layout: page
title: Exercises Ch. 8
description: Select exercises from Python Crash Course
---

# Python Crash Course Chapter 8

## 8-1. Message
Write a function called display_message() that prints one sentence telling everyone what you are learning about in this chapter. Call the function, and make sure the message displays correctly.


```python
def display_message():
    print("Chapter 8 is about functions.")
    
display_message()
```

    Chapter 8 is about functions.


## 8-2. Favorite Book
Write a function called favorite_book() that accepts one parameter, title. The function should print a message, such as One of my favorite books is Alice in Wonderland. Call the function, making sure to include a book title as an argument in the function call.


```python
def favorite_book(book):
    print(f"One of my favorite books is {book}.")
    
favorite_book("Harry Potter")
```

    One of my favorite books is Harry Potter.


## 8-3. T-Shirt
Write a function called make_shirt() that accepts a size and the text of a message that should be printed on the shirt. The function should print a sentence summarizing the size of the shirt and the message printed on it.

Call the function once using positional arguments to make a shirt. Call the function a second time using keyword arguments.


```python
def make_shirt(size, message):
    print("I'm going to make a " + size + " t-shirt.")
    print('It will say, "' + message + '"')
    
make_shirt("large", "Hi!")
make_shirt(message="Hello!", size="small")
```

    I'm going to make a large t-shirt.
    It will say, "Hi!"
    I'm going to make a small t-shirt.
    It will say, "Hello!"


## 8-5. Cities
Write a function called describe_city() that accepts the name of a city and its country. The function should print a simple sentence, such as Reykjavik is in Iceland. Give the parameter for the country a default value. Call your function for three different cities, at least one of which is not in the default country.


```python
def describe_city(city, country='sweden'):
    msg = city.title() + " is in " + country.title() + "."
    print(msg)

describe_city('stockholm')
describe_city('reykjavik', 'iceland')
describe_city('uppsala')
```

    Stockholm is in Sweden.
    Reykjavik is in Iceland.
    Uppsala is in Sweden.


## 8-6. City Names
Write a function called city_country() that takes in the name of a city and its country. The function should return a string formatted like this:

"Santiago, Chile"

Call your function with at least three city-country pairs, and print the values that are returned.


```python
def city_country(city, country):
    return(city.title() + ", " + country.title())

city = city_country('santiago', 'chile')
print(city)

city = city_country('stockholm', 'sweden')
print(city)

city = city_country('london', 'england')
print(city)
```

    Santiago, Chile
    Stockholm, Sweden
    London, England


## 8-7. Album
Write a function called make_album() that builds a dictionary describing a music album. The function should take in an artist name and an album title, and it should return a dictionary containing these two pieces of information. Use the function to make three dictionaries representing different albums. Print each return value to show that the dictionaries are storing the album information correctly.

Use None to add an optional parameter to make_album() that allows you to store the number of songs on an album. If the calling line includes a value for the number of songs, add that value to the album’s dictionary. Make at least one new function call that includes the number of songs on an album.


```python
def make_album(artist, title, tracks=0):
    album_dictionary = {
        'artist': artist.title(),
        'title': title.title(),
        }
    if tracks:
        album_dictionary['tracks'] = tracks
    return album_dictionary

album = make_album('zach bryan', 'american heartbreak')
print(album)

album = make_album('kendrick lamar', 'damn.')
print(album)

album = make_album('lil baby', "it's only me", tracks=24)
print(album)

album = make_album('tory lanez', 'sorry 4 what', tracks=20)
print(album)
```

    {'artist': 'Zach Bryan', 'title': 'American Heartbreak'}
    {'artist': 'Kendrick Lamar', 'title': 'Damn.'}
    {'artist': 'Lil Baby', 'title': "It'S Only Me", 'tracks': 24}
    {'artist': 'Tory Lanez', 'title': 'Sorry 4 What', 'tracks': 20}

