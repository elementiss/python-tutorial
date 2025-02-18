# Python - Loop Dictionaries

You can iterate over key-value pairs within the dictionary and perform operations on each pair. 


There are several ways for looping through dictionaries:

- Using a for Loop
- Using `dict.items()` method
- Using `dict.keys()` method
- Using `dict.values()` method


## Iterating over Keys

If you use a dictionary in a for statement, it traverses the keys of the dictionary.
This behavior is both intuitive and efficient, as keys are often the primary points of reference in dictionary-based operations. 


<pre><code class="language-py">
capitals = {
  "Greece": "Athens", 
  "Italy": "Rome",
  "Spain": "Madrid"  
}
# print dictionary keys one by one
for country in capitals:
    print(country)
</code></pre>

You don't need any special methods or complex syntax - the dictionary itself is directly iterable. 

Since you're only working with keys, Python doesn't need to load or process the associated values unless specifically requested. 
This can be particularly beneficial when dealing with large dictionaries.

You can update values inside the loop. In this example, we loop through the dictionary data 
and double each of its values. 

📌 Example:

<pre><code class="language-py">
data = {"a": 1, "b": 2, "c": 3}  
for key in data:  
    data[key] *= 2  
print(data)  # Output: {'a': 2, 'b': 4, 'c': 6}  
</code></pre>

👣 Explanation:

- We start with a dictionary data that has three key-value pairs.
- The `for` loop iterates over each key in the dictionary data.
- The variable `key` takes on each key in the dictionary sequentially ("a", then "b", and finally "c").
- For each key in the dictionary, we access its value using `data[key]` and multiply it by 2.
- The `*=` operator is shorthand for `data[key] = data[key] * 2`.
- Then we print the updated dictionary.

All values in the dictionary have been doubled.


## Iterating over Key-Value Pairs

To print the keys and values, we can loop through the keys and look up the corresponding values.

<pre><code class="language-py" >
capitals = {
  "Greece": "Athens", 
  "Italy": "Rome",
  "Spain": "Madrid"  
}
for key in capitals:
    value = capitals[key]
    print(key, value)
</code></pre>

Let's consider a more concise way to do the same thing with `items()` method.

<pre><code class="language-py">
capitals = {
  "Greece": "Athens", 
  "Italy": "Rome",
  "Spain": "Madrid"  
}
for key, value in capitals.items():
    print(key, value)
</code></pre>

The `items()` method returns a special view of your dictionary's contents, presenting each key-value pair as a tuple. 

You don't need to perform separate operations to access keys and values - everything is available in one go. 
Python automatically unpacks each key-value pair, making them readily available for use within your loop.

This method creates a dynamic view of the dictionary entries. 
This means if you modify the original dictionary, the view will automatically reflect these changes. 
It's like having a live camera feed of your dictionary's contents rather than a static photograph.

The `items()` method is also memory-efficient. 
Instead of creating a new list of all key-value pairs, it provides a view object that acts as a window into your dictionary. 
This is particularly important when working with large dictionaries where memory usage needs to be considered.

In practical applications, `items()` proves invaluable when you need to compare dictionaries, search for specific key-value combinations, or transform dictionary data into other formats.


## Iterating over Values

The `values()` method provides direct access to the content stored within our dictionary structure. The `values()` method 
creates a dynamic view of your dictionary's values, allowing you to work with the stored information without needing to reference its corresponding keys. 
In our capital cities example, this means we can directly access and process the capital names without dealing with their associated countries.

<pre><code class="language-py">
capitals = {
  "Greece": "Athens", 
  "Italy": "Rome",
  "Spain": "Madrid"  
}
for value in capitals.values():
    print(value)
</code></pre>


Just like looking through a photo album where you're only interested in the pictures themselves rather than their captions, 
`values()` lets you concentrate on the content. 

In practical scenarios, you might use this method when generating reports that only need the stored values, 
validating data contents, or creating lists of available options.


## list() Function

`list()` is a built-in function in Python. 
It is used to create a new list from any iterable such as tuples, strings, dictionaries, or other lists.

For dictionaries, `list(dict)` extracts the keys from the dictionary and puts them in a list.

📌 Example:

<pre><code class="language-py">
user = {"name": "Hanna", "age": 10, "processed": False}
my_list = list(user)
print(my_list)
# Output: ['name', 'age', 'processed']
</code></pre>

It is useful when you need to work with the dictionary's keys as a separate list for further operations, 
such as iteration, transformations, or filtering.

### Difference Between dict.keys() and list(dict)

Although both expressions are used in a similar way, there are significant differences between them.

| Feature | `dict.keys()` | `list(dict)` | 
|-|--|--|
| Return Type | returns a `dict_keys` view object | returns a new list object containing all keys |
| Memory Usage | creates a lightweight view that doesn't copy the keys | creates a new list in memory with copies of all the keys |
| Dynamic Updates | A `dict_keys` view reflects changes to the original dictionary | A list created with `list(dict)` is static and won't update when the dictionary changes |
| Performance | faster | slower | 

### The Difference in Performance

For large dictionaries, the difference in performance can be substantial. 

📌 This code snippet demonstrates the difference in performance between creating a keys view object 
and copying dictionary keys to a new list.

<pre><code class="language-py">
import time
big_dict = {i: i*10 for i in range(5_000_000)}
 
# Quick operation - only creates a view object
start_time = time.perf_counter()
keys_view = big_dict.keys()  
view_time = time.perf_counter() - start_time
 
# Slow operation - copies elements to a new list
start_time = time.perf_counter()
keys_list = list(big_dict)
list_time = time.perf_counter() - start_time

print(f"List time: {list_time:.6f} seconds")
print(f"View time: {view_time:.6f} seconds")
</code></pre>

👣 Explanation:

- The `time` module is imported to measure the time taken for different operations.
- A large dictionary `big_dict` is created using dictionary comprehension. 
It contains 5 million key-value pairs where each key `i` is mapped to the value `i*10`.
- `start_time` records the current time before creating the view
- `keys_view = big_dict.keys()` creates a view object of the dictionary's keys. 
This is a quick operation because it doesn't involve copying the keys to a new structure.
- `view_time` calculates the elapsed time by subtracting `start_time` from the current time after the operation.
- Similarly, `start_time` records the current time before converting the dictionary keys to a list.
- `keys_list = list(big_dict)` converts the dictionary keys into a new list. 
This is a slower operation because it involves copying each key from the dictionary to a list.
- `list_time` measures the time taken for this operation.
- The times taken for both operations are printed in seconds, with six decimal places for precision.

Output:

```
List time: 0.056749 seconds
View time: 0.000002 seconds
```

💡 Note that actual times will vary depending on your computer's specifications, python version, system load.


As you can see, creating a list from the dictionary keys is slower than getting a view of the keys. This is because:

1. `dict.keys()` is an O(1) operation for creating a view object + some overhead costs for initialization, proportional to the size.
2. `list(dict)` is an O(n) operation - it must copy each key, so the time increases linearly with the number of keys.

### The Difference in Memory Usage

📌 This code snippet demonstrates the difference in memory usage between creating a keys view object 
and copying dictionary keys to a new list.

<pre><code class="language-py">
import micropip
await micropip.install('pympler')

from pympler import asizeof
import gc

def measure_memory_usage(operation, name):
    gc.collect()                
    before = asizeof.asizeof([])
    result = operation()        
    after = asizeof.asizeof([result]) 
    memory_used = after - before 
    
    print(f"{name} uses approx. {memory_used} bytes")
    return result

n = 1_000_000
big_dict = {i: i*10 for i in range(n)}

keys_view = measure_memory_usage(lambda: big_dict.keys(), "dict.keys()")
keys_list = measure_memory_usage(lambda: list(big_dict), "list(dict)")
</code></pre>

Output:

```
dict.keys() uses approx. 24 bytes
list(dict) uses approx. 20000032 bytes
```

👣 Explanation:

- Importing Modules:
  - The `pympler.asizeof` from the `pympler` library provides a function that calculates the memory size of a Python object.
  - The `gc` module provides an interface to the automatic garbage collection facility in Python.
- `measure_memory_usage` is a function that takes an operation (as a lambda function) and its name (as a string) as arguments.
- `gc.collect()` forces the garbage collector to release unreferenced memory before measuring to ensure accurate results.
- `asizeof.asizeof([])` measures and stores the memory size of an empty list, serving as a baseline.
- Next line executes the passed operation and stores the result.
- Then we measure and store the memory size of a list containing the result of the operation.
- Finally we print the name of the operation and the approximate memory used in bytes.

When you call `dict.keys()` on a Python dictionary, you get a dictionary view object. 
This view references the dictionary’s key set without creating a separate data structure, 
so it requires only a small amount of memory (24 bytes in this example).

However, when you use `list(dict)` и and similar `sorted(dict)` function, Python generates an actual list containing a copy 
of all the keys from the dictionary. This list must allocate space for every key object, 
leading to a significantly larger memory footprint (around 20 MB for one million entries).


### When to Use Each Method

#### Use `dict.keys()` when:
- You only need to iterate over the keys
- You want to check for key existence with the `in` operator
- You need a dynamic view that reflects dictionary changes
- Performance and memory usage are concerns

#### Use `list(dict)` when:
- You need list-specific operations like indexing or slicing
- You want to modify the collection of keys without affecting the dictionary
- You need a static snapshot of the keys at a specific moment

While both methods provide access to dictionary keys, understanding 
the performance implications can help you write more efficient Python code. 



## 🧐   FAQs on Loop Dictionaries

### How can I loop through dictionary keys in a specific order? 

You can sort dictionary keys before looping using `sorted()`. For example:
 
<pre><code class="language-py">
data = {"b": 2, "a": 1, "c": 3}  
for key in sorted(data):  
    print(key, ":", data[key]) 
</code></pre>

To loop in reverse order, use `sorted(dict.keys(), reverse=True)`. 

<pre><code class="language-py">
d = {"b": 2, "a": 1, "c": 3}  
# Sorted by values
for key, value in sorted(d.items(), key=lambda item: item[1]): 
    print(key, value)
</code></pre>

Since Python 3.7, dictionaries maintain insertion order.


### Is it more efficient to use dict.items() or separate key/value access in loops?

Using `dict.items()` is generally more efficient than accessing keys and values separately in a loop 
because it avoids multiple dictionary lookups.

### What happens if I try to add or remove items while looping through a dictionary?

Modifying a dictionary's size (adding or removing items) while iterating through it can raise a 
*RuntimeError: dictionary changed size during iteration*.
It's better to create a list of changes and apply them after the loop, or use a dictionary comprehension.

<pre><code class="language-py">
capitals = {
  "Greece": "Athens", 
  "Italy": "Rome",
  "Spain": "Madrid"  
}
for key in capitals:
    if key == 'Italy':
      del capitals["Greece"]
    print(key)
</code></pre>
