### Chapter 8. Robustness and Performance

Once a program is functional, it’s essential to make it robust and performant. Python provides tools to improve error handling and optimize performance, helping programs to manage unexpected conditions and handle larger workloads efficiently.

---

#### Item 65: Take Advantage of Each Block in `try/except/else/finally`

When dealing with exceptions, Python allows handling different scenarios with `try/except/else/finally`. Each block has a specific purpose that can help manage errors and resource cleanup more effectively.

#### The `finally` Block
The `finally` block ensures that certain cleanup actions are always executed, even if an exception is raised. It's typically used for resource management, like closing a file or releasing a lock. 

Example:
```python
def try_finally_example(filename):
    print(" * Open file")
    handle = open(filename, encoding='utf-8')  # OSError may happen
    try:
        print(" * Read file")
        return handle.read()  # UnicodeDecodeError may happen
    finally:
        print(" * Close file")
        handle.close()  # Always executed
```

This ensures that the file is always closed, regardless of whether an exception is raised during reading.

#### The `else` Block
The `else` block allows you to specify code that should only run if no exception was raised in the `try` block. It helps separate normal operation logic from error-handling logic.

Example:
```python
import json

def load_json_key(data, key):
    try:
        print(" * Load JSON")
        result_dict = json.loads(data)  # May raise ValueError
    except ValueError as e:
        print(" * Handling ValueError")
        raise KeyError(key) from e
    else:
        print(" * Key lookup")
        return result_dict[key]
```

The `else` block is executed if no `ValueError` occurs during the JSON parsing. This structure makes it clear which part of the code is for normal execution and which part is for handling specific exceptions.

#### Combining `try/except/else/finally`
You can combine all these blocks to handle complex scenarios, like processing a file, handling errors, and ensuring resources are cleaned up properly.

Example:
```python
def divide_json(path):
    print(" * Open file")
    handle = open(path, "r+")  # OSError may happen
    try:
        print(" * Read file")
        data = handle.read()  # UnicodeDecodeError may happen
        print(" * Parse JSON")
        op = json.loads(data)  # ValueError may happen
        print(" * Divide")
        value = op["numerator"] / op["denominator"]  # ZeroDivisionError may happen
    except ZeroDivisionError:
        print(" * Handling ZeroDivisionError")
        return None
    else:
        print(" * Update file")
        op["result"] = value
        result = json.dumps(op)
        handle.seek(0)  # OSError may happen
        handle.write(result)  # OSError may happen
        return value
    finally:
        print(" * Close file")
        handle.close()  # Always executed
```

This approach ensures that the file is always closed and exceptions are handled gracefully.

---

#### Item 66: Consider `contextlib` and `with` Statements for Reusable `try/finally` Behavior

The `with` statement simplifies resource management, such as file handling or locking, by ensuring that resources are automatically cleaned up. The `contextlib` module allows you to create reusable context managers, making your code more concise and readable.

#### Example: Logging Context
```python
import logging
from contextlib import contextmanager

@contextmanager
def debug_logging(level):
    old_level = logging.getLogger().getEffectiveLevel()
    logging.getLogger().setLevel(level)
    try:
        yield
    finally:
        logging.getLogger().setLevel(old_level)

with debug_logging(logging.DEBUG):
    logging.debug("This is a debug message")
    logging.error("This is an error message")
```

This pattern can be extended to manage more complex resources or scenarios, ensuring consistent cleanup and error handling.

#### Using `with` Targets
Context managers can also return objects using the `as` part of the `with` statement, allowing you to interact with the context manager.

Example:
```python
@contextmanager
def log_level(level, name):
    logger = logging.getLogger(name)
    old_level = logger.getEffectiveLevel()
    logger.setLevel(level)
    try:
        yield logger
    finally:
        logger.setLevel(old_level)

with log_level(logging.DEBUG, "my_log") as logger:
    logger.debug("This is a debug message")
```

The `as` keyword lets you work directly with the logger returned by the context manager, adding flexibility to how context managers are used.

---

#### Item 67: Use `datetime` Instead of `time` for Local Clocks

When dealing with time, especially across time zones, the `time` module can be tricky and error-prone. The `datetime` module provides a more intuitive and flexible way to handle time, especially for time zone conversions and human-readable representations.

#### Problems with the `time` Module
The `time` module can convert between Unix timestamps and the local time of the host machine, but it doesn’t handle time zones well. Consider converting a human-readable time string into Unix time:

```python
import time

time_str = "2022-09-14 18:32:55"
time_format = "%Y-%m-%d %H:%M:%S"
local_time = time.strptime(time_str, time_format)
utc_now = time.mktime(local_time)
print(utc_now)
```

This works for converting local time to a Unix timestamp. However, working with time zones is more complicated and error-prone. For instance, converting time between different time zones using the `time` module is not straightforward, and the results may not be accurate.

#### The `datetime` Module

The `datetime` module in Python provides a more powerful and flexible way to handle dates and times, especially when working with time zones. It includes classes like `datetime`, `date`, `time`, and `timezone`, which allow for more precise and readable time manipulation.

```python
from datetime import datetime, timezone

# Get the current time in UTC
now_utc = datetime.now(timezone.utc)
print(now_utc)

# Convert UTC time to a different timezone (e.g., PST)
from datetime import timedelta
pst = timezone(timedelta(hours=-8))
now_pst = now_utc.astimezone(pst)
print(now_pst)
```

With `datetime`, it's much easier to work with time zones, convert between them, and manipulate time in a clear and human-friendly way.

#### Handling Time Zone Conversions with `datetime`

If you need to convert time between different time zones, `datetime` makes this task straightforward. For example, if you want to convert the time from Seoul (KST) to Vancouver (PST), you can easily do so by defining the appropriate time zones.

```python
from datetime import datetime, timedelta, timezone

# Define time zones
kst = timezone(timedelta(hours=9))  # Korea Standard Time (UTC+9)
pst = timezone(timedelta(hours=-8))  # Pacific Standard Time (UTC-8)

# Flight departure time in KST
departure_time_kst = datetime(2022, 9, 15, 15, 19, 32, tzinfo=kst)
print(f"Departure time in Seoul: {departure_time_kst}")

# Convert to PST
arrival_time_pst = departure_time_kst.astimezone(pst)
print(f"Arrival time in Vancouver: {arrival_time_pst}")
```

This shows how `datetime` simplifies handling time across different zones, eliminating the need for manual adjustments and reducing the chances of errors.

In conclusion, the `datetime` module should be your go-to tool for handling dates and times in Python, particularly when dealing with time zones and conversions. It’s more intuitive and less error-prone than the older `time` module.