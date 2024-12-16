# DATA STRUCTRES
## MORE ON LISTS
- list.append(x)
- list.extend(iterable)
- list.copy(): Returns a shallow copy of the list. Similar to a[:].
- list.reverse()
- list.sort(*, key=None, reverse=False)
- list.count(x)
- list.clear()
- list.pop([i]): Remove the item at the given position in the list, and return it. If no index is specified, a.pop() removes and returns the last item in the list.
- list.remove(x): It raises a ValueError if there is no such item.

## USING LISTS AS STACKS
```
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack       # [3, 4, 5, 6, 7]
>>> stack.pop() # 7
>>> stack       # [3, 4, 5, 6]
>>> stack.pop() # 6
>>> stack.pop() # 5
>>> stack       # [3, 4]
```

## USING LISTS AS QUEUES
```
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves 'Eric'
>>> queue.popleft()                 # The second to arrive now leaves 'John'
>>> queue                           # Remaining queue in order of arrival deque(['Michael', 'Terry', 'Graham'])
```

## LIST COMPREHENSION
```
squares = [x*2 for x in range(10)]
print(squares)

# map takes a function and iterable
squares = list(map(lambda x: x**2, range(10)))

# which is equivalent to
def double(x):
    return x*2

squares = list(map(double, range(10)))
print(squares)

# you can also run functions in list comprehension
freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
[item.strip() for item in freshfruit]
```

## UNPACKING LISTS
```
list = [1, 2, 3, 4, 5, 6]
print(*list)
print(list)
```

## DEL STATEMENT
```
a = [-1, 1, 66.25, 333, 333, 1234.5]
del a[0]
a           # [1, 66.25, 333, 333, 1234.5]
del a[2:4]
a           # [1, 66.25, 1234.5]
del a[:]
a           # []
```

## TUPLES
Tuples are `immutable`, and usually contain a `heterogeneous` sequence (different types) of elements that are accessed via unpacking or indexing (or even by attribute in the case of namedtuples). Lists are `mutable`, and their elements are usually `homogeneous` (same type) and are accessed by iterating over the list.
```
t = (1, 2, 3, 4)        # elements accessed via unpacking or indexing
                        # usaully heterogenous

t = [1,2 , 3, 4]        # elements accessed by iterating over a list
                        # usaully homogeneous      

singleton = 'hello',    # to create a tuple
print(singleton)        # ('hello',)
print(type(singleton))  # <class 'tuple'>

# unpacking tuples
tuple_obj = (1, 2, 3, 4, 5)
one, two, three, four, five = tuple_obj
first, *rest = tuple_obj        # *g returns a list of the rest of the elements

print(one, two, first, *rest)   # 1 5 1 [2, 3, 4, 5]
```

## SETS
Sets are `unordered` **collection** with `no duplicate` elements. Basic uses include membership testing and eliminating duplicate entries.
```
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(type(basket))     # <class 'set'>
print(basket)           # {'orange', 'banana', 'pear', 'apple'}
'orange' in basket      # True

a = set('abracadabra')
print(a)                # {'a', 'r', 'b', 'c', 'd'}

a = {x for x in 'abracadabra' if x not in 'abc'}
a                       # {'r', 'd'}
```

## DICTIONARIES
- Dictionaries are `indexed by keys`, a set of `key: value pairs` with the requirement that the `keys are unique` (within one dictionary).
- Performing `list(d)` on a dictionary returns a `list of all the keys` used in the dictionary.
- `del d[key]` deletes a key: value from the dictionary and returns `KeyError` if key was not found.
- `d[new_key]=value` `inserts` a new key value if key is not in the dictionary or `updates` it if it exists.
- `in` and `not in` are used to test existence in the dictionary. 

    ```
    dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])     # {'sape': 4139, 'guido': 4127, 'jack': 4098}

    # list comprehension can be used in dictionaries
    {x: x**2 for x in (2, 4, 6)}                                # {2: 4, 4: 16, 6: 36}

    # another way to create dictionaries
    dict(sape=4139, guido=4127, jack=4098)                      # {}'sape': 4139, 'guido': 4127, 'jack': 4098}
    ```

- To loop dictionaries:
    ```
    d = {'name': 'x', 'job': 'y'}

    d['age'] = 'z'

    for k, v in d.items():                                      # iterate over keys and values
        print(k, v)

    for k in d.keys():                                          # iterate over keys
        print(k)

    for v in d.values():                                        # iterate over values
        print(v)

    for i, k in enumerate(d):                                   # used to return k and index only without value
        print(i, k)

    questions = ['name', 'quest', 'favorite color']
    answers = ['lancelot', 'the holy grail', 'blue']
    for q, a in zip(questions, answers):
        print('What is your {0}?  It is {1}.'.format(q, a))

    print(tuple(zip(questions, answers)))                       # zip object is converted into a tuple
    ```