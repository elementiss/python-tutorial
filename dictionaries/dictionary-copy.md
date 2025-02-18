# Python - Dictionary Copying: Shallow and Deep Copy


For effective data management, it is important to know how to copy dictionaries properly.
This concept can be illustrated with a simple dictionary of European capitals.



## Shallow Copy

The simplest way to copy a dictionary is using what we call a "shallow copy". 
You can create a shallow copy in two ways. The first method uses the `dict.copy()` method:

<pre><code class="language-py">
capitals = {
    "Greece": "Athens",
    "Italy": "Rome",
    "Spain": "Madrid"
}
new_capitals = capitals.copy()
print(new_capitals)
print(capitals)
</code></pre>

Shallow copies create a new dictionary, but they don't create copies of the nested objects 
if your dictionary contains any. In our simple capitals example, this isn't a problem because we 
only have strings, which are immutable.

Now, consider a more complex scenario involving nested dictionaries:

<pre><code class="language-py" >
country_info = {
    "Greece": {
        "capital": "Athens",
        "population": 10.7
    }
}
print(country_info)
</code></pre>

In such cases, a shallow copy might not be sufficient, and this is where deep copying comes into play. 

## Deep Copy

To create a deep copy, we need to import Python's `copy` module and use its `deepcopy` function:

<pre><code class="language-py">
import copy
country_info = {
    "Greece": {
        "capital": "Athens",
        "population": 10.7
    }
}
new_country_info = copy.deepcopy(country_info)
print(new_country_info)
</code></pre>


The deep copy creates a completely independent copy of the original dictionary, including all nested objects. This means you can modify any level of the new dictionary without affecting the original one.

To illustrate the difference, we will observe what happens when when we modify our dictionaries:

<pre><code class="language-py">
# With shallow copy
capitals = {"Greece": "Athens", "Italy": "Rome"}
new_capitals = capitals.copy()
new_capitals["Greece"] = "Thessaloniki"
print(capitals)      
# Still shows {"Greece": "Athens", "Italy": "Rome"}
print(new_capitals)  
# Shows {"Greece": "Thessaloniki", "Italy": "Rome"}
</code></pre>

Remember that shallow copies are usually sufficient for simple dictionaries with immutable values 
like strings and numbers. However, when working with nested data structures, 
consider using deep copy to ensure complete independence between the original and copied data.


<pre><code class="language-py" >
import copy
# Dictionary with nested structure
countries = {
    "Greece": {
        "cities": ["Athens", "Thessaloniki"]
    },
    "Italy": {
        "cities": ["Rome", "Milan"]
    }
}
# Creating shallow and deep copies
shallow_copy = countries.copy()
deep_copy = copy.deepcopy(countries)

# Let's modify the nested list in the shallow copy
shallow_copy["Greece"]["cities"].append("Patras")

print("Original dict:", countries["Greece"]["cities"])
# Output: ['Athens', 'Thessaloniki', 'Patras']

print("Shallow copy:", shallow_copy["Greece"]["cities"])
# Output: ['Athens', 'Thessaloniki', 'Patras']

print("Deep copy:", deep_copy["Greece"]["cities"])
# Output: ['Athens', 'Thessaloniki']
</code></pre>


In this example, when we modify the nested list in the shallow copy, 
the change is also reflected in the original dictionary because both dictionaries 
reference the same nested list. However, the deep copy remains unchanged because 
it created independent copies of all nested objects. 


The choice between shallow and deep copying often depends on your specific needs: 
shallow copies are more memory-efficient and faster, 
while deep copies provide complete data independence but consume more memory and processing power.

## Use of the Assignment Operator: Reference Copy 

We will examine what happens when the assignment operator (=) is used with dictionaries:

<pre><code class="language-py">
capitals = {
    "Greece": "Athens",
    "Italy": "Rome"
}
# Using assignment operator
new_capitals = capitals

# Modifying the new dictionary
new_capitals["Greece"] = "Thessaloniki"

print("Original dictionary:", capitals)
# Output: {'Greece': 'Thessaloniki', 'Italy': 'Rome'}

print("New dictionary:", new_capitals)
# Output: {'Greece': 'Thessaloniki', 'Italy': 'Rome'}

# Checking if they reference the same object
print(id(capitals) == id(new_capitals))  # Output: True
</code></pre>

When using the assignment operator (=), Python doesn't create a new dictionary. 
Instead, it creates a new reference to the same dictionary object in memory. 
This means both variables (`capitals` and `new_capitals`) point to exactly the same dictionary. 
Any changes made using either variable will affect the dictionary that both variables reference. 
This is often called a "reference copy" or "aliasing" rather than an actual copy of the data. 
This behavior can lead to unexpected results if you're not aware of it, 
which is why proper copying methods (shallow or deep) should be used when you need an independent copy of a dictionary.



## Comparative Table of Different Dictionary Copying Methods

| Feature | Reference Copy | Shallow Copy | Deep Copy |
|--|---|---|---|
| Syntax | `dict2 = dict1` | `dict2 = dict1.copy()` or `dict2 = dict(dict1)` | `import copy` `dict2 = copy.deepcopy(dict1)`|
| Definition      | Creates a new reference to the same object | Creates a new dictionary with references to the same nested objects | Creates a completely new dictionary with new copies of all nested objects |
| Nested Objects  | Changes affect both dictionaries | Changes to nested objects affect both dictionaries | Changes to nested objects are completely independent |
| Performance     | Fastest | Moderate speed | Slowest |
| Use Case        | When you need just another reference to the same dictionary | When dictionary contains only immutable objects (strings, numbers, tuples) | When dictionary contains mutable objects (lists, dictionaries) and you need full independence |
| Changes to Original | Affects both dictionaries | Affects only top-level elements | Doesn't affect original dictionary at all |
| Memory Usage    | Lowest (single object) | Medium (new dictionary, same nested objects) | Highest (complete copy of all objects) |


## 🧐   FAQS on Dictionary Copying in Python

### What is the difference between a shallow copy and a deep copy of a dictionary in Python?

A shallow copy (created with `dict.copy()` or via the `dict()` constructor) duplicates only the top-level 
structure of the dictionary. However, any nested objects, such as lists or other dictionaries, 
remain references to the same original objects. 

A deep copy (created with `copy.deepcopy()`) recreates all nested objects, ensuring 
that no references point back to the original dictionary’s contents.

### Can I perform a shallow copy using list slicing on a dictionary?

No. Python’s slicing syntax (e.g., `some_list[:]`) applies to sequence types like lists, 
tuples, or strings, not dictionaries. For shallow dictionary copying, 
you can use `dict.copy()`, the `dict()` constructor, or other methods like `{k: v for k, v in original_dict.items()}`.

### Will using the assignment operator (=) create a copy of my dictionary?

No. Using the assignment operator on a dictionary only creates a new reference 
to the same dictionary object in memory. Any changes made through one reference 
will be visible in the other. If you actually need a copy, you must 
use an explicit copy method (`dict.copy()` or `copy.deepcopy()`, depending on your needs).

### What is the most efficient way to copy a dictionary in Python?

For a shallow copy, `dict.copy()` is the most efficient method. For a deep copy, use `copy.deepcopy()`, 
but be aware that it is slower due to the recursive copying of nested objects.

