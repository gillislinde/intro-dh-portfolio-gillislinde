---
layout: page
title: Exercises Ch. 5
description: Select exercises from Python Crash Course
---

# Python Crash Course Chapter 5

## 5-1. Conditional Tests:
Write a series of conditional tests. Print a statement describing each test and your prediction for the results of each test. Your code should look something like this:

car = 'subaru'
print("Is car == 'subaru'? I predict True.")
print(car == 'subaru')

print("\nIs car == 'audi'? I predict False.")
print(car == 'audi')

Look closely at your results, and make sure you understand why each line evaluates to True or False.
Create at least ten tests. Have at least five tests evaluate to True and another five tests evaluate to False.


```python
car = 'audi'
print("Is car == 'audi'? I predict True.")
print(car == 'audi')

print("---")

car = 'audi'
print("Is car != 'audi'? I predict False.")
print(car != 'audi')

print("---")

number_1 = "1"
number_2 = "10"
print("Is number_1 > number_2? I predict False.")
print(number_1 > number_2)

print("---")

a = 1
b = 1
print("Is a > b? I predict False.")
print(a > b)

print("---")

a = 1
b = 1
print("Is a < b? I predict False.")
print(a < b)

print("---")

a = 1
b = 1
print("Is a != b? I predict False.")
print(a != b)

print("---")

a = 1 
b = 1
print("Is a + b == 3? I predict False.")
print(a + b == 3)

print("---")

a = 1 
b = 1
print("Is a + b == 2? I predict True.")
print(a + b == 2)

print("---")

a = 1 
b = 1
print("Is a * b == 1? I predict True.")
print(a * b == 1)

print("---")

a = 1 
b = 1
print("Is a / b == 1? I predict True.")
print(a / b == 1)

print("---")

a = 1 
b = 1
print("Is a == b? I predict True.")
print(a == b)

print("---")

a = 1 
b = 10
print("Is a < b? I predict True.")
print(a < b)

print("---")
```

    Is car == 'audi'? I predict True.
    True
    ---
    Is car != 'audi'? I predict False.
    False
    ---
    Is number_1 > number_2? I predict False.
    False
    ---
    Is a > b? I predict False.
    False
    ---
    Is a < b? I predict False.
    False
    ---
    Is a != b? I predict False.
    False
    ---
    Is a + b == 3? I predict False.
    False
    ---
    Is a + b == 2? I predict True.
    True
    ---
    Is a * b == 1? I predict True.
    True
    ---
    Is a / b == 1? I predict True.
    True
    ---
    Is a == b? I predict True.
    True
    ---
    Is a < b? I predict True.
    True
    ---


## 5-2. More Conditional Tests
You don’t have to limit the number of tests you create to ten. If you want to try more comparisons, write more tests and add them to conditional_tests.py. Have at least one True and one False result for each of the following:

Tests for equality and inequality with strings
Tests using the lower() method
Numerical tests involving equality and inequality, greater than and less than, greater than or equal to, and less than or equal to
Tests using the and keyword and the or keyword
Test whether an item is in a list
Test whether an item is not in a list


```python
Porche = "car"
print("Is Porche == 'lame car'? I predict False")
print(Porche == car)

print("---")

Porche = "Car"
print("Is porche.lower() == 'car'? I predict True.")
print(porche.lower() == 'car')

print("---")

print("Is 1 + 1 == 2? I predict True.")
print(1 + 1 == 2)

print("---")

print("Is 1 > 1? I predict False.")
print(1 > 1)

print("---")

print("Is 1 < 1? I predict False.")
print(1 < 1)

print("---")

print("Is 1 <= 1? I predict True.")
print(1 <= 1)

print("---")

print("Is 1 >= 1? I predict True.")
print(1 >= 1)

print("---")

print("Is 1 > 1 and 1 > 2? I predict False.")
print(1 > 1 and 1 < 2)

print("---")
print("Is 1 > 1 or 1 > 2? I predict True.")
print(1 > 1 or 1 < 2)

print("---")

numbers = ["1", "2", "3"]
print("Is 1 in numbers? I predict True.")
print("1" in numbers)

print("---")

numbers = ["1", "2", "3"]
print("Is 4 in numbers? I predict False.")
print("4" in numbers)
```

    Is Porche == 'lame car'? I predict False
    False
    ---
    Is porche.lower() == 'car'? I predict True.
    True
    ---
    Is 1 + 1 == 2? I predict True.
    True
    ---
    Is 1 > 1? I predict False.
    False
    ---
    Is 1 < 1? I predict False.
    False
    ---
    Is 1 <= 1? I predict True.
    True
    ---
    Is 1 >= 1? I predict True.
    True
    ---
    Is 1 > 1 and 1 > 2? I predict False.
    False
    ---
    Is 1 > 1 or 1 > 2? I predict True.
    True
    ---
    Is 1 in numbers? I predict True.
    True
    ---
    Is 4 in numbers? I predict False.
    False


## 5-6. Stages of Life
Write an if-elif-else chain that determines a person’s stage of life. Set a value for the variable age, and then:

If the person is less than 2 years old, print a message that the person is a baby.
If the person is at least 2 years old but less than 4, print a message that the person is a toddler.
If the person is at least 4 years old but less than 13, print a message that the person is a kid.
If the person is at least 13 years old but less than 20, print a message that the person is a teenager.
If the person is at least 20 years old but less than 65, print a message that the person is an adult.
If the person is age 65 or older, print a message that the person is an elder.


```python
age = 21
if age < 2:
    print("You are a baby.")
elif age >= 2 and age < 4:
    print("You are a toddler.")
elif age >=4 and age < 13:
    print("You are a kid.")
elif age >= 13 and age < 20:
    print("You are a teenager.")
elif age >=20 and age < 65:
    print("You are an adult.")
else:
    print("You are an elder")
```

    You are an adult.


## 5-7. Favorite Fruit
Make a list of your favorite fruits, and then write a series of independent if statements that check for certain fruits in your list.

Make a list of your three favorite fruits and call it favorite_fruits.
Write five if statements. Each should check whether a certain kind of fruit is in your list. If the fruit is in your list, the if block should print a statement, such as You really like bananas!


```python
favorite_fruits = ["banana", "strawberry", "mango"]

if "banana" in favorite_fruits:
    print("I really like bananas!")
    
if "strawberry" in favorite_fruits:
    print("I really like strawberries!")
    
if "mango" in favorite_fruits:
    print("I really like mangos!")
    
if "pineapple" in favorite_fruits:
    print("I really like pineapples!")
    
if "watermelon" in favorite_fruits:
    print("I really like watermelons!")
```

    I really like bananas!
    I really like strawberries!
    I really like mangos!


## 5-8. Hello Admin
Make a list of five or more usernames, including the name 'admin'. Imagine you are writing code that will print a greeting to each user after they log in to a website. Loop through the list, and print a greeting to each user:

If the username is 'admin', print a special greeting, such as Hello admin, would you like to see a status report?
Otherwise, print a generic greeting, such as Hello Jaden, thank you for logging in again.


```python
usernames = ["admin", "user1", "user2", "user3", "user4"]

for username in usernames:
    if username == 'admin':
        print(f"Hello {username}, would you like to see a status report?")
    else:
        print(f"Hello {username}, thank you for logging in again.")
```

    Hello admin, would you like to see a status report?
    Hello user1, thank you for logging in again.
    Hello user2, thank you for logging in again.
    Hello user3, thank you for logging in again.
    Hello user4, thank you for logging in again.


## 5-9. No Users
Add an if test to hello_admin.py to make sure the list of users is not empty.

If the list is empty, print the message We need to find some users!
Remove all of the usernames from your list, and make sure the correct message is printed.


```python
usernames = ["admin", "user1", "user2", "user3", "user4"]

if usernames:
    for username in usernames:
        if username == 'admin':
            print(f"Hello {username}, would you like to see a status report?")
        else:
            print(f"Hello {username}, thank you for logging in again.")
else:
    print("We need to find some users!")
    
print("---")
    
usernames = ["admin", "user1", "user2", "user3", "user4"]
usernames.clear()

if usernames:
    for username in usernames:
        if username == 'admin':
            print(f"Hello {username}, would you like to see a status report?")
        else:
            print(f"Hello {username}, thank you for logging in again.")
else:
    print("We need to find some users!")
```

    Hello admin, would you like to see a status report?
    Hello user1, thank you for logging in again.
    Hello user2, thank you for logging in again.
    Hello user3, thank you for logging in again.
    Hello user4, thank you for logging in again.
    ---
    We need to find some users!


## 5-10. Checking Usernames
Do the following to create a program that simulates how websites ensure that everyone has a unique username.

Make a list of five or more usernames called current_users.
Make another list of five usernames called new_users. Make sure one or two of the new usernames are also in the current_users list.
Loop through the new_users list to see if each new username has already been used. If it has, print a message that the person will need to enter a new username. If a username has not been used, print a message saying that the username is available.
Make sure your comparison is case insensitive. If 'John' has been used, 'JOHN' should not be accepted. (To do this, you’ll need to make a copy of current_users containing the lowercase versions of all existing users.)


```python
current_users = ["admin", "user1", "user2", "user3", "user4"]

new_users = ["user5", "user6", "user7", "user8", "USER1"]

for username in new_users:
    if username.lower() in current_users:
        print(f"{username} is not available, please choose a new username.")
    else:
        print(f"{username} is available.")
```

    user5 is available.
    user6 is available.
    user7 is available.
    user8 is available.
    USER1 is not available, please choose a new username.

