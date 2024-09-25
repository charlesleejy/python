## 41. What are Python’s built-in functions for file handling?


### Python’s Built-in Functions for File Handling

Python provides several built-in functions to perform file handling operations such as reading from, writing to, and manipulating files. Below are some of the key built-in functions for file handling in Python:

1. **`open()`**
   - **Purpose:** Opens a file and returns a file object, which can be used to read, write, or manipulate the file.
   - **Syntax:**
     ```python
     open(filename, mode)
     ```
   - **Modes:**
     - `'r'`: Read mode (default). Opens the file for reading.
     - `'w'`: Write mode. Opens the file for writing (creates a new file or truncates the existing file).
     - `'a'`: Append mode. Opens the file for appending (writes data to the end of the file).
     - `'b'`: Binary mode. Used in combination with other modes to open files in binary format (e.g., `'rb'`, `'wb'`).
     - `'x'`: Exclusive creation mode. Fails if the file already exists.
     - `'t'`: Text mode (default). Used in combination with other modes to open files in text format (e.g., `'rt'`, `'wt'`).
   - **Example:**
     ```python
     file = open("example.txt", "r")
     ```

2. **`read()`**
   - **Purpose:** Reads the entire content of the file as a string.
   - **Syntax:**
     ```python
     file.read(size=-1)
     ```
   - **Example:**
     ```python
     file = open("example.txt", "r")
     content = file.read()
     print(content)
     file.close()
     ```
   - **Explanation:** The `read()` function reads the entire content of the file or a specified number of bytes (`size`).

3. **`readline()`**
   - **Purpose:** Reads a single line from the file.
   - **Syntax:**
     ```python
     file.readline(size=-1)
     ```
   - **Example:**
     ```python
     file = open("example.txt", "r")
     first_line = file.readline()
     print(first_line)
     file.close()
     ```
   - **Explanation:** The `readline()` function reads one line at a time from the file.

4. **`readlines()`**
   - **Purpose:** Reads all lines in a file and returns them as a list of strings.
   - **Syntax:**
     ```python
     file.readlines(hint=-1)
     ```
   - **Example:**
     ```python
     file = open("example.txt", "r")
     lines = file.readlines()
     print(lines)
     file.close()
     ```
   - **Explanation:** The `readlines()` function reads all lines of the file and returns them as a list.

5. **`write()`**
   - **Purpose:** Writes a string to the file.
   - **Syntax:**
     ```python
     file.write(string)
     ```
   - **Example:**
     ```python
     file = open("example.txt", "w")
     file.write("Hello, World!")
     file.close()
     ```
   - **Explanation:** The `write()` function writes the provided string to the file.

6. **`writelines()`**
   - **Purpose:** Writes a list of strings to the file.
   - **Syntax:**
     ```python
     file.writelines(list_of_strings)
     ```
   - **Example:**
     ```python
     lines = ["Hello, World!\n", "Welcome to file handling in Python.\n"]
     file = open("example.txt", "w")
     file.writelines(lines)
     file.close()
     ```
   - **Explanation:** The `writelines()` function writes each string from the list to the file.

7. **`close()`**
   - **Purpose:** Closes the file, ensuring that any changes are saved and resources are released.
   - **Syntax:**
     ```python
     file.close()
     ```
   - **Example:**
     ```python
     file = open("example.txt", "r")
     # Perform operations
     file.close()
     ```

8. **`with` Statement**
   - **Purpose:** The `with` statement simplifies file handling by automatically closing the file when the block of code is exited, even if an error occurs.
   - **Syntax:**
     ```python
     with open(filename, mode) as file:
         # Perform file operations
     ```
   - **Example:**
     ```python
     with open("example.txt", "r") as file:
         content = file.read()
         print(content)
     ```
   - **Explanation:** The `with` statement eliminates the need to explicitly call `close()`.

9. **`tell()`**
   - **Purpose:** Returns the current position of the file pointer.
   - **Syntax:**
     ```python
     file.tell()
     ```
   - **Example:**
     ```python
     file = open("example.txt", "r")
     print(file.tell())  # Output: 0 (initial position)
     file.read(5)
     print(file.tell())  # Output: 5 (after reading 5 characters)
     file.close()
     ```

10. **`seek()`**
    - **Purpose:** Moves the file pointer to a specified position.
    - **Syntax:**
      ```python
      file.seek(offset, whence)
      ```
    - **Parameters:**
      - `offset`: The number of bytes to move the pointer.
      - `whence`: The reference point (`0` = beginning of the file, `1` = current position, `2` = end of the file).
    - **Example:**
      ```python
      file = open("example.txt", "r")
      file.seek(10)  # Move pointer to the 10th byte
      print(file.read())
      file.close()
      ```

### Summary

Python’s built-in file handling functions allow you to perform various operations, including reading, writing, and managing file content. The `open()` function is the gateway to working with files, and the `with` statement is highly recommended for ensuring files are properly closed after operations.