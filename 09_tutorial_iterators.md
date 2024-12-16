# ITERATORS
```
for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')
```

- Behind the scenes, the for statement calls iter() on the container object. The function returns an iterator object that defines the method __next__() which accesses elements in the container one at a time. When there are no more elements, __next__() raises a StopIteration exception which tells the for loop to terminate.
    ```
    s = 'abc'
    it = iter(s)
    it
    <str_iterator object at 0x10c90e650>
    next(it)
    'a'
    next(it)
    'b'
    next(it)
    'c'
    next(it)
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
        next(it)
    StopIteration
    ```

- It is easy to add iterator behavior to your classes. Define an __iter__() method which returns an object with a __next__() method. If the class defines __next__(), then __iter__() can just return self:
    ```
    class Reverse:
        """Iterator for looping over a sequence backwards."""
        def __init__(self, data):
            self.data = data
            self.index = len(data)

        def __iter__(self):
            return self

        def __next__(self):
            if self.index == 0:
                raise StopIteration
            self.index = self.index - 1
            return self.data[self.index]
    ```

    ```
    rev = Reverse('spam')
    iter(rev)
    <__main__.Reverse object at 0x00A1DB50>
    for char in rev:
        print(char)

    m
    a
    p
    s
    ```
