---
title: Introduction to Data Science in Python - Week 1 Course Notes
date: "2021-12-24T13:12:03.284Z"
description: "Covers Python fundamentals, data manipulation with Numpy and regular expressions."
---

[Ref: Coursera - Introduction to Data Science in Python](https://www.coursera.org/learn/python-data-analysis)

### Python: Types and Sequences

**Common types**: string, None, int, float, function

**Type** function: can be used to identify the type of a given reference.

```python
type('string') # str
type(None) # NoneType
type(add_nums) # function
type((100,200)) # tuple
```

#### Tuples, Lists, Dictionaries

**Tuples**: immutable, items are ordered and cannot be changed once created.
```python
sample_tuple=(101,'x',22, 'y')
```

**Lists**: mutable, the number of elements and element values can be changed.
```python
sample_list=[200,'w',99, 'v']
sample_list.append(300)
```

Lists and tuples are iterable types.
```python
for item in sample_list:
    print(item)
```

```python
i = 0
while (i != len(sample_list))
    print(sample_list[i])
    i = i + 1
```

**in operator**
```python
20 in [20,33] # True
```

#### Slicing
```python
sample_string = 'Sample String'
print(x[:3]) # Sam
print(x[-1]) # g
```

**Split function**: breaks a string up based on a given pattern
```python
fname = 'Jane'
lname = 'Doe'
print(fname + ' ' + lname) # Jane Doe
print(fname.split('')) # ['J', 'a', 'n', 'e']
print(fname.split('')[-1]) # 'e'
```
**Dictionaries**: labelled collections which don't have an order. For each value inserted into the dictionary, a key would be needed to fetch the corresponding value.

```python
sample_dict={'Chris': 'c@j.com', 'Brook': 'b@k.com'}
sample_dict['Chris'] # 'c@j.com'
```

Iterate over keys and values using the ```items()``` function.
```python
for name, email in sample_dict.items():
    print(name, email)
```

**Unpacking values**
```python
 my_tuple = ('John', 'Doe', 30)
 fname, lname, age = my_tuple
```
**Python string formatting**
```python
order_details = {'order_id': 'o123', 'order_total': '22.20'}
order_statement = 'Order number: {} has a total of ${}'
print(order_statement.format(order_details['order_id'], order_details['order_total']))
# Order number: o123 has a total of $22.20
```

**Dates and Times**
Get current time since the epoch using the ```time``` module.
```python
import datetime as dt
import time as tm
tm.time() # seconds from epoch
dtnow = dt.datetime.fromtimestamp(tm.time())
dtnow # datetime.datetime(2021, 10, 10, 10, 10, 50, 50071)
```

#### Python Objects, map()

**Classes**: generally named in camelcase. Class variables can be declared and are shared across all instances.

Objects in Python don't have private and public methods. Constructors are optional.
```python
class Person:

    def set_age(self, new_age):
        self.age = new_age

p1 = Person()
p1.set_age(22)
```

```map()``` function takes two parameters: a function that's to be executed and, an iterable to which the function is applied to every item in the iterable. Maps are iterable, just like lists.
```map()``` returns a map object.

[Lazy evaluation](https://towardsdatascience.com/what-is-lazy-evaluation-in-python-9efb1d3bfed0) is used here. The expression is not immediately evaluated. It is only evaluated when the outcome is needed. This programming design makes it memory and time efficient.

```python
nums1 = [9, 2, 10]
nums2 = [7, 8, 2]
lowest = map(min, nums1, nums2)
lowest # map object
```

Another example of lazy evaluation is the ```range()``` function. ```range(3)``` only stores the start, stop, step values and calculates each item when it's needed.
```python
 sys.getsizeof(range(5)) # 48
 sys.getsizeof(range(500)) # 48
```
```getsizeof()``` returns the size of an object in bytes.

Other examples of lazy evaluation include: zip, generators and decorators.

**Lambdas**: Lambdas are anonymous functions. Return of a Lambda is a function reference. Default values aren't allowed for Lambda parameters.

```python
x = lambda a,b,c : a * b * c
print (x(1,2,3)) # 6
```

**List Comprehension**: condensed format. May offer readability and performance benefits.
```python
sample_list = [i for i in range(0,3) if i % 2 == 0] # [0, 2]

my_list = [i*j for i in range(10) for j in range(10)] # [0, 0, 0, 0, 1, 2, 0, 2, 4]
```

### Data Manipulation: Numpy and Regex

#### Numpy - Array Creation
One way to create an Array is to pass a list or list of lists as an argument to a numpy array.

```python
a = np.array([3,4,5])
print(a.ndim) # Prints number of dimensions of a list

b = np.array([3,4,5], [13,14,15])
print(b.shape) # Shape - returns a tuple indicating the length of each dimension
print(b.dtype) # dtype('int64')
```
Data within Numpy arrays is homogeneous.  

Some helper functions to create Numpy arrays with initial placeholders.
```python
d = np.zeros((2,3)) #2,3 is the shape
print(d)

e = np.ones((3,3))
print(e)

f = np.arange(10, 50, 2) # parameters: start, end (exclusive) and step
```

#### Array Operations

Array operators are applied element-wise.

**Boolean array**: apply an operator on an array and a boolean is returned for any element in the original.
True is emitted, if the condition is met.

```python
a = np.array([5, 10, 15])
b = np.array([1, 2, 3])
print(a - b) # [4, 8, 12]
print(a * b)

farenheit = np.array([0, -10, 15])
celcius = (farenheit - 31) * (5/9)
celcius%2 == 0 # returns boolean array
```
**Matrix manipulation**:

- ```*``` is for element-wise comparison
- ```@``` sign is used for dot product

```python
a = np.array([[2,2], [0,1]])
b = np.array([[2,2], [0,1]])

print(a*b)
print(a@b)
```
**Upcasting**: when manipulating arrays of different types, the more general of the two types is used for the resulting array.

#### Indexing, Slicing and Iterating

```python
a = np.array([[1,4], [4,5], [5,6]])
print(a) # array([[1, 4],[4, 5],[5, 6]])
```
Pluck out specific elements from a n-dimensional array. In the second approach here, two lists get zipped.
```python
np.array([a[1,1], a[2,1]  ]) # array([5, 6])
print(a[ [1, 2], [1,1] ]) # [5 6]
```
#### Boolean Indexing

```python
print(a>1)
# [[False  True] [ True  True] [ True  True]]
```
The above values can be placed as a mask over the original array (boolean masking) to return a 1 dimensional array. Operation used here is broadcasted.
```python
print(a[a>2]) # [4 4 5 5 6]
```
#### Slicing
A slice of an array is a view into an array's data. Passing by reference: modifying a sub-array will consequently modify the original array.

```python
a = np.array([[1,4,2], [4,5,2], [5,6,7]])
a[:2] # returns first rows
a[:2, 1:3] # [[4 2] [5 2]]
sub_a = a[:2, 1:3] # [[4 2] [5 2]]
sub_a[0,0] = 99
print(sub_a) # [[99  2] [ 5  2]]
print(a) # [[ 1 99  2] [ 4  5  2] [ 5  6  7]]
```
**Numpy**: fetching a column of data as a list versus persevering the general shape of their own rows. This example illustrates how the shape of data is just an abstraction which can be layered on top of data as needed.

```python
b = np.array([[1,4,2], [4,5,2], [5,6,7]])
b[:, 0] # array([1, 4, 5])
b[:, 0:1] # array([[1], [4], [5]])
```
**Basic statistics:**

Mean for a specific column.
```python
b[:, -1].mean() # 3.666
```

### Manipulating Text with Regex
**re.match()** checks for a string match at the beginning of a string and returns a boolean.

**re.search()** checks for a string match anywhere in the string and returns a boolean.

**re.findall()**  find all occurrences of a given pattern in a string

**re.split()**  splits a string into a list of substrings, based on a given pattern

```python
import re
text = "does world exist in hello world"
if re.search('world', text):
    print('yes') # prints yes
else:
    print('no')
```

```python
text = "Ms Jane is a student. Jane is a composer"
print(re.match('Jane', text)) # None
re.findall('Jane', text) # ['Jane', 'Jane']
```

#### Regex API
**Anchors**: specify the start and/or the end of a string that you're trying to match.
 Caret character ^ indicates start and the dollar sign character indicates end.

 ```python
 text = "Jane is a student. Jane is a composer"
 re.search('^Jane', text) # <re.Match object span(0,3) match='Jane'>
 ```
**Set operator**
Find the number of occurrences of A or B in a string.
```python
text = "ABABCB"
re.findall('[AB]', text) # ['A', 'B', 'A', 'B', 'B']
```
Find all instances where A is followed by B or C
```python
text = "ACBABCB"
re.findall('[A][B-C]', text) # ['AC', 'AB']
```
Match any value at the beginning of a string which is not an A.
```python
re.findall('^[^A]', text) # []
```

**Quantifiers**: are the number of times a pattern is to be matched in order to count as a match. e(m, n): expression where m, n represent the minimum and maximum number of times the item could be matched.
```python
text = "ACBAABCBAAA"
re.findall('A{2,4}', text) # ['AA', 'AAA']

# Here 2 represents min and max of the expression
re.findall('A{2}', text) # ['AA', 'AA']
```
**Meta characters**
- \w special pattern: any letter or digit
- \s any whitespace character
