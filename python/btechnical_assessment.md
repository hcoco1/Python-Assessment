#### Navigation

[Back to Home 🏠](../README.md) | [Back to Introduction ](aintroduction.md)  |  [Next: Challenge](challenge.md)

## Unit 4 Career Preparation: Technical Assessment

### Problem 1

Write a script that:

- Reads the file problem1.txt.
- Adds each line to a new list.
- Prints the new list.


```python
with open('problem1.txt', 'r') as file:
    items_list = [line.strip() for line in file]
print(f"new_items_list = {items_list}")
# new_items_list = ['item1', 'item2', 'item3', 'item4', 'item5']
```

### Problem 2

Write a script that:

- Reads the file problem2.txt.
- Counts how many times 192.168.1.1 appears in the file.
- Prints the result.


```python
with open('problem2.txt', 'r') as file:
    count = 0
    for line in file:
        if line.strip() == '192.168.1.1':
            count += 1
print(f"The IP 192.168.1.1 appears {count} times.")
# The IP 192.168.1.1 appears 5 times.
```

### Problem 3

Write a script using a function (dedupe) that:

- Takes a list l = [1,5,7,2,4,3,5,1,6,2,6].
- Returns a new list that contains all of the elements from the first list, excluding duplicates.


```python
l = [1, 5, 7, 2, 4, 3, 5, 1, 6, 2, 6]
def dedupe(l):
    unique = []
    for item in l:
        if item not in unique:
            unique.append(item)
    return unique
#print the list only for testing. The instructions only ask for a function that return a list (not printing a list)
#new_list = dedupe(l)
#print(new_list)
# [1, 5, 7, 2, 4, 3, 6]
```

### Problem 4

Write a program (using a function) that:

- Asks the user for a long string containing multiple words.
- Prints back the same string, except with the words in reverse order.
- For example, if the user types the string: 'My name is robert', it will print 'robert is name My'.


```python
def reverse_order(sentence):
    words = sentence.split(' ')
    reversed_words = reversed(words)
    reversed_sentence = ' '.join(reversed_words)
    return reversed_sentence
user_input1 = input("Please enter a long string containing multiple words: ")
reversed_string = reverse_order(user_input1)
print(reversed_string)
# eeeeeeeeeeeeeeeeeee fffffffffffffffff vvvvvvvvvvvvvvv xcvxcv
```

### Problem 5

Write a script that:

- Opens the file problem5.txt.
- Counts each port and puts the results in a dictionary.


```python
with open('problem5.txt', 'r') as file:
    port_counts = {} #The results are assigned to this dictionary
    for line in file:
        if line.strip():
            port = int(line.strip())
            if port in port_counts:
                port_counts[port] += 1
            else:
                port_counts[port] = 1
#print the dict for testing. The instructions only ask for put results in a dictionary.
#print(port_counts)
# {80: 7, 443: 3, 22: 5, 21: 2, 25: 3, 389: 1, 3389: 1, 445: 3}
```



#### Navigation

[Back to Home 🏠](../README.md) | [Back to Introduction ](aintroduction.md)  |  [Next: Challenge](challenge.md)