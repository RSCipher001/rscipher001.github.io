---
title: "Python Cheatsheet"
date: 2019-11-10T23:16:00+05:30
description: "Python Cheatsheet"
tags: [python]
---

## One Liners
This is a list of some awesome one liners

### Start local server
```python
# Python 3
python -m http.server

# Python 2
python -m SimpleHTTPServer

# Custom Port
python -m http.server 8081
```

### Execute Python code from shell (bash/zsh/etc)

This is helpful when you want to execute simple python code but don't want to launch python shell, you can also use grep or other utilities with this approach
```bash
# This print print 4
python -c "print(2+2)"

# Executing multiple lines
python -c "print(2+2);print('Another line')"
```

### Execute a file in interactive shell
This is very useful when you want to execute already written code in interactive shell

```python
exec(open("./filename.py").read())
```

## LinkedIn Learning Advanced Python

### PEP Guidelines
- imports go on their own lines
- Two blank lines separate classes from other functions
- Within classes, one blank line separates methods
- Long comments are limited to 72 characters instead of 79 for lines of code.

### String & byte conversion
```python
b = bytes([0x41, 0x42, 0x43, 0x44])
s = "This is a string"

# Convert byte to string
s2 = b.decode('utf-8')

# Convert string to byte
b2 = s.encode('utf-8')
```

### Template string
```python
from string import Template

# Usual string formatting with format()
str1 = "You're watching {0} by {1}".format("Advanced Python", "Joe Marini")
print(str1)

# create a template with placeholders
templ = Template("You're watching ${title} by ${author}")

# use the substitute method with keyword arguments
str2 = templ.substitute(title="Advanced Python", author="Joe Marini")
print(str2)

# use the substitute method with a dictionary
data = { 
    "author": "Joe Marini",
    "title": "Advanced Python"
}
str3 = templ.substitute(data)    
print(str3)
```

### Using iterators
Iterators are the most commonly used features of python

```python
# define a list of days in English and French
days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
daysFr = ["Dim", "Lun", "Mar", "Mer", "Jeu", "Ven", "Sam"]

# use iter to create an iterator over a collection
i = iter(days)
print(next(i))  # Sun
print(next(i))  # Mon
print(next(i))  # Tue

# iterate using a function and a sentinel
with open("testfile.txt", "r") as fp:
	# Empty double codes are condition for termination
    for line in iter(fp.readline, ''):
        print(line)
```

#### Using enumerate
```python
# use regular iteration over the days
for m in range(len(days)):
    print(m+1, days[m])

# using enumerate reduces code and provides a counter
for i, m in enumerate(days, start=1):
    print(i, m)
```

#### Using zip
```python
# use zip to combine sequences
for m in zip(days, daysFr):
    print(m)

for i, m in enumerate(zip(days, daysFr), start=1):
    print(i, m[0], "=", m[1], "in French")
```

### Using itertools
```python
# A common function
def testFunction(x):
    return x < 40
```

#### Using cycle to create infinite iterator
```python
def main():
# cycle iterator can be used to cycle over a collection
seq1 = ["Joe", "John", "Mike"]
cycle1 = itertools.cycle(seq1)
print(next(cycle1))   # Joe
print(next(cycle1))   # John
print(next(cycle1))   # Mike
print(next(cycle1))   # Joe
```

#### Using count
```python
# use count to create a simple counter
count1 = itertools.count(100, 10)
print(next(count1))  # 100
print(next(count1))  # 110
print(next(count1))  # 120
```

#### Using accumulate
```python
# accumulate creates an iterator that accumulates values
vals = [10, 20, 30, 40, 50, 40, 30]

# accumulate will stop at max
acc = itertools.accumulate(vals, max)
print(list(acc))

# incremental addition, instead max function we will use custom function
 = itertools.accumulate(vals, lambda a, b: a + b)
print(list(addition))
```

#### Using chain
```python
# use chain to connect sequences together
x = itertools.chain("ABCD", "1234")
print(list(x))
```
#### Using dropwhile/takewhile
```python
# dropwhile and takewhile will return values until
# a certain condition is met that stops them
# This are filters
print(list(itertools.dropwhile(testFunction, vals)))
print(list(itertools.takewhile(testFunction, vals)))
```


### Using Sorted, Filter & Map
Common functions
```python
def filterFunc(x):
    if x % 2 == 0:
        return False
    return True


def filterFunc2(x):
    if x.isupper():
        return False
    return True


def squareFunc(x):
    return x**2


def toGrade(x):
    if (x >= 90):
        return "A"
    elif (x >= 80 and x < 90):
        return "B"
    elif (x >= 70 and x < 80):
        return "C"
    elif (x >= 65 and x < 70):
        return "D"
    return "F"
```

```python
# define some sample sequences to operate on
nums = (1, 8, 4, 5, 13, 26, 381, 410, 58, 47)
chars = "abcDeFGHiJklmnoP"
grades = (81, 89, 94, 78, 61, 66, 99, 74)

# use filter to remove items from a list
odds = list(filter(filterFunc, nums))
print(odds)

# use filter on non-numeric sequence
lowers = list(filter(filterFunc2, chars))
print(lowers)

# use map to create a new sequence of values
squares = list(map(squareFunc, nums))
print(squares)

# use sorted and map to change numbers to grades
grades = sorted(grades)
letters = list(map(toGrade, grades))
print(letters)
```

### Built in functions

These are built in function so you don't need to import these

#### any and all
```python
list1 = [1, 2, 3, 0, 5, 6]

# any will return true if any of the sequence values are true
print(any(list1))

# all will return true only if all values are true
print(all(list1))

# min and max will return minimum and maximum values in a sequence
print("min: ", min(list1))
print("max: ", max(list1))    

# Use sum() to sum up all of the values in a sequence
print("sum: ", sum(list1))
```

### Functions
These are functions related code snippets

#### Docstring example
```python
def myFunction(arg1, arg2=None):
    """myFunction(arg1, arg2=None) --> Doesn't really do anything special.

    Parameters:
    arg1: the first argument. Whatever you feel like passing.
    arg2: the second argument. Defaults to None. Whatever makes you happy.
    """
    print(arg1, arg2)


def main():
    print(myFunction.__doc__)


if __name__ == "__main__":
    main()
```

#### Keyword argument
```python
# use keyword-only arguments to help ensure code clarity
def myFunction(arg1, arg2, *, suppressExceptions=False):
    print(arg1, arg2, suppressExceptions)


def main():
    # try to call the function without the keyword
    # myFunction(1, 2, True)
    myFunction(1, 2, suppressExceptions=True)


if __name__ == "__main__":
    main()
```

#### Variable arugment list
```python
# define a function that takes variable arguments
def addition(base, *args):
    result = 0
    for arg in args:
        result += arg

    return result


def main():
    # pass different arguments
    print(addition(5, 10, 15, 20))
    print(addition(1, 2, 3))

    # pass an existing list
    myNums = [5, 10, 15, 20]
    print(addition(*myNums))


if __name__ == "__main__":
    main()
```

### Collections

These are some of the most used functions from python collections library

#### Counter
```python
from collections import Counter


def main():
    # list of students in class 1
    class1 = ["Bob", "James", "Chad", "Darcy", "Penny", "Hannah"
              "Kevin", "James", "Melanie", "Becky", "Steve", "Frank"]

    # list of students in class 2
    class2 = ["Bill", "Barry", "Cindy", "Debbie", "Frank",
              "Gabby", "Kelly", "James", "Joe", "Sam", "Tara", "Ziggy"]

    # Create a Counter for class1 and class2
    c1 = Counter(class1)
    c2 = Counter(class2)

    # How many students in class 1 named James?
    print(c1["James"])

    # How many students are in class 1?
    print(sum(c1.values()), "students in class 1")

    # Combine the two classes
    c1.update(class2)
    print(sum(c1.values()), "students in class 1 and 2")

    # What's the most common name in the two classes?
    print(c1.most_common(3))

    # Separate the classes again
    c1.subtract(class2)
    print(c1.most_common(1))

    # What's common between the two classes?
    print(c1 & c2)


if __name__ == "__main__":
    main()
```

#### Defaultdict
```python
from collections import defaultdict


def main():
    # define a list of items that we want to count
    fruits = ['apple', 'pear', 'orange', 'banana',
              'apple', 'grape', 'banana', 'banana']

    # use a dictionary to count each element
    fruitCounter = defaultdict(int)

    # Count the elements in the list
    for fruit in fruits:
        fruitCounter[fruit] += 1

    # print the result
    for (k, v) in fruitCounter.items():
        print(k + ": " + str(v))


if __name__ == "__main__":
    main()
```


#### Deque
```python
import collections
import string


def main():
    # initialize a deque with lowercase letters
    d = collections.deque(string.ascii_lowercase)

    # deques support the len() function
    print("Item count: " + str(len(d)))

    # deques can be iterated over
    for elem in d:
        print(elem.upper(), end=",")

    # manipulate items from either end
    d.pop()
    d.popleft()
    d.append(2)
    d.appendleft(1)
    print(d)

    # rotate the deque
    print(d)
    d.rotate(1)
    print(d)


if __name__ == "__main__":
    main()
```

#### Namedtuple
```python
import collections


def main():
    # create a Point namedtuple
    Point = collections.namedtuple("Point", "x y")

    p1 = Point(10, 20)
    p2 = Point(30, 40)

    print(p1, p2)
    print(p1.x, p1.y)

    # use _replace to create a new instance
    p1 = p1._replace(x=100)
    print(p1)


if __name__ == "__main__":
    main()
```


### Ordereddict
```python
from collections import OrderedDict


def main():
    # list of sport teams with wins and losses
    sportTeams = [("Royals", (18, 12)), ("Rockets", (24, 6)), 
                ("Cardinals", (20, 10)), ("Dragons", (22, 8)),
                ("Kings", (15, 15)), ("Chargers", (20, 10)), 
                ("Jets", (16, 14)), ("Warriors", (25, 5))]

    # sort the teams by number of wins
    sortedTeams = sorted(sportTeams, key=lambda t: t[1][0], reverse=True)

    # create an ordered dictionary of the teams
    teams = OrderedDict(sortedTeams)
    print(teams)

    # Use popitem to remove the top item
    tm, wl = teams.popitem(False)
    print("Top team: ", tm, wl)

    # What are next the top 4 teams?
    for i, team in enumerate(teams, start=1):
        print(i, team)
        if i == 4:
            break

    # test for equality
    a = OrderedDict({"a": 1, "b": 2, "c": 3})
    b = OrderedDict({"a": 1, "c": 3, "b": 2})
    print("Equality test: ", a == b)


if __name__ == "__main__":
    main()
```

### Classes
Most of the classes stuff is related to magic methods

#### String representation
```python

class Person():
    def __init__(self):
        self.fname = "Joe"
        self.lname = "Marini"
        self.age = 25

    # use __repr__ to create a string useful for debugging
    def __repr__(self):
        return "<Person Class - fname:{0}, lname:{1}, age{2}>".format(self.fname, self.lname, self.age)

    # use str for a more human-readable string
    def __str__(self):
        return "Person ({0} {1} is {2})".format(self.fname, self.lname, self.age)

    # use bytes to convert the informal string to a bytes object
    def __bytes__(self):
        val = "Person:{0}:{1}:{2}".format(self.fname, self.lname, self.age)
        return bytes(val.encode('utf-8'))


def main():
    # create a new Person object
    cls1 = Person()

    # use different Python functions to convert it to a string
    print(repr(cls1))
    print(str(cls1))
    print("Formatted: {0}".format(cls1))
    print(bytes(cls1))


if __name__ == "__main__":
    main()
```

#### Number like behaviour
```python

class Point():
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self):
        return "<Point x:{0},y:{1}>".format(self.x, self.y)

    # implement addition
    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    # implement subtraction
    def __sub__(self, other):
        return Point(self.x - other.x, self.y - other.y)

    # implement in-place addition
    def __iadd__(self, other):
        self.x += other.x
        self.y += other.y
        return self


def main():
    # Declare some points
    p1 = Point(10, 20)
    p2 = Point(30, 30)
    print(p1, p2)

    # Add two points
    p3 = p1 + p2
    print(p3)

    # subtract two points
    p4 = p2 - p1
    print(p4)

    # Perform in-place addition
    p1 += p2
    print(p1)


if __name__ == "__main__":
    main()
```

#### Enmum class
```python
from enum import Enum, unique, auto


# Unique annotation prevents duplicate, by default duplicates are allowed
@unique
class Fruit(Enum):
    APPLE = 1
    BANANA = 2
    ORANGE = 3
    TOMATO = 4
    PEAR = auto() # Auto is equivalent to auto_increment


def main():
    # enums have human-readable values and types
    print(Fruit.APPLE)
    print(type(Fruit.APPLE))
    print(repr(Fruit.APPLE))

    # enums have name and value properties
    print(Fruit.APPLE.name, Fruit.APPLE.value)

    # print the auto-generated value
    print(Fruit.PEAR.value)

    # enums are hashable - can be used as keys
    myFruits = {}
    myFruits[Fruit.BANANA] = "Come Mr. Tally-man"
    print(myFruits[Fruit.BANANA])


if __name__ == "__main__":
    main()
```


### Computed attributes
```python

class myColor():
    def __init__(self):
        self.red = 50
        self.green = 75
        self.blue = 100

    # use getattr to dynamically return a value
    def __getattr__(self, attr):
        if attr == "rgbcolor":
            return (self.red, self.green, self.blue)
        elif attr == "hexcolor":
            return "#{0:02x}{1:02x}{2:02x}".format(self.red, self.green, self.blue)
        else:
            raise AttributeError

    # use setattr to dynamically return a value
    def __setattr__(self, attr, val):
        if attr == "rgbcolor":
            self.red = val[0]
            self.green = val[1]
            self.blue = val[2]
        else:
            super().__setattr__(attr, val)

    # use dir to list the available properties
    def __dir__(self):
        return ("rgbolor", "hexcolor")


def main():
    # create an instance of myColor
    cls1 = myColor()
    # print the value of a computed attribute
    print(cls1.rgbcolor)
    print(cls1.hexcolor)

    # set the value of a computed attribute
    cls1.rgbcolor = (125, 200, 86)
    print(cls1.rgbcolor)
    print(cls1.hexcolor)

    # access a regular attribute
    print(cls1.red)

    # list the available attributes
    print(dir(cls1))


if __name__ == "__main__":
    main()
```


#### Comparision
```python

class Employee():
    def __init__(self, fname, lname, level, yrsService):
        self.fname = fname
        self.lname = lname
        self.level = level
        self.seniority = yrsService

    # implement comparison functions by emp level
    def __ge__(self, other):
        if self.level == other.level:
            return self.seniority >= other.seniority
        return self.level >= other.level

    def __gt__(self, other):
        if self.level == other.level:
            return self.seniority > other.seniority
        return self.level > other.level

    def __lt__(self, other):
        if self.level == other.level:
            return self.seniority < other.seniority
        return self.level < other.level

    def __le__(self, other):
        if self.level == other.level:
            return self.seniority <= other.seniority
        return self.level <= other.level

    def __eq__(self, other):
        return self.level == other.level


def main():
    # define some employees
    dept = []
    dept.append(Employee("Tim", "Sims", 5, 9))
    dept.append(Employee("John", "Doe", 4, 12))
    dept.append(Employee("Jane", "Smith", 6, 6))
    dept.append(Employee("Rebecca", "Robinson", 5, 13))
    dept.append(Employee("Tyler", "Durden", 5, 12))

    # Who's more senior?
    print(bool(dept[0] > dept[2]))
    print(bool(dept[4] < dept[3]))

    # sort the items
    emps = sorted(dept)
    for emp in emps:
        print(emp.lname)


if __name__ == "__main__":
    main()
```

### Loggig
Logging is a really important part of python development. Logger is used for writing logs to files/console that can be used for debugging, it is really usefull for apps running in serverless environment

**Note:** You can't use interactive python shell to understand logging. It will not print anything when writing on console.

#### Basic logging
```python
import logging


def main():
    # Use basicConfig to configure logging
    # this is only executed once, subsequent calls to
    # basicConfig will have no effect
    logging.basicConfig(level=logging.DEBUG,
                        filemode="w",
                        filename="output.log")

    # Try out each of the log levels
    logging.debug("This is a debug-level log message")
    logging.info("This is an info-level log message")
    logging.warning("This is a warning-level message")
    logging.error("This is an error-level message")
    logging.critical("This is a critical-level message")

    # Output formatted string to the log
    logging.info("Here's a {} variable and an int: {}".format("string", 10))


if __name__ == "__main__":
    main()
```

#### Custom Logging
```python
import logging

# This is extra data we are writing to log
# In most cases this will be replaced dynamically.
extData = {'user': 'joem@example.com'}


# This function will be used to understand how to log function name in log
def anotherFunction():
    logging.debug("This is a debug-level log message", extra=extData)


def main():
    # set the output file and debug level, and
    # use a custom formatting specification

    # This string is log format
    fmtStr = "%(asctime)s: %(levelname)s: %(funcName)s Line:%(lineno)d User:%(user)s %(message)s"

    # This string is date format in logs
    dateStr = "%m/%d/%Y %I:%M:%S %p"
    logging.basicConfig(filename="output.log",
                        level=logging.DEBUG,
                        format=fmtStr,
                        datefmt=dateStr)

    logging.info("This is an info-level log message", extra=extData)
    logging.warning("This is a warning-level message", extra=extData)
    anotherFunction()


if __name__ == "__main__":
    main()
```


### Comprehensions
Comprehensions are like short and clean syntax for very common tasks related to data

#### Set comprehensions
```python

def main():
    # define a list of temperature data points
    ctemps = [5, 10, 12, 14, 10, 23, 41, 30, 12, 24, 12, 18, 29]

    # build a set of unique Fahrenheit temperatures
    ftemps1 = [(t * 9/5) + 32 for t in ctemps]
    ftemps2 = {(t * 9/5) + 32 for t in ctemps}
    print(ftemps1)
    print(ftemps2)

    # build a set from an input source
    sTemp = "The quick brown fox jumped over the lazy dog"
    chars = {c.upper() for c in sTemp if not c.isspace()}
    print(chars)


if __name__ == "__main__":
    main()
```

#### List comprehensions

```python

def main():
    # define two lists of numbers
    evens = [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
    odds = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]

    # Perform a mapping and filter function on a list
    evenSquared = list(
        map(lambda e: e**2, filter(lambda e: e > 4 and e < 16, evens)))
    print(evenSquared)

    # Derive a new list of numbers frm a given list
    evenSquared = [e ** 2 for e in evens]
    print(evenSquared)

    # Limit the items operated on with a predicate condition
    oddSquared = [e ** 2 for e in odds if e > 3 and e < 17]
    print(oddSquared)


if __name__ == "__main__":
    main()
```


### Dictionary comprehensions

```python

def main():
    # define a list of temperature values
    ctemps = [0, 12, 34, 100]

    # Use a comprehension to build a dictionary
    tempDict = {t: (t * 9/5) + 32 for t in ctemps if t < 100}
    print(tempDict)
    print(tempDict[12])

    # Merge two dictionaries with a comprehension
    team1 = {"Jones": 24, "Jameson": 18, "Smith": 58, "Burns": 7}
    team2 = {"White": 12, "Macke": 88, "Perce": 4}
    newTeam = {k: v for team in (team1, team2) for k, v in team.items()}
    print(newTeam)


if __name__ == "__main__":
    main()
```