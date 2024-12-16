# EXCEPTION HANDLING
- SyntaxError (invalid syntax): The parser repeats the offending line and displays little arrows pointing at the token in the line where the error was detected.
- Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it. Errors detected during execution are called exceptions and are not unconditionally fatal like:
    - ZeroDivisionError: division by zero
    - NameError: name 'spam' is not defined
    - TypeError: can only concatenate str (not "int") to str
    ```
    # If an exception occurs which does not match the exception named in the except clause, it is passed on to outer try statements; if no handler is found, it is an unhandled exception and execution stops with an error message.
    try:
        ...
    except name:
        ...
    ```

    ```
    except (RuntimeError, TypeError, NameError):
        pass
    ```

- When an exception occurs, it may have associated values, also known as the exception’s arguments. The presence and types of the arguments depend on the exception type:
    ```
    try:
        raise Exception('spam', 'eggs')
    except Exception as inst:
        print(type(inst))    # the exception type
        print(inst.args)     # arguments stored in .args
        print(inst)          # __str__ allows args to be printed directly,
                            # but may be overridden in exception subclasses
        x, y = inst.args     # unpack args
        print('x =', x)
        print('y =', y)
    ```

- Exception can be used as a wildcard that catches (almost) everything. However, it is good practice to be as specific as possible with the types of exceptions that we intend to handle, and to allow any unexpected exceptions to propagate on.

- The most common pattern for handling `Exception` is to print or log the exception and then re-raise it (allowing a caller to handle the exception as well):
    ```
    try:
        f = open('myfile.txt')
        s = f.readline()
        i = int(s.strip())
    except OSError as err:
        print("OS error:", err)
    except ValueError:
        print("Could not convert data to an integer.")
    except Exception as err:
        print(f"Unexpected {err=}, {type(err)=}")
        raise
    ```

- The try … except statement has an optional else clause, which, when present, must follow all except clauses. It is useful for code that must be executed if the try clause does not raise an exception. For example:
    ```
    for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
    ```

- The raise statement allows the programmer to force a specified exception to occur. For example:
    ```
    raise NameError('improper name')
    ```

- If you need to determine whether an exception was raised but don’t intend to handle it, a simpler form of the raise statement allows you to re-raise the exception:
    ```
    try:
        raise NameError('HiThere')
    except NameError:
        print('An exception flew by!')
        raise
    ```

- Exception Chaining: If an unhandled exception occurs inside an except section, it will have the exception being handled attached to it and included in the error message.
    ```
    try:
        open("database.sqlite")
    except OSError:
        raise RuntimeError("unable to handle error")

    Traceback (most recent call last):
    File "<stdin>", line 2, in <module>
        open("database.sqlite")
        ~~~~^^^^^^^^^^^^^^^^^^^
    FileNotFoundError: [Errno 2] No such file or directory: 'database.sqlite'

    During handling of the above exception, another exception occurred:

    Traceback (most recent call last):
    File "<stdin>", line 4, in <module>
        raise RuntimeError("unable to handle error")
    RuntimeError: unable to handle error
    ```

- To indicate that an exception is a direct consequence of another, the raise statement allows an optional from clause:
    ```
    raise RuntimeError from exc
    ```

- It also allows disabling automatic exception chaining using the from None idiom:
    ```
    try:
        open('database.sqlite')
    except OSError:
        raise RuntimeError from None
    ```

- The try statement has another optional clause which is intended to define clean-up actions that must be executed under all circumstances.
- The finally clause runs whether or not the try statement produces an exception.
- If an exception occurs during execution of the try clause, the exception may be handled by an except clause. If the exception is not handled by an except clause, the exception is re-raised after the finally clause has been executed.
- An exception could occur during execution of an except or else clause. Again, the exception is re-raised after the finally clause has been executed.
- If the finally clause executes a break, continue or return statement, exceptions are not re-raised.
- If the try statement reaches a break, continue or return statement, the finally clause will execute just prior to the break, continue or return statement’s execution.
- If a finally clause includes a return statement, the returned value will be the one from the finally clause’s return statement, not the value from the try clause’s return statement.
    ```
    try:
        raise KeyboardInterrupt
    finally:
        print('Goodbye, world!')
    ```

- Enriching exceptions with notes: When an exception is created in order to be raised, it is usually initialized with information that describes the error that has occurred. There are cases where it is useful to add information after the exception was caught. For this purpose, exceptions have a method add_note(note) that accepts a string and adds it to the exception’s notes list. The standard traceback rendering includes all notes, in the order they were added, after the exception.
    ```
    try:
        raise TypeError('bad type')
    except Exception as e:
        e.add_note('Add some information')
        e.add_note('Add some more information')
        raise
    ```

- User Defined Exceptions: In Python, we can define custom exceptions by creating a new class that is derived from the built-in Exception class.
    ```
    class CustomError(Exception):
        pass

    raise CustomError("Example of Custom Exceptions in Python")
    ```

- Customizing Exception Classes: We can further customize this class to accept other arguments as per our needs.
    ```
    class SalaryNotInRangeError(Exception):
        """Exception raised for errors in the input salary.

        Attributes:
            salary -- input salary which caused the error
            message -- explanation of the error
        """

        def __init__(self, salary, message="Salary is not in (5000, 15000) range"):
            self.salary = salary
            self.message = message
            super().__init__(self.message)


    salary = int(input("Enter salary amount: "))
    if not 5000 < salary < 15000:
        raise SalaryNotInRangeError(salary)
    ```