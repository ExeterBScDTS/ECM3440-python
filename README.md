# ECM3440-python

## Advanced Python examples and exercises

These examples assume a reasonable knowledge of Python, and are intended to extend your
knowledge to include language features used in web programming.

### Rationale

If you've learned Python as an introduction to programming you might at times
struggle to read and
understand Python code written by others. This is because Python has many features that aren't taught in
introductory courses, but are important when using web frameworks and other larger software
environments.

## Language features


### Type hints and linting

If you edit your Python scripts using an editor, or
IDE, that has Python editing features you will be aware that many programming errors,
particularly syntax errors, can be spotted by editors. This form of program checking is called 'linting' because the first such static testing program was called 'lint' as it found the 'fluff' in your programs.  

Like code reviews conducted by human reviewers there is no requirement that the program is complete or even that it is syntactically correct. 
Static testing isn't limited to finding syntax errors, which you
would find out about soon enough when they prevent your program from running. Linting can also
find semantic errors such as unreachable lines of code.

 As Python is a dynamically typed language, there is another sort of error that we encounter, the `TypeError`.  For example a common mistake is to write something like this:

```python
num = input("type a number ")
if num == 1:
    # do something
elif num == 2:
    # do something else
else:
    # etc
```

This is perfectly valid Python but the result of the `input()` function is
always a string, so this will not work as intended.

```python
num : int = input("type a number ")
if num == 1:
    # do something
elif num == 2:
    # do something else
else:
    # etc
```

By adding a *type hint*, in this case `: int`, we instruct the linter to check that all uses of the variable `num` are consistent with an integer type. When this code is linted the following error is shown:

```none
lint_fragment.py:1: error: Incompatible types in assignment (expression has type "str", variable has type "int")
```
Note that this is a linting error, in this case the output of the `mypy` program, not a Python interpreter error. The program will still run, and its behaviour is still
incorrect, but we now know there is an error to be fixed.

*Type hints* are especially useful for function signatures. Note that the return type is also hinted.  For functions that do not return a value use `-> None`.

```python
def my_func(my_arg:str, count:int=1) -> str:
```

#### Static checking tools

* <http://mypy-lang.org/>

* <https://www.pylint.org/>

* <https://code.visualstudio.com/docs/python/linting>

### Classes and decorators

<https://realpython.com/python-metaclasses/>

### Generators and yield

You will be familiar with `range()`, which is often used in `for` loops like this:

```python
for n in range(3,13,3):
    print(n)
```

In Python We can write our own generators by using the `yield` keyword rather than  `return`, like this:

```python
def my_generator(count):
    n = 0
    while n < count:
        yield "n is " + str(n)
        n += 1

for s in my_generator(4):
    print(s)
```

### Miscellaneous new features

    F strings <https://realpython.com/python-f-strings/>

    data classes <https://realpython.com/python37-new-features/>

## Programming styles and patterns

Being familiar with the syntax of a programming language and the libraries of functions available is only a part of the skills needed to turn designs into
working software.  There are various programming styles, or idioms, and patterns that enable programmers to create high quality software.

### Pure functions and methods

It is worth noting that the methods of built in Python *types* such as `str` and `dict` are *pure*, by which it is meant that they have no side effects. Those new to Python are
sometimes caught out by this, especially the string methods such as `upper()`. For example:

```python
name = "Bob"
name.upper()
print(name)
```

This prints `Bob`, whereas this:

```python
print("Bob".upper())
```
gives `BOB`.

A corrected form of the first example is often given as:

```python
name = "Bob"
name = name.upper()
print(name)
```
This code recognizes that Python strings are *immutable*. The string methods such as `upper()` give new strings as return values.  One consequence of this is that we can write code such as this:

```python
label = "a&b".replace("&","_").upper().rjust(8)
```

This style of programming is called *functional programming*.

## Concurrency

Programs that run continuously will generally need to accept new input, create output and perform some data transformation at the same time. This is called `concurrency` and can be achieved in numerous ways. This is a big subject with a lot of
theoretical and practical considerations.  For the purposes of designing and
developing business applications it isn't necessary to consider parallel computation of the type that might be used in scientific programming or 3D graphics.

### Coroutines

An event loop runs in a thread (typically the main thread) and executes all callbacks and Tasks in its thread. While a Task is running in the event loop, no other Tasks can run in the same thread. When a Task executes an await expression, the running Task gets suspended, and the event loop executes the next Task.
<https://docs.python.org/3/library/asyncio-dev.html>

<https://docs.python.org/3/library/asyncio-task.html>

### Threads

<https://pymotw.com/2/threading/>

<https://docs.python.org/3/library/threading.html>

### Multiprocessing

This is an alternative style of concurrency that uses capabilities built into the operating system.  It is effectively equivalent to running two, or more, copies of the Python interpreter, all running the same Python program but at any given time running different functions or using different data.

<https://docs.python.org/3/library/multiprocessing.html>

## Building, testing and debugging

### Modules and packages

* ```__init__.py```

* pip
<https://pypi.org/project/pip/>


### Unit testing

## APIs

### Urllib

### WSGI


Video: You Don't Need That! <https://www.youtube.com/watch?v=imW-trt0i9I> Christopher Neugebauer



* <https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/>


## Unit testing

Essential for TDD

For examples of significant project that use ```unittest``` see,

* <https://github.com/django/django>

* <https://github.com/scrapy/scrapy>

* <https://github.com/faif/python-patterns>

Using ```pytest``` see,

* <https://github.com/pallets/flask>

## Design patterns

* <https://github.com/faif/python-patterns>