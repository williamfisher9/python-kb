
# CLASSES
- Classes partake of the dynamic nature of Python: they are created at runtime, and can be modified further after creation.
- A `namespace` is `a mapping from names to objects`. Most namespaces are currently implemented as Python dictionaries, but that’s normally not noticeable in any way (except for performance), and it may change in the future. Examples of namespaces are: the set of built-in names (containing functions such as abs(), and built-in exception names); the global names in a module; and the local names in a function invocation. In a sense the set of attributes of an object also form a namespace. The important thing to know about namespaces is that there is absolutely no relation between names in different namespaces; for instance, two different modules may both define a function maximize without confusion — users of the modules must prefix it with the module name.
- `Attributes` may be `read-only` or `writable`. In the latter case, assignment to attributes is possible. Module attributes are writable: you can write modname.the_answer = 42. Writable attributes may also be deleted with the del statement. For example, del modname.the_answer will remove the attribute the_answer from the object named by modname.
- Namespaces are created at different moments and have different lifetimes. The namespace containing the built-in names is created when the Python interpreter starts up, and is never deleted. The global namespace for a module is created when the module definition is read in; normally, module namespaces also last until the interpreter quits. The statements executed by the top-level invocation of the interpreter, either read from a script file or interactively, are considered part of a module called __main__, so they have their own global namespace. (The built-in names actually also live in a module; this is called builtins.)
- The `local namespace for a function` is created when the function is called, and deleted when the function returns or raises an exception that is not handled within the function.
- A `scope` is a textual region of a Python program where a namespace is directly accessible. “Directly accessible” here means that an unqualified reference to a name attempts to find the name in the namespace.
- At any time during execution, there are 3 or 4 nested scopes whose namespaces are directly accessible:
    - The innermost scope, which is searched first, contains the local names.
    - The scopes of any enclosing functions, which are searched starting with the nearest enclosing scope, contain non-local, but also non-global names.
    - The next-to-last scope contains the current module’s global names.
    - The outermost scope (searched last) is the namespace containing built-in names.
- Namespace and Scope example:
    ```
    def scope_test():
        def do_local():
            spam = "local spam"

        def do_nonlocal():
            nonlocal spam
            spam = "nonlocal spam"

        def do_global():
            global spam
            spam = "global spam"

        spam = "test spam"
        do_local()
        print("After local assignment:", spam)
        do_nonlocal()
        print("After nonlocal assignment:", spam)
        do_global()
        print("After global assignment:", spam)

    scope_test()
    print("In global scope:", spam)

    After local assignment: test spam
    After nonlocal assignment: nonlocal spam
    After global assignment: nonlocal spam
    In global scope: global spam
    ```

- When a class definition is entered, a new namespace is created, and used as the local scope — thus, all assignments to local variables go into this new namespace. In particular, function definitions bind the name of the new function here. In the below example, MyClass.i and MyClass.f are valid attribute references, returning an integer and a function object, respectively. Class attributes can also be assigned to, so you can change the value of MyClass.i by assignment. __doc__ is also a valid attribute, returning the docstring belonging to the class: "A simple example class".
    ```
    class MyClass:
        """A simple example class"""
        i = 12345

        def f(self):
            return 'hello world'
    ```

- Class instantiation uses function notation. Creates a new instance of the class and assigns this object to the local variable x.
    ```
    x = MyClass()
    ```

- The instantiation operation (“calling” a class object) creates an empty object. Many classes like to create objects with instances customized to a specific initial state. Therefore a class may define a special method named __init__(), like this:
    ```
    def __init__(self):
        self.data = []
    ```
    ```
    class Complex:
        def __init__(self, realpart, imagpart):
            self.r = realpart
            self.i = imagpart

    x = Complex(3.0, -4.5)
    x.r, x.i
    ```

- There are two kinds of valid attribute names: data attributes and methods.
- When calling a method:
    ```
    x.f()
    ```
    ```
    xf = x.f
    xf()
    ```

- Generally speaking, `instance variables` are for data unique to each instance and `class variables` are for attributes and methods shared by all instances of the class:
    ```
class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.kind                  # shared by all dogs
    'canine'
    >>> e.kind                  # shared by all dogs
    'canine'
    >>> d.name                  # unique to d
    'Fido'
    >>> e.name                  # unique to e
    'Buddy'
    ```

    ```
    class Dog:

        tricks = []             # mistaken use of a class variable

        def __init__(self, name):
            self.name = name

        def add_trick(self, trick):
            self.tricks.append(trick)

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.add_trick('roll over')
    >>> e.add_trick('play dead')
    >>> d.tricks                # unexpectedly shared by all dogs
    ['roll over', 'play dead']
    ```

- Any function object that is a class attribute defines a method for instances of that class. It is not necessary that the function definition is textually enclosed in the class definition: assigning a function object to a local variable in the class is also ok. For example:
    ```
    def f1(self, x, y):
        return min(x, x+y)

    class C:
        f = f1

        def g(self):
            return 'hello world'

        h = g
    ```

- The name BaseClassName must be defined in a namespace accessible from the scope containing the derived class definition. In place of a base class name, other arbitrary expressions are also allowed. This can be useful, for example, when the base class is defined in another module:
    ```
    class DerivedClassName(modname.BaseClassName):
    ```

- Python has two built-in functions that work with inheritance:
    - Use isinstance() to check an instance’s type: isinstance(obj, int) will be True only if obj.__class__ is int or some class derived from int.
    - Use issubclass() to check class inheritance: issubclass(bool, int) is True since bool is a subclass of int. However, issubclass(float, int) is False since float is not a subclass of int.

- Python supports a form of multiple inheritance as well. A class definition with multiple base classes looks like this:
    ```
    class DerivedClassName(Base1, Base2, Base3):
    ```

- `Private Variables`: private instance variables that cannot be accessed except from inside an object don’t exist in Python. 
- However, there is a convention that is followed by most Python code: a name prefixed with an underscore (e.g. _spam) should be treated as a non-public part of the API (whether it is a function, a method or a data member). 
- It should be considered an implementation detail and subject to change without notice.
- `Name Mangling`: since there is a valid use-case for class-private members (namely to avoid name clashes of names with names defined by subclasses), there is limited support for such a mechanism, called name mangling. Any identifier of the form __spam (at least two leading underscores, at most one trailing underscore) is textually replaced with _classname__spam, where classname is the current class name with leading underscore(s) stripped. This mangling is done without regard to the syntactic position of the identifier, as long as it occurs within the definition of a class. Name mangling is helpful for letting subclasses override methods without breaking intraclass method calls. For example:
    ```
    class Mapping:
        def __init__(self, iterable):
            self.items_list = []
            self.__update(iterable)

        def update(self, iterable):
            for item in iterable:
                self.items_list.append(item)

        __update = update   # private copy of original update() method

    class MappingSubclass(Mapping):

        def update(self, keys, values):
            # provides new signature for update()
            # but does not break __init__()
            for item in zip(keys, values):
                self.items_list.append(item)
    ```

- Sometimes it is useful to have a data type
    ```
    from dataclasses import dataclass

    @dataclass
    class Employee:
        name: str
        dept: str
        salary: int
    ```
