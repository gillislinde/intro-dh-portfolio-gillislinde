---
layout: page
title: Exercises Ch. 3
description: Select exercises from Python Crash Course
---


# Phython Crash Course Chpater 3

## 3-1. Names
Store the names of a few of your friends in a list called names. Print each person’s name by accessing each element in the list, one at a time.


```python
friends = ['Wade', 'Allen', 'Jordan']
print(friends[0])
print(friends[1])
print(friends[2])
```

    Wade
    Allen
    Jordan


## 3-2. Greetings
Start with the list you used in Exercise 3-1, but instead of just printing each person’s name, print a message to them. The text of each message should be the same, but each message should be personalized with the person’s name.


```python
friends = ['Wade', 'Allen', 'Jordan']
print(f"What's up, {friends[0]}?")
print(f"What's up, {friends[1]}?")
print(f"What's up, {friends[2]}?")
```

    What's up, Wade?
    What's up, Allen?
    What's up, Jordan?


## 3-3. Your Own List
Think of your favorite mode of transportation, such as a motorcycle or a car, and make a list that stores several examples. Use your list to print a series of statements about these items, such as “I would like to own a Honda motorcycle.”


```python
sports_cars = ['Porche', 'Ferrari', 'Pagani']
print(f"I would love to drive a {sports_cars[0]}!")
print(f"I would love to drive a {sports_cars[1]}!")
print(f"I would love to drive a {sports_cars[2]}!")
```

    I would love to drive a Porche!
    I would love to drive a Ferrari!
    I would love to drive a Pagani!


## 3-4. Guest List
If you could invite anyone, living or deceased, to dinner, who would you invite? Make a list that includes at least three people you’d like to invite to dinner. Then use your list to print a message to each person, inviting them to dinner.


```python
guests = ['Mom', 'Sister', 'Dad']
print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")
```

    Please come to my dinner, Mom!
    Please come to my dinner, Sister!
    Please come to my dinner, Dad!


## 3-5. Changing Guest List
You just heard that one of your guests can’t make the dinner, so you need to send out a new set of invitations. You’ll have to think of someone else to invite.

Start with your program from Exercise 3-4. Add a print() call at the end of your program stating the name of the guest who can’t make it.
Modify your list, replacing the name of the guest who can’t make it with the name of the new person you are inviting.
Print a second set of invitation messages, one for each person who is still in your list.


```python
guests = ['Mom', 'Sister', 'Dad']
print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")

print(f"{guests[0]} is unavailble.")

guests.remove("Mom")

new_guest = "Friend"
guests.append(new_guest)

print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")
```

    Please come to my dinner, Mom!
    Please come to my dinner, Sister!
    Please come to my dinner, Dad!
    Mom is unavailble.
    Please come to my dinner, Sister!
    Please come to my dinner, Dad!
    Please come to my dinner, Friend!


## More Guests
You just found a bigger dinner table, so now more space is available. Think of three more guests to invite to dinner.

Start with your program from Exercise 3-4 or Exercise 3-5. Add a print() call to the end of your program informing people that you found a bigger dinner table.
Use insert() to add one new guest to the beginning of your list.
Use insert() to add one new guest to the middle of your list.
Use append() to add one new guest to the end of your list.
Print a new set of invitation messages, one for each person in your list.


```python
guests = ['Mom', 'Sister', 'Friend']
print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")

print("I found a bigger table!")

guests.insert(0, "Friend_2")
guests.insert(2, "Friend_3")
guests.append("Friend_4")

print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")
print(f"Please come to my dinner, {guests[3]}!")
print(f"Please come to my dinner, {guests[4]}!")
print(f"Please come to my dinner, {guests[5]}!")
```

    Please come to my dinner, Mom!
    Please come to my dinner, Sister!
    Please come to my dinner, Friend!
    I found a bigger table!
    Please come to my dinner, Friend_2!
    Please come to my dinner, Mom!
    Please come to my dinner, Friend_3!
    Please come to my dinner, Sister!
    Please come to my dinner, Friend!
    Please come to my dinner, Friend_4!


## 3-7. Shrinking Guest List
You just found out that your new dinner table won’t arrive in time for the dinner, and you have space for only two guests.

Start with your program from Exercise 3-6. Add a new line that prints a message saying that you can invite only two people for dinner.
Use pop() to remove guests from your list one at a time until only two names remain in your list. Each time you pop a name from your list, print a message to that person letting them know you’re sorry you can’t invite them to dinner.
Print a message to each of the two people still on your list, letting them know they’re still invited.
Use del to remove the last two names from your list, so you have an empty list. Print your list to make sure you actually have an empty list at the end of your program.


```python
guests = ['Mom', 'Sister', 'Friend']
print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")

print("I found a bigger table!")

guests.insert(0, "Friend_2")
guests.insert(2, "Friend_3")
guests.append("Friend_4")

print(f"Please come to my dinner, {guests[0]}!")
print(f"Please come to my dinner, {guests[1]}!")
print(f"Please come to my dinner, {guests[2]}!")
print(f"Please come to my dinner, {guests[3]}!")
print(f"Please come to my dinner, {guests[4]}!")
print(f"Please come to my dinner, {guests[5]}!")

print("Sorry, I can now only invite two people!")

print(F"Sorry, {guests[5]} I can no longer invite you to dinner.")
guests.pop()
print(guests)

print(F"Sorry, {guests[4]} I can no longer invite you to dinner.")
guests.pop()
print(guests)

print(F"Sorry, {guests[3]} I can no longer invite you to dinner.")
guests.pop()
print(guests)

print(F"Sorry, {guests[2]} I can no longer invite you to dinner.")
guests.pop()
print(guests)

print(f"Dear {guests[0]}, you are still invited!")
print(f"Dear {guests[0]}, you are still invited!")

del guests[0]
del guests[0]
print(guests)
```

    Please come to my dinner, Mom!
    Please come to my dinner, Sister!
    Please come to my dinner, Friend!
    I found a bigger table!
    Please come to my dinner, Friend_2!
    Please come to my dinner, Mom!
    Please come to my dinner, Friend_3!
    Please come to my dinner, Sister!
    Please come to my dinner, Friend!
    Please come to my dinner, Friend_4!
    Sorry, I can now only invite two people!
    Sorry, Friend_4 I can no longer invite you to dinner.
    ['Friend_2', 'Mom', 'Friend_3', 'Sister', 'Friend']
    Sorry, Friend I can no longer invite you to dinner.
    ['Friend_2', 'Mom', 'Friend_3', 'Sister']
    Sorry, Sister I can no longer invite you to dinner.
    ['Friend_2', 'Mom', 'Friend_3']
    Sorry, Friend_3 I can no longer invite you to dinner.
    ['Friend_2', 'Mom']
    Dear Friend_2, you are still invited!
    Dear Friend_2, you are still invited!
    []


## 3-8. Seeing the World
Think of at least five places in the world you’d like to visit.

Store the locations in a list. Make sure the list is not in alphabetical order.
Print your list in its original order. Don’t worry about printing the list neatly, just print it as a raw Python list.
Use sorted() to print your list in alphabetical order without modifying the actual list.
Show that your list is still in its original order by printing it.
Use sorted() to print your list in reverse alphabetical order without changing the order of the original list.
Show that your list is still in its original order by printing it again.
Use reverse() to change the order of your list. Print the list to show that its order has changed.
Use reverse() to change the order of your list again. Print the list to show it’s back to its original order.
Use sort() to change your list so it’s stored in alphabetical order. Print the list to show that its order has been changed.
Use sort() to change your list so it’s stored in reverse alphabetical order. Print the list to show that its order has changed.


```python
locations = ["North America", "South America", "Europe", "Asia", "Africa"]

print(locations)

print(sorted(locations))

print(locations)

locations.reverse()
print(locations)

locations.reverse()
print(locations)

locations.sort()
print(locations)

locations.sort(reverse=True)
print(locations)
```

    ['North America', 'South America', 'Europe', 'Asia', 'Africa']
    ['Africa', 'Asia', 'Europe', 'North America', 'South America']
    ['North America', 'South America', 'Europe', 'Asia', 'Africa']
    ['Africa', 'Asia', 'Europe', 'South America', 'North America']
    ['North America', 'South America', 'Europe', 'Asia', 'Africa']
    ['Africa', 'Asia', 'Europe', 'North America', 'South America']
    ['South America', 'North America', 'Europe', 'Asia', 'Africa']



```python

```
