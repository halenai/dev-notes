# Python 3

## Contents
* [Basic Syntax](#basic-syntax)
* [Data Types](#data-types)
* [Sequences](#sequences)
  * Strings
  * Tuples
  * Lists
  * Sets
  * Dictionaries
* [Conditional Statement](#conditional-statement)
* [Loops](#loops)
* [Functions](#functions)
* [Modules](#modules)
* [Classes](#classes)
* [Test-Driven Development (TDD)](#test-driven-development-tdd)
  * Terminology
  * Not Big Design Up Front
  * Workflow
  * Useful Concepts
  * Testing Best Practices
* [Logging](#logging)
  * Basic Interface
  * Logger Objects
---

## Basic Syntax

> Indentation in Python is required. Is used to demarcate blocks of code.

Print a string to the screen
```Python
print('Hello, world!')
```

Print a format string (variable names enclosed with `{}` will be replaced by variable values)
```Python
print(f'Hello, {name}!')
```

Set variable `name` to the user input returned by `input()`
```Python
name = input()
```

## Data Types

Python is a weakly typed language

* `int` integer value
* `float` floating point value
* `str` text string
* `bool` boolean value (True or False)
* `None` empty value

## Sequences

Note that any sequence in Python can contain any number of data types.

### Strings

Strings are justs sequence of characters, and can be indexed as such.

```Python
  name = "Alice"
  print(name[0])
```

### Tuples

Tuples are immutable collections of values under a single name, which can be indexed positionally.

```Python
  coordinates = (10.0, 20.0)
  print(coordinates[1])
```

### Lists

Lists are mutable collections of values under a single name, which can be indexed positionally. Indexing out of range raises a Python ‘exception’. In this case, an `IndexError`, because there is no fourth value in `names` for Python to return.

```Python
  names = ["Alice", "Bob", "Charlie"]
  print(names[2])
```

### Sets

Sets are unordered collection of unique items. Because they are unordered, they cannot be indexed.

```Python
  s = set()
  s.add(1)
  s.add(3)
  s.add(5)
```

### Dictionaries

Dictionaries (or dicts) are like lists, except that they are unordered and their `value`s are indexed by `key`s. The `+=` operator increments the left-hand side by the right-hand side.

```Python
  ages = {"Alice": 22, "Bob": 27}
  print(ages["Alice"])
  ages["Alice"] += 1
```

## Conditional statement

* The Python interpreter knows where the conditional `if` block ends and the `elif` block begins because of the changes in indentation. `elif` and `else` blocks are optional.

```Python
if x > 0:
    print("x is positive")
elif x < 0:
    print("x is negative")
else:
    print("x is zero")
```

## Loops

For-loops iterate over their bodies a limited number of times. In this case, the number of iterations is set by `range(5)`. `range(5)` returns the sequence of numbers starting at 0 through 4. Each value is passed to `i` once, resulting in the loop running a total of 5 times. `i` is normally referred to as an iterator variable.

```Python
for i in range(5):
    print(i)
```

This for-loop iterates over `names`, which is a list. Every value in the list is assigned, in order, to the iterator `name` once.

```Python
for name in names:
    print(name)
```

## Functions

Python has built-in functions, such as `print()` and `input()`, but Python also allows for the creation of user-defined functions. This is a function called `square`, which takes a single argument `x`, and returns the value `x * x`. Like loops, the body of a function must be indented.

Trying to call a function that hasn’t been defined will raise a `NameError` exception.

```Python
  def square(x):
      return x * x
```

## Modules

Modules are separate `.py` files of code, often written by others, used in a new file without rewriting all the old code again. Using modules allows, for example, the use of functions across a program larger than a single file.

Assuming the `square` function shown above was saved in `functions.py`, adding this line atop a new module will allow for the use of `square` there as well.

```Python
from functions import square
```

If, for example, `functions.py` also included some other code that wouldn't neccesarily be inside a function, that code would be executed every time `square` was imported from `functions`, because the Python interpreter reads through the entire `functions.py` file. To remedy this, code that should only run when their containing file is run directly should be encapsulated in a function, called, for example, `main`. After, the following should be appended:

```Python
if __name__ == "__main__":
    main()
```

This should be interpreted as saying ‘if this file is currently being run’, execute `main`.

## Classes

A Python `class` can be thought of as a way to define a new, custom Python data type, somewhat analagous to defining a custom function. By convention, `class` names tend to start with a capital letter.

This creates a new `class` called `Point`:

```Python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

The __init__ function is a special function that defines the information needed when a new `Point` is created.

* `self` is always required, which refers to the `Point` being created, while `x` and `y` are its coordinates.
* `self.x` and `self.y` actually do the work of creating `x` and `y` attributes for the `Point` and assigning the m the values passed to `__init__`.

This instantiates a new `Point` with `x = 3` and `y = 5`. When this line is run, the `__init__` function of the Point class is automatically run.

```Python
p = Point(3, 5)
```

To access the x attribute of p, use dot notation:

```Python
print(p.x)
```

## Test-Driven Development (TDD)

In TDD the first step is always the same: _write a test_.

_First_ write the test; _then_ run it and check that it fails as expected. _Only then_ go ahead and build some of the app.

TDD is a _discipline_, and that means it's not something that comes naturally; because many of the payoffs aren't immediate but only come in the longer term, you have to force yourself to do it in the moment.

### Terminology

__Functional tests__ may be called _acceptance tests_ or _end-to-end tests_ and they look at how the whole application functions, from the outside. Another term is _black box test_, because the test doesn't know anything about the internals  of the system under test.

Functional tests can be a sort of specification for the application. It tends to track what might be called a _User story_, and follows how the user might work with a particular feature and how the app should respond to them. They have a human-readable story that can be followed and it's made explicit by using comments that accompany the test code.

__Unit tests__ test the application from the inside, from the point of view of the programmer.

### Not Big Design Up Front

TDD is closely associated with the agile movement in software development, which includes a reaction against _Big Design Up Front_, the traditional software engineering practice whereby, after a lengthy requirements gathering exercise, there is an equally lengthy design stage where the software is planned out on paper. The agile philosophy is that you learn more from solving problems in practice than in theory, especially when the application confronts with real users as soon as possible. Instead of a long up-front design phase, you try to put a _minimum viable application_ early, and let the design evolve gradually based on feedback from real-world usage.

### Workflow

1. Write a _functional test_ describing the new functionality from the user's point of view
2. Once you have a functional test that fails, start to think about how to write code that can get it to pass. Then you use one or more _unit tests_ to define how you want the code to behave. Each line of production code you write should be tested by (at least) one your unit tests
3. Once you have a failing unit test, you write the smallest amount of _application code_ you can, just enough to get the unit test to pass. You may iterate between steps 2 and 3 a few times, until you think the functional test will get a little further.
4. Rerun the functional test and see if it pass, or get a little further. That may prompt you to write some new unit tests, and some new code, and so on.

![TDD Process](../img/tdd_process.png)

The functional tests drive development from a high level, while unit tests drive at a low level.

![TDD Process](../img/double_loop_tdd.png)

> Functional tests should help you build an application with the right functionality, and guarantee you never accidentally break it. Unit tests should help you to write code that's clean and bug free.

#### Red/Green/Refactor

The unit-test/code cycle is usually taught as _Red, Green, Refactor:_

* Start by writing a unit test which fails (_Red_).
* Write the simplest possible code to get it to pass (_Green_), _even if that means cheating_.
* _Refactor_ to get to better code that makes more sense.

#### Refactoring

* __Eliminate duplication__: if your test uses a magic constant, and your application code also uses it, that counts as duplication, so it justifies refactoring. Removing the magic constant from the application code usually means you have to stop cheating.
* __Triangulation__: if your test lets you get away with writing "cheating" code that you're not comfortable with, _write another test_ that forces you to write some better code.

### Useful Concepts

* __Regression__: When new code breaks some aspect of the application which used to work.
* __Unexpected failure__: When a test fails in a way it wasn't expected. This either means that a mistake in the tests was made, or that the tests have helped to find a regression and a fix in the code is required.
* __Red/Green/Refactor__: Another way of describing the TDD process. See above.
* __Triangulation__: Adding a test case with a new specific example for some existing code, to justify generalising the implementation (which may be a "cheat" until that point).
* __Three strikes and refactor__: A rule of thumb for when to remove duplication from code. When two pieces of code look very similar, it often pays to wait until you see a third use case, so that you're more sure about what part of the code really is the common, re-usable part to refactor out.

### Testing Best Practices

* __Ensuring test isolation and managing global state__: Different tests shouldn't affect one another. This means to reset any permanent state at the end of each test. Django's test runner helps us do this by creating a test database, which it wipes clean in between each test.
* __Avoid "voodoo" sleeps__: Whenever a wait for something to load is needed, it's always tempting to use time.sleep. But the problem is that length of time to wait is always a bit of a shot in the dark, either too short and vulnerable to spurious failures, or too long and it'll slow down our test runs. Prefer a retry loop that polls the app and moves on as soon as possible.
* __Don't rely on implicit waits__: "Explicit is better than implicit", as the Zen of Python says, so prefer explicit waits.

## Logging

Python provides logging through the ```logging``` module. It can be used in two broad ways and both share the same principles:
* __Basic interface__: simple to set up, useful for scripts and mid-size applications
* __Logger objects__: complex to set up, far more powerful. Scales to any size

### Basic Interface

Usage

```Python
import logging
logging.warning('Watch out!')
logging.error('Watch out!')
```
Output

```Shell
$ WARNING:root:Watch Out!
$ ERROR:root:Watch Out!
```

#### Configuring the Basic Interface

The `logging.basicConfig()` method has to be called exactly once and it must happen before the first logging event. Additionally if the program has several threads, it must be called from the main thread and *only* the main thread.

Basic Arguments

* __level__: the log level threshold
* __format__: the format of the log records
* __filename__: filename to write log messages, by default writes to stderr
* __filemode__: "a" to append to the log file (default), "w" to overwrite

Log Level signals

The following are the log level signals supported by the `logging` module from lowest to highest severity. The order matters in the list below; _debug_ is considered strictly less severe than _info_, and so on.

* __debug__: detailed information, should be used when diagnosing problems (shouldn't be used in production)
* __info__: confirmation that everything is working as expected (might be used in production depending on the application)
* __warning__: something unexpected happened or a potential problem in the near future (eg. filesystem full)
* __error__: the application has not been able to perform a function
* __critical__: a serious error, the application is unable to continue running

Each level has a corresponding uppercased constant in the library (e.g., `logging.WARNING` for `logging.warning()`) and are used when defining the log level threshold. The default is `logging.WARNING` and it it can be changed with `logging.basicConfig(level=logging.INFO)`.

The phrase _log level_ has two different meanings depending on the context. It can mean the __severity__ of the message, which can be set by choosing which of the methods to use (e.g., `logging.warning()`). Or it can mean the __threshold__ for ignoring a message which is signaled by the constants (e.g., `logging.WARNING`).

Constants can also be used in the more general `logging.log` method

```Python
logging.log(logging.DEBUG, 'Small detail, useful for troubleshooting')
```

This is useful to modify the log level dynamically at runtime:

```Python
def log_results(message, level=logging.INFO):
    logging.log(level, 'Results: ' + message)
```

##### Format Attributes

Named fields are defined in percent-formatting by %(FIELDNAME)x, where "x" is a type code: _s_ for string, _d_ for integer (decimal), and _f_ for floating-point.
The default is `%(levelname)s:%(name)s:%(message)s` where name is the name of the logger object (by default _root_).

Some of the most common attributes:

Attribute | Format        | Description
--------- | ------------- | -----------
asctime   | %(asctime)s   | Human-readable date/time
funcName  | %(funcName)s  | Name of function containing the logging call
lineno    | %(lineno)s    | The line number of the logging call
message   | %(message)s   | The log message
pathname  | %(pathname)s  | Full pathname of the source file of the logging call
levelname | %(levelname)s | Text logging level for the message ('DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL')
name      | %(name)s      | The logger's name

Full list can be found [here](https://docs.python.org/3/library/logging.html#logrecord-attributes)

__Note__: if the log level threshold is higher than the message itself, the line does nothing. Having this into consideration it's important to consider avoiding formatting the string passed to the logger object in order to avoid using system memory and CPU cycles when no logging will take place.

#### Implementation Example

```Shell
$ export MODE=development
```

```Python
import os
mode = os.environ.get('MODE', 'production').upper()

log_file = 'myapp.log'

# mode can be set by environment variable, command line option etc.
if mode === 'DEVELOPMENT':
    log_level = logging.DEBUG
    log_mode = 'w'
else:
    log_level = logging.WARNING
    log_mode = 'a'

logging.basicConfig(level = log_level, filename = log_file, filemode = log_mode)
```

### Logger Objects

Larger Python applications tend to have different logging needs. `logging` meets these needs through a richer interface, called _logger objects_ or simplu _loggers_.

When a call to `logging.warning()` (or other log method) is made, they convey messages through what is called the _root logger_, the primary, default logger object.

`logging.basicConfig` operates on this root logger and the actual root logger object can be fetch by calling `logging.getLogger()`.

```Python
logger = logging.getLogger()
logger.name
```

```Shell
> 'root'
```

Logger objects have all the same methods the logging module itself has:

```Python
import logging
logger = logging.getLogger()
logger.debug('Small detail. Useful for troubleshooting.')
logger.info('This is informative.')
logger.warning('This is a warning message.')
logger.error('Uh oh. Something went wrong.')
logger.critical('We have a big problem!')
```
