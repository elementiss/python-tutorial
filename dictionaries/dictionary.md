# Python Dictionaries

A dictionary in Python is like a real-world dictionary - it's a collection of pairs where each
word (key) has its corresponding definition (value). In programming terms,
we call these "key-value pairs".

Here's a simple example of a dictionary containing countries and their capitals:


```python
capitals = {
    "Greece": "Athens",
    "Italy": "Rome",
    "Spain": "Madrid"
}
```

In this case, the country names are our keys, and the capital cities are our values.

## Creating Your First Dictionary

You can create an empty dictionary in two ways:

- Method 1: Using curly braces
- Method 2: Using the `dict()` constructor

<pre><code class="language-py" >
empty_dict = {}
empty_dict = dict()

print(empty_dict)
</code></pre>

💡 Because `dict` is the name of a built-in function, you should avoid using it as a variable name.


To create a dictionary with data, we use curly braces and colons to connect keys with their values:

<pre><code class="language-py" >
capitals = {
    "Greece": "Athens",
    "Italy": "Rome",
    "Spain": "Madrid"
}
print(capitals)
</code></pre>

### Using the `dict()` constructor

Creating a dictionary using `dict()` constructor with keyword arguments:

<pre><code class="language-py" >
# create a new user
user = dict(name = "John", age = 31)
print(user)

user2 = dict(user) # a new dictionary-copy will be created
print(user2)
</code></pre>

👣 Explanation:

- First, we create a new dictionary user with keys "name" and "age" assigned the values "John" and 31, respectively.
- The `print(user)` statement outputs the dictionary: `{'name': 'John', 'age': 31}`.
- Then we create a new dictionary `user2` that is a copy of the existing dictionary user.

This method works when the keys are simple strings.


### Creating a Dictionary from a List of Tuples

<pre><code class="language-py" >
user3 = dict([("name", "Eric"), ("age", 40)])
print(user3)
</code></pre>

👣 Explanation:

- This creates a new dictionary `user3` from a list of tuples. Each tuple represents a key-value pair.
- The dictionary becomes {'name': 'Eric', 'age': 40}.
- The `print(user3)` statement outputs the dictionary.


### Creating a Dictionary by Pairing Values from Two Iterables

This creates a new dictionary `user4` by pairing elements from two iterables using the `zip` function.

<pre><code class="language-py" >
user4 = dict(zip(['name', 'age'], ["Hanna", 25]))
print(user4)
</code></pre>

👣 Explanation:

- `zip(['name', 'age'], ["Hanna", 25])` pairs the first elements together and the second elements together, resulting in: `("name", "Hanna")` and `("age", 25)`.
- The dictionary becomes `{'name': 'Hanna', 'age': 25}`.
- The `print(user4)` statement outputs the dictionary.


### Creating a Dictionary Using the `fromkeys()` method

The `dict.fromkeys()` method allows you to create a new dictionary with keys
from a given iterable and each key set to a specified default value.
If no default value is provided, the keys are initialized with `None`.

<pre><code class="language-py" >
user = dict.fromkeys(['name', 'age'])
print(user)   # {'name': None, 'age': None}

point = dict.fromkeys(['x', 'y', 'z'], 100)
print(point)   # {'x': 100, 'y': 100, 'z': 100}
</code></pre>

👣 Explanation:

- We use `dict.fromkeys()` to create a dictionary with keys from the list `['name', 'age']`
- Since no default value is provided, each key is initialized to `None`.
- Then we use `dict.fromkeys()` to create a dictionary with keys from the list `['x', 'y', 'z']`.
- Each key is initialized to the specified default value 100.
- The `print(point)` statement outputs the dictionary.


It is useful when you need a dictionary where all the keys have the same values.


## Dictionary Length

Just like with lists and strings, Python makes it super easy to find out how many items
are in a dictionary. We use the built-in `len()` function:

<pre><code class="language-py">
capitals = {
    "Greece": "Athens",
    "Italy": "Rome",
    "Spain": "Madrid"
}
number_of_countries = len(capitals)
print(number_of_countries)  # 3
</code></pre>

This gives us the total number of key-value pairs in the dictionary.
It's useful when you need to check if a dictionary is empty: `len(capitals) == 0`.

💡 Remember that each key-value pair counts as one item, regardless of how complex the values might be.


## The Structure Behind the Scenes

Under the hood, Python dictionaries are implemented using hash tables.
When you create a key-value pair, Python calculates a hash value for the key (like a unique fingerprint).
This hash value determines where in memory the value will be stored.
That's why dictionary keys must be immutable (unchangeable) - things like strings, numbers, or tuples.


This hash table implementation is what makes dictionaries so fast for lookups.
When you access a value using its key, Python:

- Calculates the key's hash value
- Uses that hash to immediately locate the value in memory
- Returns the value to you

That's why looking up values in a dictionary is incredibly efficient, even with thousands of items!


## Dictionary Rules to Remember

Here are some important points to keep in mind:

- Keys must be unique, duplicates not allowed (you can't have two "Greece" keys in the same dictionary)
- Keys must be immutable (strings, numbers, tuples - but not lists)
- Values can be any type (numbers, strings, lists, other dictionaries, etc.)
- Dictionaries are mutable (you can change them after creation)


### Duplicates Not Allowed

If you attempt to create a dictionary with duplicate keys, the latter key-value pair will override the former one.
This is because dictionaries are designed to have unique keys, and any subsequent assignment
to an existing key will update its value.

<pre><code class="language-py" >
capitals = {
    "Greece": "Athens",
    "Italy": "Rome",
    "Italy": "Milano",
    "Spain": "Madrid"
}
print(capitals)
</code></pre>

👣 Explanation:

- The dictionary `capitals` is defined with four entries.
- The key "Italy" appears twice, first with the value "Rome" and then with "Milano".
- When Python processes the dictionary, it will keep the last assignment for the duplicate key and ignore any previous assignments for that key.

💡 In Python, dictionaries cannot have two items with the same key. If a key is repeated, the last key-value pair will overwrite any previous ones.



### Dictionary Items - Data Types

Dictionaries are highly versatile and can store values of any data type.

<pre><code class="language-py" >
capitals = {
    "Population": 7.4,
    "electric": False,
    "Italy": "Rome",
    "colors": ["red", "white", "blue"]
}
print(capitals)
</code></pre>

👣 Explanation:

In this example, we demonstrate how a single dictionary can hold different types of values:

- Numeric Value. The key "Population" is associated with a numeric value, a float 7.4.
- Boolean Value. The key "electric" is associated with a boolean value False.
- String Value. The key "Italy" is associated with a string "Rome".
- List Value. The key "colors" is associated with a list containing three strings: "red", "white", and "blue".


### Dictionary Keys - Data Types

The fundamental rule is simple: any immutable object can be a dictionary key. Here are the common types you can use:

<pre><code class="language-py">
mixed_keys = {
   "string_key": "value1",               # String
   42: "value2",                         # Integer
   3.14: "value3",                       # Float
   True: "value4",                       # Boolean
   (1, 2): "value5",                     # Tuple
   frozenset(['red', 'blue']): 'value6', # frozenset
   "π": "value7",                        # Unicode string
   None: "value8"                        # None
}
print(mixed_keys)
print(mixed_keys[(1, 2)])      # Using tuple key
</code></pre>

Yes, you can absolutely mix different types of keys in the same dictionary!


Python treats keys of different types that look similar as distinct keys:

<pre><code class="language-py" >
tricky_dict = {
    1: "integer one",
    "1": "string one"
}
# These are different
print(tricky_dict[1])      # Access integer key
print(tricky_dict["1"])    # Access string key
</code></pre>

💡 Be careful! True == 1 in Python.

In Python, True is equivalent to 1 and False is equivalent to 0.
This behavior can lead to surprising results when working with dictionaries because both True and 1 will be treated as the same key.

<pre><code class="language-py">
tricky_dict = {
    1: "integer one",
    1.0: "float one",
    True: "boolean true"
}
# But watch out!
print(tricky_dict[1])      # Same as tricky_dict[True]
print(tricky_dict[1.0])    # the same
print(tricky_dict[True])   # Returns "boolean true"
</code></pre>

👣 Explanation:

- The dictionary `tricky_dict` is defined with three keys: 1, 1.0, and True.
- When Python processes this dictionary, each new key-value pair that is equivalent to an existing key overwrites the previous value associated with that key.
- As a result, the last key-value pair `True: "boolean true"` will overwrite any prior values associated with the keys 1 and 1.0.

🗝️ To avoid confusion, it's best to avoid using True, False, integers, and floats that
may have equivalent values as dictionary keys if possible.


### Invalid Key Types

Not everything can be a dictionary key.

In Python, dictionary keys must be immutable and hashable. Immutable objects are those
that cannot be changed after their creation, and hashable objects are those that have a hash value that does not change during their lifetime.

📌 Example:

<pre><code class="language-py" >
# Lists cannot be keys (they're mutable)
invalid_dict = {
    [1, 2, 3]: "value"  # This raises TypeError
}
# Dictionaries cannot be keys
another_invalid = {
    {"a": 1}: "value"   # This raises TypeError
}
# Sets cannot be keys
also_invalid = {
    {1, 2, 3}: "value"  # This raises TypeError
}
</code></pre>

👣 Explanation:

- Lists in Python are mutable, which means their contents can change over time.
As a result, lists are not hashable, and therefore cannot be used as dictionary keys.
Attempting to use a list as a dictionary key will raise a `TypeError`.
- Dictionaries in Python are also mutable, as their key-value pairs can be changed, added, or removed.
Consequently, dictionaries are not hashable and cannot be used as keys in another dictionary.
Using a dictionary as a key will raise a `TypeError`.
- Sets are mutable collections of unique elements, and their contents can change.
Since sets are mutable, they are not hashable and cannot be used as dictionary keys.
Using a set as a key will raise a `TypeError`.

Always use appropriate data types for dictionary keys to avoid runtime errors.


### 🗝️  Best Practices for Choosing Keys

- Use strings when possible. They're the most common and readable choice
- Be consistent. Try to use the same type of keys throughout a dictionary
- Document special cases. If you need to use mixed key types, document why
- Float Keys. While legal, they can be tricky due to precision issues
- Tuple Keys. Make sure all elements in the tuple are immutable:

<pre><code class="language-py" >
# This works
good_dict = {(1, "a", True): "value"}

# This raises TypeError (list inside tuple is mutable)
bad_dict = {(1, [2, 3]): "value"}
</code></pre>


While Python offers great flexibility with dictionary keys, keeping things simple and consistent
will make your code more maintainable and less prone to errors.


## Checking Dictionary Type

Just like with any Python object, we can use the built-in `type()` function to confirm we're working with a dictionary.

<pre><code class="language-py" >
capitals = {
    "Greece": "Athens",
    "Italy": "Rome",
    "Spain": "Madrid"
}
# Check the type
print(type(capitals))

# You can also use isinstance() for type checking
is_dictionary = isinstance(capitals, dict)
print(is_dictionary)  # Returns True
</code></pre>

For dictionaries, the function `type()` returns `<class 'dict'>`.


This kind of type checking becomes especially valuable when working with dynamic data where the type might vary.

## Converting a Dictionary to a String

Sometimes, you need to convert a dictionary into a string — maybe to print it in a readable format, 
save it to a file, or send it over a network.

### Using str() for a Quick Conversion

If you just need a simple string representation, you can use Python’s built-in `str()` function:

<pre><code class="language-py" >
my_dict = {"name": "Alice", "age": 30, "city": "New York"}
print(str(my_dict))
</code></pre>

This works, but the output isn’t always the cleanest, especially if the dictionary is large or nested.
This format isn’t structured in a way that makes it easy to parse later.

### Pretty Printing with pprint

If you want a cleaner, more readable output (especially for nested dictionaries), the `pprint` module is a better option:

```python
import pprint
pprint.pprint(my_dict)
pprint.pprint(my_dict, sort_dict=False)
pprint.pp(my_dict)
```

By default, `pprint` sorts the dictionary by keys before formatting. 
To print the dictionary in the order of key insertion, use the `sort_dicts` boolean parameter or the `pp()` method.


Interested in more? Check out additional details about this library here: [pprint - Data pretty printer](https://docs.python.org/3/library/pprint.html)


### Converting to JSON with json.dumps()

If you’re working with APIs, storing data, or need structured output, `json.dumps()` is a great choice:

<pre><code class="language-py" >
import json

my_dict = {"name": "Alice", "age": 30, "city": "New York"}

json_string = json.dumps(my_dict, indent=4)
print(json_string)
</code></pre>

This method ensures the dictionary is formatted in valid JSON, making it ideal for saving or sharing data.

### Joining Key-Value Pairs as a Custom String

This approach is useful when you need a human-friendly, inline representation.

<pre><code class="language-py" >
my_dict = {"name": "Alice", "age": 30, "city": "New York"}

custom_string = ", ".join(f"{key}: {value}" for key, value in my_dict.items())

print(custom_string)
</code></pre>

### Using repr() 

`repr()` returns a string representation of an object that can be used to recreate it in code. 
This is useful for debugging and logging, but not ideal for human-readable output.

<pre><code class="language-py" >
my_dict = {"name": "Alice", "age": 30, "city": "New York"}
print(repr(my_dict))
</code></pre>

At first glance, it looks similar to `str()`, but `repr()` ensures the output is a valid Python expression 
that represents the object as closely as possible. 
This means that passing the result of `repr()` into `eval()` can  reconstruct the original object.

Each method serves a purpose, so pick the one that fits your use case best!

## Why Not Always Use a Dictionary Instead of a List?

Lists and dictionaries serve different purposes and each has its own advantages.

- Lists use less memory than dictionaries since they don't need to store key-value pairs and hash tables. For simple sequential data, lists are more space-efficient.
- Lists allow duplicate elements, while dictionary keys must be unique. If you need to track repeated items, use a list.
- If you primarily access elements in sequence or by numeric index, lists are more natural.

Using a dictionary for everything can slow your code down, make it harder to read, and use more resources than necessary.

🗝️  A good rule of thumb: Use a list when you have a collection of similar items in a sequence. Use a dictionary when you need to associate values with unique keys or need fast lookups by key.


## How to Check if a Dictionary is Empty

Often, you may need to check if a dictionary is empty before performing operations on it.

📌 1. Using `not` with a Dictionary

<pre><code class="language-py" >
my_dict = {}

if not my_dict:
    print("The dictionary is empty")
else:
    print("The dictionary is not empty")
</code></pre>

👣 Explanation:

- In Python, empty containers (lists, tuples, sets, dictionaries) evaluate to False in a Boolean context.
- If the dictionary is empty, `not my_dict` returns True, and the corresponding block of code executes.
- It is concise, readable, and efficient.

📌 2. Using `len()` Function

<pre><code class="language-py" >
my_dict = {}
if len(my_dict) == 0:
   print("The dictionary is empty")
</code></pre>

👣 Explanation:

- The `len()` function returns the number of key-value pairs in the dictionary.
- If `len(my_dict) == 0`, it confirms that the dictionary is empty.
- This method is explicit but slightly less Pythonic than using `not`.

📌 3. Comparing with an Empty Dictionary

<pre><code class="language-py" >
my_dict = {}
if my_dict == {}:
   print("The dictionary is empty")
</code></pre>

👣 Explanation:

- This method explicitly checks if `my_dict` is equal to `{}`.
- While this approach works, it is not as efficient as using not because it performs a comparison operation.



## 🧐   FAQs on Python Dictionaries

### What is a dictionary in Python and how do I create one?

A dictionary is a collection of key-value pairs. You can create one using curly braces {} or the `dict()` constructor.

```python
user1 = {'name': 'John', 'age': 30}
user2 = dict(name='John', age=30)
user3 = dict([("name", "John"), ("age", 30)])
user4 = dict(zip(['name', 'age'], ["John", 30]))
user5 = dict.fromkeys(['name', 'age'])
```

###  What types can I use as dictionary values?

Any Python object can be a dictionary value, including:

- Numbers, strings, lists
- Other dictionaries
- Custom objects
- Functions
- None


### What types can I use as dictionary keys?

Only immutable types can be dictionary keys, including:

- Strings
- Numbers (integers, floats)
- Tuples (if they contain only immutable elements)
- Frozensets

Lists, dictionaries, and sets cannot be used as keys because they are mutable.

### Can a tuple be used as a dictionary key?

Yes, a tuple is a hashable value and can be used as a dictionary key.
The following code example shows a dictionary with keys representing a simple x,y grid system.

<pre><code class="language-py" >
coordinates = { (0,0) : 100, (1,1) : 200}
coordinates[(1,0)] = 150
coordinates[(0,1)] = 125

print(coordinates)
</code></pre>


### How does Python handle duplicate keys in dictionaries?

If you try to add a duplicate key, the new value will overwrite the old one. The last assignment wins:


```python
my_dict = {'a': 1, 'a': 2}  # Results in {'a': 2}
```

### How to sum the values of a dictionary

You can achieve this using a variety of methods.

Method 1: Using `sum()` with the `values()` method

<pre><code class="language-py" >
my_dict = {'a': 10, 'b': 20, 'c': 30}

total = sum(my_dict.values())
print(f"Total sum of values: {total}")
</code></pre>

Method 2: Using a loop

<pre><code class="language-py" >
my_dict = {'a': 10, 'b': 20, 'c': 30}

total = 0
for value in my_dict.values():
    total += value

print(f"Total sum of values using loop: {total}")
</code></pre>

Method 3: Using list comprehension

<pre><code class="language-py" >
my_dict = {'a': 10, 'b': 20, 'c': 30}

total = sum(my_dict[i] for i in my_dict)
print(f"Total sum of values using list comprehension: {total}")
</code></pre>

Method 3a: Using list comprehension for nested dictionaries

<pre><code class="language-py" >
nested_dict = {  
    'group1': {'item1': 10, 'item2': 20},  
    'group2': {'item3': 30, 'item4': 40}  
}

total = sum(sum(v for v in inner_dict.values()) 
                  for inner_dict in nested_dict.values())
print(f"Total sum of nested values: {total}")
</code></pre>


Method 4: Using the Lambda Function

<pre><code class="language-py" >
import functools
my_dict = {'a': 10, 'b': 20, 'c': 30}

total = functools.reduce(lambda x, y: x+y, my_dict.values(), 0)

print(f"Total sum of values using the lambda function: {total}")
</code></pre>

Method 5: Using `operator.add` With Reduce

<pre><code class="language-py" >
from functools import reduce
from operator import add
my_dict = {'a': 10, 'b': 20, 'c': 30}

total = reduce(add, my_dict.values())
print(f"Total sum of values using the lambda function: {total}")
</code></pre>


Method 6: Using Pandas

<pre><code class="language-py" >
import micropip
await micropip.install("pandas")

import pandas as pd
my_dict = {'a': 10, 'b': 20, 'c': 30}

series = pd.Series(my_dict)
total = series.sum()
print(f"Total sum of values using Pandas: {total}")
</code></pre>

All these methods will give you the sum of the values in the dictionary.
But if your dictionary contains non-numeric values (e.g., strings, lists, `None`),
attempting to sum the values will raise a `TypeError`.

Note that `sum(my_dict)` will try to sum the keys of the dictionary
(since `my_dict` in an iteration context yields its keys).
This will cause a `TypeError` because the keys are strings and cannot be summed directly.

