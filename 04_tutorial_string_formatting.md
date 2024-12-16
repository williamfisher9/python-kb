
# STRING FORMATTING
- You can convert any value to a string with the repr() or str() functions. 
- The str() function is meant to return representations of values which are fairly human-readable, while repr() is meant to generate representations which can be read by the interpreter.
- Passing an integer after the ':' will cause that field to be a minimum number of characters wide. This is useful for making columns line up.

    ```
    year = 2016
    event = 'Referendum'

    print(f'Results of the {year} {event}')

    print('Results of the {0} {1}'.format(year, event))

    print('We are the {} who say "{}!"'.format('knights', 'Ni'))

    print('This {food} is {adjective}.'.format(food='spam', adjective='absolutely horrible'))

    print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred', other='Georg'))

    table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
    print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))

    table = {k: str(v) for k, v in vars().items()}
    message = " ".join([f'{k}: ' + '{' + k +'};' for k in table.keys()])
    print(message.format(**table))

    for x in range(1, 11):
        print('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))
    ```

- The str.rjust() method of string objects right-justifies a string in a field of a given width by padding it with spaces on the left. 
- There are similar methods str.ljust() and str.center(). These methods do not write anything, they just return a new string.
    ```
    for x in range(1, 11):
        print(repr(x).rjust(2), repr(x*x).rjust(3), end=' ')
        # Note use of 'end' on previous line
        print(repr(x*x*x).rjust(4))

    table = {'I': 1829, 'J': 733, 'K': 3562}
    for k, v in table.items():
        print(f'{k:5} ==> {v:8}')

    bugs = 'roaches'
    count = 13
    area = 'living room'
    print(f'Debugging {bugs=} {count=} {area=}')
    ```

- str.zfill(), which pads a numeric string on the left with zeros
    ```
    '12'.zfill(5)
    ```

- Old string formatting
    ```
    import math
    print('The value of pi is approximately %5.3f.' % math.pi)
    ```
