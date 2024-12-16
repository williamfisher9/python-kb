# INTRODUCTION
### CHECK PYTHON VERSION
```
$ python --version      # shows installed version of python
$ py -v                 # shows installed version of python
```

### CREATE A VIRTUAL ENVIRONMENT PROFILE
```
$ py -m venv .venv                  # create a virtual env for the created application
$ source .venv/Scripts/activate     # run the profile
$ deactivate                        # exit from the profile
```

### INSTALL A PACKAGE IN THE PROFILE
```
pip install ...       # install py packages
```

### EXIT PYTHON INTERPRETOR
```
>>> exit()
```

### ARGV: ARGUMENTS READING
```
$ py file-name.py -m xyz -n soo

import sys
print(len(sys.argv))    # 5
print(sys.argv[0])      # file-name.py
```

### MULTI-LINE PRINT AND OTHER PRINT OPTIONS
```
print("""
Usage: thingy [OPTIONS]
        -h      Displaythings
        -l      List items
""")
```

```
s = 'yes \n it is nice to meet you'
print(s)

print('yes "it is" nice to meet you')
print("yes /" it is nice/" to meet you")
```

```
>>> print(3*'py' + 'yhon')
pypypyyhon
```

```
>>> text = ('py'
... 'thon')
>>> print(text)
python
```

```
prefix = 'python'
print(prefix + ' is easy to learn')
```

### LISTS
```
>>> word = 'python'
>>> print(len(word))
>>> print(word[0])
>>> print(word[5])
>>> print(word[-1])     # n
>>> print(word[-6])     # p
>>> word[0:2]           # py
>>> word[-3:-1]         # ho
>>> word[:2] + word[2:]   # python
>>>
>>> try:
...     print(word[7])
... except IndexError as exc:
...     print(exc)
```

```
>>> rgb = ["Red", "Green", "Blue"]
>>> rgba = rgb
>>> id(rgb) == id(rgba)  # they reference the same object
>>> True
>>> rgba.append("Alph")
>>> rgb
>>> ["Red", "Green", "Blue", "Alph"]
```

```
>>> correct_rgba = rgba[:]
>>> correct_rgba[-1] = "Alpha"
>>> correct_rgba
["Red", "Green", "Blue", "Alpha"]
>>> rgba
["Red", "Green", "Blue", "Alph"]
>>> correct_rgba[:] = []
[]
```

### NESTED LISTS
```
a = ['a', 'b', 'c']
n = [1, 2, 3]
x = [a, n]
x
[['a', 'b', 'c'], [1, 2, 3]]
x[0]
['a', 'b', 'c']
x[0][1]
'b'
```

### SWAP
```
>>> a, b = 0, 1
>>> a, b = b, a
```

### USER INPUT HANDLING
```
x = int(input("Enter an integer: "))
if x < 10:
   print("less than 10")
else:
   print("else")
```

```
x = int(input("Enter an integer value: "))
y = list()
while x > 10:
   y.append(x)
   x = int(input("Enter an integer value: "))

print(y)
```

### DICTIONARIES
```
users = {'John': 'active', 'Thai': 'inactive', 'James': 'active'}
print(users)

active_users = dict()
inactive_users = dict()

for user, status in users.copy().items():
    print(user + ' - ' + status)
    if status == 'active':
        active_users[user] = status
        del users[user]
    if status == 'inactive':
        inactive_users[user] = status
        del users[user]

print(users)
print(active_users)
print(inactive_users)
```

### RANGE
```
for i in range(10):
    print(i)

for i in range(10, 100, 10):
    print(i)

list(range(-10, -100, -30))

a = ['Mary', 'had', 'a', 'little', 'lamb']
for i in range(len(a)):
    print(i, a[i])

sum(range(4))
```

### PASS STATEMENT
```
while True:
    pass

# Minimal classes
class MyEmptyClass:
    pass
```

### MATCH STATEMENT (SWITCH)
```
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

### COMBINING SEVERAL LITERALS IN A SINGLE PATTERN USING | (“OR”):
```
case 401 | 403 | 404:
    print(f"X={401}")
    return "Not allowed"
```

### ENUMS
```
from enum import Enum
class Color(Enum):
    RED = 'red'
    GREEN = 'green'
    BLUE = 'blue'

print(Color.RED)            # Color.RED
print(Color("red"))         # Color.RED
print(Color.RED.value)      # red

color = Color(input("Enter your choice of 'red', 'blue' or 'green': "))

match color:
    case Color.RED:
        print("I see red!")
    case Color.GREEN:
        print("Grass is green")
    case Color.BLUE:
        print("I'm feeling the blues :")
```

```
def ask_ok(prompt, retries = 4, reminder = 'Please try again!'):
    while True:
        reply = input(prompt)
        if reply.upper() in ['YES', 'YE', 'Y']:
            break
        retries -= 1
        if retries < 1:
            raise ValueError('invalid user response')
        print(reminder)

ask_ok("Would you like to quit?[Y] ")
```

#### FUNCTIONS OPTIONAL AND REQUIRED ARGUMENTS
```
# accepts one required argument and 3 optional arguments
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')       # replaces the new-line ending with the space
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")

parrot("10")
-- This parrot wouldn't voom if you put 10 volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's a stiff !
```

#### FUNCTIONS POSITIONAL AND NAMED ARGUMENTS
- Positional arguments cannot be placed after named arguments.
- The first argument should not be named if followed by a positional argument.
- *arguments should precede **keywords
```
def func(one, *arguments, **keywords):
    print(one)
    print(arguments)
    print(type(arguments))
    print(keywords)
    print(type(keywords))

func("one", "two", "three", "four", five="six", seven="eight")

one
('two', 'three', 'four')
<class 'tuple'>
{'five': 'six', 'seven': 'eight'}
<class 'dict'>
```

```
# accepts both names and positional arg 
# standard_arg(arg=2) or standard_arg(2)
def standard_arg(arg):
    print(arg)
 
# because of the slash, it only accepts positional argument for all arguments up to the slash
# otherwise returns an error
# pos_only_arg(2)
def pos_only_arg(arg, /):
    print(arg)

# because of the star, it only accepts a named arg for all arguments after the star
# kwd_only_arg(arg=3)
def kwd_only_arg(*, arg):
    print(arg)

# arguments before the slash are positional. only one argument before the slash
# arguments after the star are named. only one argument after the slash
# standard is the second positional or named argument
# call the function combined_example("one", "two", kwd_only="test")
# call the function combined_example("one", standard="two", kwd_only="test")
def combined_example(pos_only, /, standard, *, kwd_only):
    print(pos_only, standard, kwd_only)
```

```
def foo(name, /, **kwds):
    return name in kwds['name']

print(foo("test", name="test"))     # True
```

```
def foo(name, **kwds):
    print(name)
    print(kwds)
    print(name in kwds.values())

print(foo('name', a='yyy', b='sss', c='name'))
```

```
args = [3, 6]
list(range(*args))            # call with arguments unpacked from a list
[3, 4, 5]
```

### FUNCTIONS ANNOTATIONS AND ARGUMENTS
```
def f(ham: str, eggs: str = 'eggs') -> str:
    print("Annotations:", f.__annotations__)
    print("Arguments:", ham, eggs)
    return ham + ' and ' + eggs

f('spam')
Annotations: {'ham': <class 'str'>, 'return': <class 'str'>, 'eggs': <class 'str'>}
Arguments: spam eggs
'spam and eggs'
```

### DOCSTRING
```
def my_function():
    """Do nothing, but document it.

    No, really, it doesn't do anything.
    """
    pass

print(my_function.__doc__)
Do nothing, but document it.

    No, really, it doesn't do anything.
```

### LAMBDA
```
def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)
mytripler = myfunc(3)

print(mydoubler(11))    # 22
print(mytripler(11))    # 33
```

```
pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
pairs.sort(key=lambda pair: pair[1])
print(pairs)    # [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```
