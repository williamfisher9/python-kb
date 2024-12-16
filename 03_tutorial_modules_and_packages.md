
# MODULES
- Python has a way to put definitions in a file and use them in a script or in an interactive instance of the interpreter. `Such a file is called a module`. Definitions from a module can be imported into other modules or into the main module.
- A module is a file containing Python definitions and statements. The file name is the module name with the suffix `.py` appended.
- Within a module, the module’s name (as a string) is available as the value of the global variable __name__. For instance, use your favorite text editor to create a file called fibo.py then import the module by `import fibo` and run the functions using `fibo.fib(10)`
- Within a module, the name __name__ of the module is __main__ while in the module thats is importing the module it is fibo `print(fibo.__name__)`
 - An example is 2 files, one is `app.py` and the other is `fibo.py`. The name __name__ of the module in fibo.py is __main__ while in app.py if you call `print(fibo.__name__)` it will show `fibo`. 
 - If you intend to use a function often you can assign it to a local name:
    ```
    >>> fib = fibo.fib
    >>> fib(500)
    ```
- There is a variant of the import statement that imports names from a module directly into the importing module’s namespace. For example:
    ```
    >>> from fibo import fib, fib2
    >>> fib(500)
    ```
- There is even a variant to import all names that a module defines. This imports all names except those beginning with an underscore (_):
    ```
    >>> from fibo import *
    >>> fib(500)
    ```
- Another import variant:
    ```
    >>> from fibo import fib as fibonacci
    ```
- To run a Python module use the below command:
    ```
    $ python fibo.py <arguments>
    ```
    Inside the file make sure to add the below:
    ```
    if __name__ == "__main__":
        import sys
        fib(int(sys.argv[1]))
    ```
- When a module named spam is imported, the interpreter first searches for a built-in module with that name. These module names are listed in sys.builtin_module_names. If not found, it then searches for a file named spam.py in a list of directories given by the variable sys.path. sys.path is initialized from these locations: 
    - The directory containing the input script (or the current directory when no file is specified).
    - PYTHONPATH (a list of directory names, with the same syntax as the shell variable PATH).
    - The installation-dependent default (by convention including a site-packages directory, handled by the site module).

- "Compiled" Python files - To speed up loading modules, Python caches the compiled version of each module in the __pycache__ directory under the name module.version.pyc, where the version encodes the format of the compiled file; it generally contains the Python version number. For example, in CPython release 3.3 the compiled version of spam.py would be cached as __pycache__/spam.cpython-33.pyc. This naming convention allows compiled modules from different releases and different versions of Python to coexist. 
    - Python checks the modification date of the source against the compiled version to see if it’s out of date and needs to be recompiled. This is a completely automatic process. Also, the compiled modules are platform-independent, so the same library can be shared among systems with different architectures.
    - Python does not check the cache in two circumstances. First, it always recompiles and does not store the result for the module that’s loaded directly from the command line. Second, it does not check the cache if there is no source module. To support a non-source (compiled only) distribution, the compiled module must be in the source directory, and there must not be a source module.
- `sys` is built into every Python interpreter.
- `dir()` function is used to find out which names a module defines. It returns a sorted list of strings:
    ```
    >>> import fibo
    >>> dir(fibo)       # ['__name__', 'fib', 'fib2']
    ```

# PACKAGES
- Packages are a way of structuring Python’s module namespace by using “dotted module names”. For example, the module name A.B designates a submodule named B in a package named A. Just like the use of modules saves the authors of different modules from having to worry about each other’s global variable names.
- If there is a folder with name sound that has a folder called effects and a file inside it called echo.py:
    ```
    # users of a package can import an individual module from the package:
    >>> import sound.effects.echo

    # or the submodule:
    >>> from sound.effects import echo

    # or a function from the module:
    >>> from sound.effects.echo import echofilter
    ```
- In `import item.subitem.subsubitem` every name except the last must be a packge
- `from sound.effects import *` will import every file in the package and this may take a long time so it is better to add `__init__.py` file to the package with `__all__` variable to index all submodules.
- Relative paths can be used when importing modules:
    ```
    >>> from . import echo
    >>> from .. import formats
    >>> from ..filters import equalizer
    ```