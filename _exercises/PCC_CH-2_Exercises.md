---
layout: page
title: Exercises Ch. 2
description: Select exercises from Python Crash Course
---



# Python Crash Course Chapter 2 Exercises
## 2-1 Simple Message
Store a message in a variable, and then print that message


```python
message = "Hello World!"
print(message)
```

    Hello World!


## 2-1 Simple Messages
Store a message in a variable, and print that message. Then change the value of your variable ot a new message and print the new message.


```python
message = "Hi!"
print(message)
```

    Hi!



```python
message = "Hello!"
print(message)
```

    Hello!


## 2-3 Personal Message
Store a person’s name in a variable, and print a message to that person. Your message should be simple, such as, “Hello Eric, would you like to learn some Python today?”


```python
persons_name = "Wade"
message = "Hello " + persons_name + ", would you like to learn some Python today?"
print(message)
```

    Hello Wade, would you like to learn some Python today?


## 2-4 Name Cases
Store a person’s name in a variable, and then print that person’s name in lowercase, uppercase, and titlecase.


```python
persons_name = "Wade Perry"
print(persons_name.lower())
print(persons_name.upper())
print(persons_name.title())

```

    wade perry
    WADE PERRY
    Wade Perry


## 2-5 Famous Quote
Find a quote from a famous person you admire. Print the quote and the name of its author. 


```python
quote = 'Nelson Mandela once said, "It always seems impossible until it is done."'
print(quote)
```

    Nelson Mandela once said, "It always seems impossible until it is done."


## 2-6 Famous Quote 2
Repeat Exercise 2-5, but this time store the famous person’s name in a variable called famous_person. Then compose your message and store it in a new variable called message. Print your message.


```python
famous_person = "Nelson Mandela"
message = famous_person + ' once said, "It always seems impossible until it is done."'
print(message)
```

    Nelson Mandela once said, "It always seems impossible until it is done."


## 2-7 Stripping Names
Store a person’s name, and include some whitespace characters at the beginning and end of the name. Make sure you use each character combination, "\t" and "\n", at least once.


```python
name = " Wade Perry "
print(name)
print(name.lstrip())
print(name.rstrip())
print(name.strip())

tabbed_name = "\tWade Perry"
print(tabbed_name.lstrip())
new_line_name = "\nWade Perry"
print(new_line_name.lstrip())

```

     Wade Perry 
    Wade Perry 
     Wade Perry
    Wade Perry
    Wade Perry
    Wade Perry


## 2-10 Adding Comments
Choose two of the programs you’ve written, and add at least one comment to each. If you don’t have anything specific to write because your programs are too simple at this point, just add your name and the current date at the top of each program file. Then write one sentence describing what the program does.


```python
persons_name = "Wade Perry"
print(persons_name.lower()) # Prints in lower case
print(persons_name.upper()) # Prints in upper case
print(persons_name.title()) # Prints in title case

famous_person = "Nelson Mandela" # Creates famous_person variable
message = famous_person + ' once said, "It always seems impossible until it is done."' #imbeds famous_person variable into message
print(message) # Prints message
```

    wade perry
    WADE PERRY
    Wade Perry
    Nelson Mandela once said, "It always seems impossible until it is done."

