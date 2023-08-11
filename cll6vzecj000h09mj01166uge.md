---
title: "Python3: Assignment, Shallow Copy, and Deep Copy Methods"
seoTitle: "Python3: Assignment, Shallow Copy, and Deep Copy Methods"
seoDescription: "Unlock the potential of Python 3 with our in-depth guide on assignments, shallow copy, and deep copy methods. Learn when to use them for efficient coding."
datePublished: Fri Aug 11 2023 17:53:11 GMT+0000 (Coordinated Universal Time)
cuid: cll6vzecj000h09mj01166uge
slug: python3-assignment-shallow-copy-and-deep-copy-methods
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691701930749/42878c01-46bc-430d-93d5-5c646f7302cf.jpeg
tags: python, python3, hashnode, wemakedevs, deep-copy-vs-shallow-copy

---

In programming, knowing how to handle data is important for strong, error-free code. Three key ideas are assignment, shallow copy, and deep copy. They help developers make, copy, and change objects without causing problems. This guide will explain how they work, when to use them, and how they affect performance.

## Assignment `a=b`

In many languages, variables just point to things, not the things themselves. So, changing something through one variable also changes it for other variables connected to the same thing.

### Assignment `a=b` for Mutable Objects

[![Source: Google Developers](https://cdn.hashnode.com/res/hashnode/image/upload/v1691700316717/b1bdac0c-0c3f-4482-914f-98e098464e86.png align="left")](https://developers.google.com/edu/python/lists)

The assignment is straightforward for mutable objects. When you assign a mutable object to a new variable, both variables reference the same object. This means that changes made through one variable will directly affect the other.

```python
# Initial list with heterogeneous nested sublists
old_list = [12, 24, [1, 'apple', 3.14], ['banana', 42], ]

# Creating a new list that references the same nested sublists
new_list = old_list

# Modifying an element within the nested sublist of the new_list
new_list[2][1] = 'orange'

# Displaying the contents of both lists and their respective IDs
print('Old List:', old_list)
print('ID of Old List:', id(old_list))

print('New List:', new_list)
print('ID of New List:', id(new_list))

# Modifying old_list
old_list.append('Cherry')

# Check if the contents of old_list and new_list are the same
print(old_list==new_list)
print(id(old_list)==id(new_list))

# Output
'''
Old List: [12, 24, [1, 'orange', 3.14], ['banana', 42]]
ID of Old List: 4377486848
New List: [12, 24, [1, 'orange', 3.14], ['banana', 42]]
ID of New List: 4377486848
True
True
'''
```

When you use the assignment operator (`=`) to create a new reference to an object, both the original variable and the new variable point to the same object in memory. Therefore, modifying the object through one reference will affect the other reference as well.

### Assignment `a=b` for **Immutable Objects**

For immutable objects, such as strings and tuples, assignment works differently. Since these objects cannot be modified once created, assignment behaves similarly to a shallow copy.

```python
x = 10
y = x
x = 20  # This change won't affect y

print(x,y)

original_string = "Hello"
copied_string = original_string

copied_string += " World"  
# This creates a new string, not affecting the original

print(original_string)
print(copied_string)

print(id(original_string))
print(id(copied_string))

#Output
'''
20 10
Hello
Hello World
4367045040
4367148528
'''
```

---

**Immutable objects, such as strings, do not require copying since they remain constant, so Python uses the same data; ids are always the same**

Deep copying is suitable for nested structures, as it duplicates all elements, including nested lists. Shallow copying creates a new outer list while retaining references to the inner lists.

Using assignment does not create a copy; instead, it establishes a link to the existing data. So you need `copy` to create a new list with the same contents.

---

## **Shallow Copy** `a=copy(b)`

> It copies only the top-level elements, not any child or nested objects

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691700086164/b01f9e89-1b26-4f3d-a07b-dd48f028fa25.png align="center")

For mutable objects, a shallow copy creates a new object, but the **nested objects are still shared references**. This can lead to unexpected behaviour if you're not careful with changes to nested objects.

```python
import copy

# Example 1: Shallow Copy of Lists

old_list = [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
# Shallow copy creates a new list, but the nested lists are still referenced
new_list = copy.copy(old_list)
# Let's modify a nested list in the old_list
old_list[0][0] = 100
# Both the old_list and new_list are affected, as they share the same nested lists
print("Old list:", old_list)
print("New list:", new_list)

# Example 2: Shallow Copy and Appending

# Original list with nested lists
old_list = [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
# Shallow copy of the old_list
new_list = copy.copy(old_list)
# Appending a new nested list to the old_list
old_list.append([20, 20, 20])
# The appended list affects only the old_list, not the new_list
print("Old list:", old_list)
print("New list:", new_list)

# Example 3: Shallow Copy and Nested Modifications

old_list = [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
# Shallow copy of the old_list
new_list = copy.copy(old_list)
# Modifying a value within a nested list in the old_list
old_list[1][1] = 'BB'
# The modification is reflected in both the old_list and new_list
print("Old list:", old_list)
print("New list:", new_list)

# Output
'''
Old list: [[100, 12, 13], [14, 15, 16], [17, 18, 19]]
New list: [[100, 12, 13], [14, 15, 16], [17, 18, 19]]
Old list: [[11, 12, 13], [14, 15, 16], [17, 18, 19], [20, 20, 20]]
New list: [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
Old list: [[11, 12, 13], [14, 'BB', 16], [17, 18, 19]]
New list: [[11, 12, 13], [14, 'BB', 16], [17, 18, 19]]
'''
```

## **Deep Copy** `a=deepcopy(b)`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691700021779/b52b8e8e-66e7-4a68-b3a6-87277287167b.png align="center")

For Mutable Objects, A deep copy **creates a fully independent copy of an object and all of its nested objects.** Changes made to the deep copied object do not affect the original object or its nested elements.

```python
import copy

# Example 1: Deep Copy of Lists

old_list = [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
# Deep copy creates a new list and new nested lists
new_list = copy.deepcopy(old_list)
# Modifying a nested list in the old_list
old_list[0][0] = 100
# Only the old_list is affected, as the new_list has independent nested lists
print("Old list:", old_list)
print("New list:", new_list)


# Example 2: Deep Copy and Appending

old_list = [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
# Deep copy of the old_list
new_list = copy.deepcopy(old_list)
# Appending a new nested list to the old_list
old_list.append([20, 20, 20])
# The appended list affects only the old_list, not the new_list
print("Old list:", old_list)
print("New list:", new_list)


# Example 3: Deep Copy and Nested Modifications

old_list = [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
# Deep copy of the old_list
new_list = copy.deepcopy(old_list)
# Modifying a value within a nested list in the old_list
old_list[1][1] = 'BB'
# The modification is only reflected in the old_list, not the new_list
print("Old list:", old_list)
print("New list:", new_list)

# Output
'''
Old list: [[100, 12, 13], [14, 15, 16], [17, 18, 19]]
New list: [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
Old list: [[11, 12, 13], [14, 15, 16], [17, 18, 19], [20, 20, 20]]
New list: [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
Old list: [[11, 12, 13], [14, 'BB', 16], [17, 18, 19]]
New list: [[11, 12, 13], [14, 15, 16], [17, 18, 19]]
'''
```

### TL;DR

* Assignment creates a new reference to an existing object.
    
* A shallow copy creates a new object with shared references for nested elements.
    
* Deep copy, on the other hand, creates a fully independent copy of the object and its nested elements.
    

References:

* [https://developers.google.com/edu/python/lists](https://developers.google.com/edu/python/lists)
    
* [https://docs.python.org/3/library/copy.html#:~:text=A%20shallow%20copy%20constructs%20a,objects%20found%20in%20the%20original](https://docs.python.org/3/library/copy.html#:~:text=A%20shallow%20copy%20constructs%20a,objects%20found%20in%20the%20original).
    
* Images Inspiration: [geeksforgeeks](https://www.geeksforgeeks.org)