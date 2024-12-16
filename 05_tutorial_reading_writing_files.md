
# READING AND WRITING FILES
- open() returns a file object, and is most commonly used with two positional arguments and one keyword argument: open(filename, mode, encoding=None)
- Mode argument is optional and is considered 'r' if ommited. 'r+' opens the file for both read and write.
- If encoding is not specified, the default is platform dependent.
- Because UTF-8 is the modern de-facto standard, encoding="utf-8" is recommended unless you know that you need to use a different encoding. 
- Appending a 'b' to the mode opens the file in binary mode. Binary mode data is read and written as bytes objects. You can not specify encoding when opening file in binary mode.
    ```
    f = open('workfile', 'w', encoding="utf-8")
    ```

- It is good practice to use the with keyword when dealing with file objects. 
- The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. 
- Using with is also much shorter than writing equivalent try-finally blocks:
    ```
    with open('workfile', encoding="utf-8") as f:
        read_data = f.read()
    ```

- To read a file’s contents, call f.read(size), which reads some quantity of data and returns it as a string (in text mode) or bytes object (in binary mode). 
- Size is an optional numeric argument. When size is omitted or negative, the entire contents of the file will be read and returned; it’s your problem if the file is twice as large as your machine’s memory. Otherwise, at most size characters (in text mode) or size bytes (in binary mode) are read and returned. 
- If the end of the file has been reached, f.read() will return an empty string ('').
    ```
    f.read()
    ```

- f.readline() reads a single line from the file; a newline character (\n) is left at the end of the string, and is only omitted on the last line of the file if the file doesn’t end in a newline.
    ```
    f.readline()
    ```

    ```
    for line in f:
        print(line, end='')
    ```

- If you want to read all the lines of a file in a list you can also use list(f) or f.readlines().

- f.write(string) writes the contents of string to the file, returning the number of characters written.
    ```
    f.write('This is a test\n')
    ```

- f.tell() returns an integer giving the file object’s current position in the file represented as number of bytes from the beginning of the file when in binary mode and an opaque number when in text mode.

- To change the file object’s position, use f.seek(offset, whence). The position is computed from adding offset to a reference point; the reference point is selected by the whence argument.
- A whence value of 0 measures from the beginning of the file, 1 uses the current file position, and 2 uses the end of the file as the reference point. whence can be omitted and defaults to 0, using the beginning of the file as the reference point.
    ```
    f = open('workfile', 'rb+')
    f.write(b'0123456789abcdef')
    f.seek(5)       # Go to the 6th byte in the file
    f.read(1)       # b'5'
    f.seek(-3, 2)   # Go to the 3rd byte before the end
    f.read(1)       # b'd'
    ```

- In text files (those opened without a b in the mode string), only seeks relative to the beginning of the file are allowed (the exception being seeking to the very file end with seek(0, 2)) and the only valid offset values are those returned from the f.tell(), or zero. Any other offset value produces undefined behaviour.

    ```
    # when reading and writing, use seek to write to a specified position.
    # without seekign a position, it will always start from the beginning
    with open('test.txt', 'r+', encoding='utf-8') as f:
    f.seek(0, 2)
    f.write('\n')
    f.write('test123')

    f.seek(0)
    lists = f.readlines()
    print(lists)
    ```
