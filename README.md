## Python 2 or 3? 

For people new to python one of the main issues they first have to surpass is which version to use; either 2.7 or 3.x. Python 3.0 was released in 2008 but despite having many nice new features has encountered slow adoption rates. One of the key reasons being breaking changes causing packages not to update creating a vicious cycle of not updating because your dependencies' dependency is not updated. I will not go too much into this but if you have some grasp of what you are doing or want to be doing you can check the status of the more popular dependencies on [Python3 Wall of Superpowers](https://python3wos.appspot.com/). As to why you should use 3 over 2 there are many blog posts already in existence such as Eev.ee’s  [PythonFAQ: Why should I use Python 3?](https://eev.ee/blog/2016/07/31/python-faq-why-should-i-use-python-3/) and from the python wiki: [Python2orPython3](https://wiki.python.org/moin/Python2orPython3).

A couple key differences you may notice right away would be:

* In python 2 integer division is the default so 5/2 would give you 2 where as in python 3 you are required to specifically request integer division with //.
* print is now a function in python 3 and must be called with print(str)
* Strings are now unicode by default 

For this whatever this is I will be using Python 3.5 because apparently that’s what I have installed. Python 3.6 has added some nice sugar,and I think I have been unable to get Apache to run with python 3.5 in windows but that constraint is irrelevant for now. 

Once you decide which version of python you want you can go
to <https://www.python.org/downloads/>
and download the correct version for your architecture. To note 32-bit python
can only use 2GB of memory if I recall correctly so be careful you do not
accidentally download that one.

## Which IDE to use:

Now that you have decided what version to use must next
decide on an IDE. I personally like Pycharm produced by JetBrains the makers of
Resharper. Students form most Universities can get the professional edition for
free on a renewing 1-year basis or just use the community edition (I will
provide a link in the resources section of this still not sure what to call it).
Other options include Eclipse, notepad++, idle, VisualCode, atom, sublime,
etc.. Pycharm’s darcula colour scheme is my favourite by far so I will be using
that when I need to include screen shots. 

## Some resources that might be useful: 

* https://www.jetbrains.com/student/
* https://education.github.com/pack
* https://git-scm.com/downloads 
* https://sourceforge.net/projects/kdiff3/files/
* https://notepad-plus-plus.org/download/v7.5.1.html 
* https://code.visualstudio.com/ 

# Standards 
There are two main guidelines for styling python code PEP-8 and the Google Sytyle Guide. Some main takeaways are:
* **VARIABLE NAMES**
	* CONSTANTS_ARE_ANGRY_SNAKECASE
	* ClassesAreUpperCamelCase
	* modules_are_snake_case
	* functions_are_snake_case
	* variables_are_snake_case
	* _private_variables_are_undescored_first
	* __obsfucated_variables_should_be_avoided
	* unwanted_shadows_
	* \_\_to_override_built_ins\_\_ (\_\_open\_\_)
* 4 spaces for indentation 
* order imports std library, 3rd party, in house packages, application packages
	* Avoid from package import * as it makes it unclear where functions are from
* Use Pycharm to add docstrings and document your functions
* Avoid unessary new lines
* use `is None` and `is True`
* With python 3.6+ You can use type hinting in function names but ensure you do not need to support backwards compatibility
* Options for string creation
```python
# f strings python 3.6+
x = 'World'
print(f'Hello {world}')

#str.format()
"First, thou shalt count to {0}".format(10) # References first positional argument
"Bring me a {}".format('Cookie') # Implicitly references the first positional argument
"From {} to {}".format('zero', 'hero')    # Same as "From {0} to {1}"
"My quest is {name}".format(name='to pet dragons') # References keyword argument 'name'

```

# Main Data types
## [Strings](https://docs.python.org/3/library/stdtypes.html#string-methods)
**Immutable but sliceable series of characters.**

Strings can be quoted with ', ", ''', or """. Triple quotes will allow you to spread across multiple lines.
```python
foo = 'foo'
bar = "bar's"
foo_bar_ra = '''
	FOO
	BAR
	RAA
'''
```
You can slice strings as you would an array.
```python
my_string = 'Hello My Name Is Joe And I work in a Button Factory'
print(my_string[0]) # -> H
print(my_string[0:5]) # -> Hello
print(my_string[5:]) # -> My Name Is Joe And I work in a Button Factory
print(my_string[-1]) # -> y
```
The most efficient way to concatenate strings is to use .join instead of +
```python
my_string_p2 = 'I have a wife and a kid and a family.'
full_string = '. '.join([my_string, my_string_p2])
print(full_string) # Hello My Name Is Joe And I work in a Button Factory. I have a wife and a kid and a family.
```
It is usually a good idea when comparing to use functions like .lower()
```python
	x, y = 'Timmy.Ghost', 'timmy.ghost'
	x == y # False
	x.lower() == y.lower() # True
```
```str.strip()``` should be used to sanitize input text and removes extraneous spaces and new lines characters.

```len(str)``` is used to get the length of a string

Documentation for other functions such as .upper, .index(), .find(), .isalpha(), .isdigit(), .replace()

## [Numbers](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)
Python will generally handle datatype conversion of numbers for you minus instances like 2 / 5 in python 2.7 being integer division by default.

| Operation | Result |
| ----------- | ------ |
| ```x + y``` | sum of x and y |
| ```x - y``` | difference of x and y |
| ```x * y``` | product of x and y |
| ```x / y``` | quotient of x and y |
| ```x // y``` | floored quotient of x and y |
| ```x % y``` | remainder of x / y |
| ```-x``` | x negated |
| ```+x``` | x unchanged |
| ```abs(x)``` | absolute value or magnitude of x |
| ```int(x)``` | x converted to integer |
| ```float(x)``` | x converted to floating point |
| ```complex(re, im)``` | a complex number with real part re, imaginary part im. im defaults to zero. |
| ```c.conjugate()``` | conjugate of the complex number c |
| ```divmod(x, y)``` | the pair (x // y, x % y) |
| ```pow(x, y)``` | x to the power y |
| ```x ** y``` | x to the power y |
| ``` math.floor(x)``` | the greatest Integral <= x |
| ``` math.ceil(x)``` | the least Integral >= x |

## [Lists](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
A list represents a mutable series of data that can hold multiple data types. 

| Operation | Result |
| -------------- | -------- |
| ``` x in s``` | True if an item of s is equal to x, else False |
| ``` x not in s``` | False if an item of s is equal to x, else True |
| ``` s + t``` | the concatenation of s and t |
| ``` s * n or n * s``` | equivalent to adding s to itself n times |
| ``` s[i]``` | ith item of s, origin 0 |
| ``` s[i:j]``` | slice of s from i to j |
| ``` s[i:j:k]``` | slice of s from i to j with step k |
| ``` len(s)``` | length of s |
| ``` min(s)``` | smallest item of s |
| ``` max(s)``` | largest item of s |
| ``` s.index(x[, i[, j]])``` | index of the first occurrence of x in s (at or after index i and before index j) |
| ``` s.count(x)``` | total number of occurrences of x in s |
| ``` sorted(s)``` | returns a sorted version of the list |
| ``` s.sort()``` | preforms an in-place sort of the list; accepts sort function |

**DO NOT USE LISTS AS DEFAULT PARAMETERS** This will cause the list to be modified each time the function is called and never re-instantiated. 

## Tuples
Tuples are basically immutable lists. To define an singleton tuple use ``` (T,) ``` instead of ```(T)```

## Dictionary
Dicts are a mapping of hashable values to arbitrary objects.
```python
>>> a = dict(one=1, two=2, three=3)
>>> b = {'one': 1, 'two': 2, 'three': 3}
>>> c = dict(zip(['one', 'two', 'three'], [1, 2, 3]))
>>> d = dict([('two', 2), ('one', 1), ('three', 3)])
>>> e = dict({'three': 3, 'one': 1, 'two': 2})
>>> a == b == c == d == e
True
```

## Sets

# Comprehension


# Useful Builtings
* dir()
* help()
* pprint
* sys.path
* with open
* math
* ```range(start, stop[, step])``` || ```range(stop)```
```python 
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1, 11))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> list(range(0, 30, 5))
[0, 5, 10, 15, 20, 25]
>>> list(range(0, 10, 3))
[0, 3, 6, 9]
>>> list(range(0, -10, -1))
[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
>>> list(range(0))
[]
>>> list(range(1, 0))
[]
```





# Source control
	SVN vs Git -> Github/bitbucket
[GitTalk]: qblack.github.io/GitTalk	"GitTalk"



# Virtualenvs 



	Virtualenv wrapper
	Home variable
# Requirements.txt
# setup.py
# configuring a project to become an executable
# Accronyms: SOLID, DRY, RTFS, REST
# Database connections


# Important Packages
## requests
## pandas
## numpy
## jupyter
## jupyter lab
## twine
## sqlalchmey
## pyodbc
## celery
## flower


# anacondas



# Notepad++ tips and tricks


## Other Places to learn

* https://github.com/EbookFoundation/free-programming-books/blob/master/free-programming-books.md#professional-development
* http://www.oreilly.com/data/free/archive.html?imm_mid=0e8008&cmp=em-data-confreg-na-stny16_em13_vip_offer_lc 