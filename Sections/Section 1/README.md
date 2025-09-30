# Introduction To Python

### What is python?
- Python is a high-level, general-purpose programming language.
Its design philosophy emphasizes code readability with the use of significant indentation.
- Python is dynamically type-checked and garbage-collected.
- Python consistently ranks as one of the most popular programming languages, and it has gained widespread use in the machine learning community. It is widely taught as an introductory programming language.

### What is anaconda and why we need it?
- Anaconda is an open-source distribution platform and ecosystem for data science,
machine learning, and AI that simplifies managing Python and R programming languages,
their packages, and environments.
- It includes a powerful package and environment manager called conda,
a graphical user interface called Anaconda Navigator for managing projects without the command line,
and comes with over 250 pre-installed essential data science packages.
- Anaconda streamlines the process of setting up and maintaining development environments,
making data science workflows more accessible and efficient.  


- How does python run (interpreter)
- Script vs CLI vs Notebook
- Installing python (anaconda)

## Getting started
### Whitespace Formatting

Many languages use curly braces to delimit blocks of code. Python uses indentation:
```python
for i in [1, 2, 3, 4, 5]:
    print(i)            # first line in "for i" block
    for j in [1, 2, 3, 4, 5]:
        print(j)        # first line in "for j" block
        print(i + j)    # last line in "for j" block
    print(i)            # last line in "for i" block
print("done looping")
```

This makes Python code very readable, but it also means that you have to be very careful with your formatting.
Whitespace is ignored inside parentheses and brackets, which can be helpful for long-winded computations:

```python
long_winded_computation = (1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10 + 11 + 12 +
13 + 14 + 15 + 16 + 17 + 18 + 19 + 20)
```

and for making code easier to read:
```python
list_of_lists = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
easier_to_read_list_of_lists = [ [1, 2, 3],
                                 [4, 5, 6],
                                 [7, 8, 9] ]
```


### Modules

Certain features of Python are not loaded by default.
These include both features included as part of the language as well as third-party features that you download yourself. In order to use these features, you’ll need to import the modules that contain them.
One approach is to simply import the module itself:

```python
import numpy
my_array = numpy.ones(3)
```

Here re is the module containing functions and constants for working with arrays.
After this type of import you can only access those functions by prefixing them with `numpy.`.
If you already had a different re in your code you could use an alias:

```python
import numpy as np
my_array = np.ones(3)
```

You might also do this if your module has an unwieldy name or if you’re going to be typing it a lot.
For example, when visualizing data with `matplotlib`, a standard convention is:
```python
import matplotlib.pyplot as plt
```

If you need a few specific values from a module, you can import them explicitly and use them without qualification:

```python
from collections import defaultdict, Counter
lookup = defaultdict(int)
my_counter = Counter()
```

If you were a bad person, you could import the entire contents of a module into your namespace, which might inadvertently overwrite variables you’ve already defined:

```python
match = 10
from re import *    # uh oh, re has a match function
print match         # "<function re.match>"
```

However, since you are not a bad person, you won’t ever do this.


### Functions
A function is a rule for taking zero or more inputs and returning a corresponding output.
In Python, we typically define functions using def:
```python
def double(x):
    """this is where you put an optional docstring
    that explains what the function does.
    for example, this function multiplies its input by 2"""
    return x * 2
```

Python functions are first-class, which means that we can assign them to variables and pass them into functions just like any other arguments:

```python
def apply_to_one(f):
    """calls the function f with 1 as its argument"""
    return f(1)
my_double = double          # refers to the previously defined function
x = apply_to_one(my_double) # equals 2
```

Function parameters can also be given default arguments, which only need to be specified when you want a value other than the default:
```python
def my_print(message="my default message"):
    print(message)

my_print("hello") # prints 'hello'
my_print() # prints 'my default message'
```

It is sometimes useful to specify arguments by name:
```python
def subtract(a=0, b=0):
    return a - b

subtract(10, 5) # returns 5
subtract(0, 5) # returns -5
subtract(b=5) # same as previous
```

We will be creating many, many functions.

### String

Strings can be delimited by single or double quotation marks (but the quotes have to match):

```python
single_quoted_string = 'data science'
double_quoted_string = "data science"
```

Python uses backslashes to encode special characters. For example:

```python
tab_string = "\t"   # represents the tab character
len(tab_string)     # is 1
```

If you want backslashes as backslashes (which you might in Windows directory names or in regular expressions), you can create raw strings using `r""`:

```python
not_tab_string = r"\t"  # represents the characters '\' and 't'
len(not_tab_string)     # is 2
```

You can create multiline strings using `triple-[double-]-quotes`:
```python
multi_line_string = """This is the first line.
and this is the second line
and this is the third line"""
```

### Exception

When something goes wrong, Python raises an exception.
Unhandled, these will cause your program to crash.
You can handle them using try and except:

```python
try:
    print 0 / 0
except ZeroDivisionError:
    print "cannot divide by zero"
```

Although in many languages exceptions are considered bad, in Python there is no shame in using them to make your code cleaner, and we will occasionally do so.

### Lists

Probably the most fundamental data structure in Python is the list.
A list is simply an ordered collection. (It is similar to what in other languages might be called an array, but with some added functionality.)

```python
integer_list = [1, 2, 3]
heterogeneous_list = ["string", 0.1, True]
list_of_lists = [ integer_list, heterogeneous_list, [] ]

list_length = len(integer_list) # equals 3
list_sum = sum(integer_list)    # equals 6
```

You can get or set the nth element of a list with square brackets:
```python
x = range(10)   # is the list [0, 1, ..., 9]
zero = x[0]     # equals 0, lists are 0-indexed
one = x[1]      # equals 1
nine = x[-1]    # equals 9, 'Pythonic' for last element
eight = x[-2]   # equals 8, 'Pythonic' for next-to-last element
x[0] = -1       # now x is [-1, 1, 2, 3, ..., 9]
```

You can also use square brackets to “slice” lists:

```python
first_three = x[:3]                 # [-1, 1, 2]
three_to_end = x[3:]                # [3, 4, ..., 9]
one_to_four = x[1:5]                # [1, 2, 3, 4]
last_three = x[-3:]                 # [7, 8, 9]
without_first_and_last = x[1:-1]    # [1, 2, ..., 8]
copy_of_x = x[:]                    # [-1, 1, 2, ..., 9]
```

Python has an in operator to check for list membership:
```python
1 in [1, 2, 3] # True
0 in [1, 2, 3] # False
```

This check involves examining the elements of the list one at a time, which means that you probably shouldn’t use it unless you know your list is pretty small (or unless you don’t care how long the check takes).
It is easy to concatenate lists together:

```python
x = [1, 2, 3]
x.extend([4, 5, 6]) # x is now [1,2,3,4,5,6]
```

If you don’t want to modify x you can use list addition:

```python
x = [1, 2, 3]
y = x + [4, 5, 6] # y is [1, 2, 3, 4, 5, 6]; x is unchanged
```

More frequently we will append to lists one item at a time:

```python
x = [1, 2, 3]
x.append(0) # x is now [1, 2, 3, 0]
y = x[-1]   # equals 0
z = len(x)  # equals 4
```

It is often convenient to unpack lists if you know how many elements they contain:

```python
x, y = [1, 2] # now x is 1, y is 2
```

although you will get a ValueError if you don’t have the same numbers of elements on both sides.
It’s common to use an underscore for a value you’re going to throw away:

```python
_, y = [1, 2] # now y == 2, didn't care about the first element
```


### Tuples

Tuples are lists’ immutable cousins.
Pretty much anything you can do to a list that doesn’t involve modifying it, you can do to a tuple.
You specify a tuple by using parentheses (or nothing) instead of square brackets:

```python
my_list = [1, 2]
my_tuple = (1, 2)
other_tuple = 3, 4
my_list[1] = 3 # my_list is now [1, 3]
try:
    my_tuple[1] = 3
except TypeError:
    print "cannot modify a tuple"
```
Tuples are a convenient way to return multiple values from functions:
```python
def sum_and_product(x, y):
    return (x + y),(x * y)
sp = sum_and_product(2, 3)      # equals (5, 6)
s, p = sum_and_product(5, 10)   # s is 15, p is 50
```

Tuples (and lists) can also be used for multiple assignment:
```python
x, y = 1, 2 # now x is 1, y is 2
x, y = y, x # Pythonic way to swap variables; now x is 2, y is 1
```


### Dictionaries

Another fundamental data structure is a dictionary, which associates values with keys
and allows you to quickly retrieve the value corresponding to a given key:

```python
empty_dict = {} # Pythonic
empty_dict2 = dict() # less Pythonic
grades = { "Joel" : 80, "Tim" : 95 } # dictionary literal
```

You can look up the value for a key using square brackets:

```python
joels_grade = grades["Joel"] # equals 80
```

But you’ll get a KeyError if you ask for a key that’s not in the dictionary:
```python
try:
    kates_grade = grades["Kate"]
except KeyError:
    print "no grade for Kate!"
```

You can check for the existence of a key using in:

```python
joel_has_grade = "Joel" in grades # True
kate_has_grade = "Kate" in grades # False
```

Dictionaries have a get method that returns a default value (instead of raising an exception) when you look up a key that’s not in the dictionary:

```python
joels_grade = grades.get("Joel", 0)  # equals 80
kates_grade = grades.get("Kate", 0)  # equals 0
no_ones_grade = grades.get("No One") # default default is None
```

You assign key-value pairs using the same square brackets:

```python
grades["Tim"] = 99          # replaces the old value
grades["Kate"] = 100        # adds a third entry
num_students = len(grades)  # equals 3
```

We will frequently use dictionaries as a simple way to represent structured data:
```python
tweet = {
"user" : "joelgrus",
"text" : "Data Science is Awesome",
"retweet_count" : 100,
"hashtags" : ["#data", "#science", "#datascience", "#awesome", "#yolo"]
}
```
Besides looking for specific keys we can look at all of them:
```python
tweet_keys = tweet.keys()       # list of keys
tweet_values = tweet.values()   # list of values
tweet_items = tweet.items()     # list of (key, value) tuples
"user" in tweet_keys            # True, but uses a slow list in
"user" in tweet                 # more Pythonic, uses faster dict in
"joelgrus" in tweet_values      # True
```

Dictionary keys must be immutable; in particular, you cannot use lists as keys.
If you need a multipart key, you should use a tuple or figure out a way to turn the key into a string.
