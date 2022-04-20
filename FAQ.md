# Typical questions on tech interviews
###### If you are reading this, then you know I know the answers :D
I may also use this as a reference / reminder when working because human memory isn't perfect

___

### Python basics
[Glossary](https://docs.python.org/3/glossary.html)

> #### Variable types

Immutable (have to be re-written entirely):
* [Booleans](https://www.w3schools.com/python/python_booleans.asp) `False`: `None`, `int(0)`, `str("")`, `tuple(())`, `list([])`, `dict({})`.
* [Numbers](https://www.w3schools.com/python/python_numbers.asp) `int, float, complex` 
* [Strings](https://www.w3schools.com/python/python_strings.asp) single: `''`/`""`, multi: `''' ''''`, formatting: `"" + str(var)`, `f"{var}"`, `"{1}" t.format(var)`.
* [Tuples](https://www.w3schools.com/python/python_tuples.asp) `()` Collection, ordered, unchangeable. Allows duplicates.

Mutable (can be changed):
* [List](https://www.w3schools.com/python/python_lists.asp) `[]` Collection, ordered, changeable. Allows duplicates.
* [Dictionaries](https://www.w3schools.com/python/python_dictionaries.asp) `{"key": "value"}` Collection, ordered (from 3.7), changeable. No duplicates.
* [Sets](https://www.w3schools.com/python/python_sets.asp) `{}` Collection, unordered, unchangeable (can add/remove), unindexed. No duplicates.

The `index()` method returns the position at the first occurrence of the specified value.

<br /><br />
> #### Iteration / Generation

An [iterator](https://www.w3schools.com/python/python_iterators.asp) is an object that can be iterated upon and contains a countable number of values.  
Technically, in Python, an iterator is an object which implements the iterator protocol, which consist of the methods `__iter__()` and `__next__()`.

[Generators](https://realpython.com/introduction-to-python-generators/) don't store data in memory, instead they return the answer only when called.  
Generator functions use `yield()` instead of `return()`, also `throw()` for errors and `close()` to finish.
On `yield()` statement, function execution is suspended yielded value returns to the caller but that doesn't stop the function.  
Using generators on mutable objects saves memory.  

<br /><br />
> #### Lambda functions

##### [lambda](https://www.w3schools.com/python/python_lambda.asp) arguments : expression

Simple usage: `lambda a, b : a + b`

Advanced usage:
```py
def multiply_by(n):
  return lambda a : a * n

multiply_by_two = multiply_by(2)

print(multiply_by_two(11))
```

<br /><br />
> #### Decorators

A [decorator](https://realpython.com/primer-on-python-decorators/) is a function that takes another function and extends the behavior of the latter function without explicitly modifying it.

```py
def decorator(func):
    def wrapper():
        # action 1
        function()
        # action 3
    return wrapper

@decorator
def function():
    # action 2
```
calling `function` actually returns `wrapper` of `decorator`.

<br /><br />
> #### Classes

A [class](https://docs.python.org/3/tutorial/classes.html) is a user-defined blueprint or prototype from which objects are created.  
Additional info on [class and static methods](https://realpython.com/instance-class-and-static-methods-demystified/).

```py
class Example:
    class_car = 1           # class variables belong to all instances of that class
    _protected_var = 1      # not hidden but should be only used internally
    __private_var = 1       # private, is hidden and protected from subclasses
    # same underscore rules apply to methods

    def instance_method(self):  # instance method
        self.x = 1              # instance variable (shuold be declared in a function)
        return self.x

    @classmethod            # only has access to class variables
    def class_method(cls):  # can be used to change the entire class and all subsequent instances
        return cls.x

    @staticmethod           # static methods can't access neither class, nor instance variables
    def static_method():    # they are primarily used for namespacing
        return 'static method'
```

Built in functions (not all, just the most used ones):  
* `__init__(self, [,args...])` is is called when a new class object is created.
* `__dict__(self)` returns a dictionary containing the class's namespace.
* `__bases__(self)` returns base classes.
* `__del__(self)` deletes the instance from memory.
* `__str__(self)` gives a user-friendly representation.
* `__repr__(self)` gives a developer-friendly representation.
* `__cmp__(self, x)` compares instance to another object.

<br /><br />
> #### Asynchronicity

**Concurrency** means executing multiple tasks at the same time but not necessarily simultaneously.  
**Parallelism** means executing multiple tasks at the same time simultaneously. Can only be achieved with multiple cores.

**Threads** run in the same memory space, while **processes** have separate memory.

**Global Interpreter Lock** (GIL) makes sure there is, at any time, only one **thread** is running.  
That ensures **thread-safety** and prevents threads from **racing** to make changes to memory.

To achieve **parallelism** Python has `multiprocessing` module which is not affected by the GIL.

<br /><br />
___

### Django
`ORM`  
`Models`  
`Serializers`  
`Views`  
`URLs`  
`Templates`  
`Tests`  
`Middlewares`  

### APIs
`REST`  
`SOAP`  
`RPC`  

### Databases
`SQL vs NoSQL`  
`Postgres`  
`Mongo`  

### Network
`HTTP / HTTPS`  
`TCP / UDP`  

### Hosting
`Nginx`  
`Gunicorn`  
`Docker`  
`AWS`  

### Caching
`Memcached`  
`Redis`

### Background tasks
`Celery`  
`Redis queue`  

### Git
`Overview`  
`Git flow`  
`Typical operations`  
