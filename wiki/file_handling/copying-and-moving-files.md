## How do you copy and move files in Python?


In Python, you can copy and move files using the `shutil` module, which provides high-level file operations. Below are the methods for copying and moving files:

### 1. **Copying Files**

The `shutil` module provides several functions for copying files:

- **`shutil.copy(src, dst)`**: Copies the content and metadata (file permissions) of the file from the source path `src` to the destination path `dst`. The destination can be a directory or a file path.
- **`shutil.copy2(src, dst)`**: Similar to `shutil.copy()`, but also attempts to preserve additional metadata like timestamps.

**Example:**

```python
import shutil

# Copying a file
shutil.copy('source.txt', 'destination.txt')

# Copying a file to a directory
shutil.copy('source.txt', '/path/to/destination/directory/')

# Copying a file with metadata
shutil.copy2('source.txt', 'destination.txt')
```

- **Explanation:**
  - `shutil.copy('source.txt', 'destination.txt')`: Copies `source.txt` to `destination.txt`. If `destination.txt` already exists, it will be overwritten.
  - `shutil.copy('source.txt', '/path/to/destination/directory/')`: Copies `source.txt` to the specified directory, preserving the original file name.
  - `shutil.copy2('source.txt', 'destination.txt')`: Copies `source.txt` to `destination.txt`, preserving additional metadata like timestamps.

### 2. **Moving Files**

The `shutil` module provides the `move()` function for moving files or directories:

- **`shutil.move(src, dst)`**: Moves a file or directory from the source path `src` to the destination path `dst`. If the destination is on the same filesystem, the move is performed as a rename operation, which is faster. If the destination is on a different filesystem, the file is copied to the new location and then deleted from the original location.

**Example:**

```python
import shutil

# Moving a file
shutil.move('source.txt', 'destination.txt')

# Moving a file to a directory
shutil.move('source.txt', '/path/to/destination/directory/')

# Moving a directory
shutil.move('/path/to/source_directory/', '/path/to/destination_directory/')
```

- **Explanation:**
  - `shutil.move('source.txt', 'destination.txt')`: Moves `source.txt` to `destination.txt`. If `destination.txt` already exists, it will be overwritten.
  - `shutil.move('source.txt', '/path/to/destination/directory/')`: Moves `source.txt` to the specified directory.
  - `shutil.move('/path/to/source_directory/', '/path/to/destination_directory/')`: Moves the entire directory from the source to the destination.

### 3. **Copying Directories**

To copy an entire directory and its contents, you can use the `shutil.copytree()` function:

- **`shutil.copytree(src, dst)`**: Recursively copies an entire directory tree from `src` to `dst`. The destination directory must not exist before copying.

**Example:**

```python
import shutil

# Copying an entire directory
shutil.copytree('/path/to/source_directory', '/path/to/destination_directory')
```

- **Explanation:** This will copy all files and subdirectories from `source_directory` to `destination_directory`.

### 4. **Deleting Files or Directories**

For completeness, you can also delete files or directories using the `os` and `shutil` modules:

- **`os.remove(path)`**: Deletes a file.
- **`shutil.rmtree(path)`**: Recursively deletes a directory and all its contents.

**Example:**

```python
import os
import shutil

# Deleting a file
os.remove('file_to_delete.txt')

# Deleting a directory
shutil.rmtree('/path/to/directory_to_delete/')
```

### Summary

- **Copying Files:** Use `shutil.copy()` or `shutil.copy2()` for copying files.
- **Moving Files:** Use `shutil.move()` for moving files or directories.
- **Copying Directories:** Use `shutil.copytree()` for copying entire directory trees.
- **Deleting Files/Directories:** Use `os.remove()` for files and `shutil.rmtree()` for directories.

These functions from the `shutil` module make it easy to perform file and directory operations in Python, whether you need to copy, move, or delete files.