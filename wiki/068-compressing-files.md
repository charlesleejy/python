## 68. How do you compress files in Python?


In Python, you can compress files using the `zipfile` and `tarfile` modules, which support creating ZIP and TAR archives, respectively. Below are examples of how to compress files using these modules:

### 1. **Compressing Files into a ZIP Archive using `zipfile`**

The `zipfile` module allows you to create, read, write, and extract ZIP files.

**Example: Compressing Multiple Files into a ZIP Archive**

```python
import zipfile

# Create a ZIP file
with zipfile.ZipFile('archive.zip', 'w') as zipf:
    # Add files to the ZIP archive
    zipf.write('file1.txt')
    zipf.write('file2.txt')
    zipf.write('file3.txt')
```

- **Explanation:**
  - `zipfile.ZipFile('archive.zip', 'w')`: Creates a new ZIP file named `archive.zip` in write mode (`'w'`).
  - `zipf.write('file1.txt')`: Adds `file1.txt` to the ZIP archive. This is repeated for other files.

**Example: Compressing an Entire Directory into a ZIP Archive**

```python
import zipfile
import os

def zipdir(path, ziph):
    # Iterate over all the files and directories in the specified path
    for root, dirs, files in os.walk(path):
        for file in files:
            ziph.write(os.path.join(root, file),
                       os.path.relpath(os.path.join(root, file),
                                       os.path.join(path, '..')))

# Create a ZIP file
with zipfile.ZipFile('archive.zip', 'w', zipfile.ZIP_DEFLATED) as zipf:
    zipdir('my_folder', zipf)
```

- **Explanation:**
  - `os.walk(path)`: Recursively walks through all directories and files in the specified directory (`my_folder`).
  - `zipf.write()`: Adds each file to the ZIP archive, preserving the directory structure.
  - `zipfile.ZIP_DEFLATED`: Compresses the files within the ZIP archive.

### 2. **Compressing Files into a TAR Archive using `tarfile`**

The `tarfile` module allows you to create, read, and extract TAR archives, with or without compression (e.g., `.tar`, `.tar.gz`, `.tar.bz2`).

**Example: Compressing Files into a Gzipped TAR Archive**

```python
import tarfile

# Create a TAR.GZ file
with tarfile.open('archive.tar.gz', 'w:gz') as tar:
    tar.add('file1.txt')
    tar.add('file2.txt')
    tar.add('file3.txt')
```

- **Explanation:**
  - `tarfile.open('archive.tar.gz', 'w:gz')`: Creates a new Gzipped TAR file named `archive.tar.gz` in write mode (`'w:gz'`).
  - `tar.add('file1.txt')`: Adds `file1.txt` to the TAR archive. This is repeated for other files.

**Example: Compressing an Entire Directory into a Gzipped TAR Archive**

```python
import tarfile

# Create a TAR.GZ file
with tarfile.open('archive.tar.gz', 'w:gz') as tar:
    tar.add('my_folder', arcname=os.path.basename('my_folder'))
```

- **Explanation:**
  - `tar.add('my_folder', arcname=os.path.basename('my_folder'))`: Adds the entire `my_folder` directory to the TAR archive, preserving the directory structure.

### 3. **Choosing Between ZIP and TAR**

- **ZIP (`zipfile`):**
  - Commonly used and widely supported on many platforms.
  - Supports compression within the archive.
  - Suitable for compressing individual files or directories.

- **TAR (`tarfile`):**
  - Commonly used on Unix/Linux systems.
  - Often combined with `gzip` or `bzip2` for compression (`.tar.gz`, `.tar.bz2`).
  - Efficient for compressing large collections of files and directories.

### Summary

- **ZIP Files:** Use the `zipfile` module to compress files or directories into a ZIP archive.
- **TAR Files:** Use the `tarfile` module to create TAR archives, optionally compressed with Gzip or Bzip2.

Both `zipfile` and `tarfile` provide powerful tools for compressing and managing files in Python, depending on your needs and the platform you are working on.