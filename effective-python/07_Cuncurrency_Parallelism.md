### Chapter 7. Concurrency and Parallelism

Concurrency and parallelism are two key concepts in computer science that allow programs to execute multiple tasks at the same time or appear to do so. Python provides a variety of ways to write concurrent and parallel programs, although true parallelism can be challenging to achieve due to the Global Interpreter Lock (GIL) in CPython.

#### Concurrency vs. Parallelism

- **Concurrency** is the ability of a program to manage multiple tasks at the same time, interleaving execution but not necessarily speeding up the total work.
- **Parallelism** is when a program actually executes multiple tasks at the same time, reducing the total time needed to complete the work.

---

#### Item 52: Use `subprocess` to Manage Child Processes

Python's `subprocess` module is the best tool for running and managing child processes from a parent Python script. It provides flexibility for launching subprocesses, capturing their output, and managing their execution.

Examples of managing child processes include:
1. **Running a child process and capturing its output**:
   ```python
   import subprocess
   result = subprocess.run(['echo', 'Hello from child'], capture_output=True, text=True)
   print(result.stdout)
   ```
2. **Running multiple subprocesses in parallel**:
   ```python
   procs = [subprocess.Popen(['sleep', '1']) for _ in range(5)]
   for proc in procs:
       proc.communicate()
   ```
   This reduces the total execution time by running subprocesses simultaneously.

3. **Handling timeouts for subprocesses**:
   ```python
   try:
       subprocess.run(['sleep', '10'], timeout=2)
   except subprocess.TimeoutExpired:
       print("Timeout expired!")
   ```

---

#### Item 53: Use Threads for Blocking I/O, Avoid for Parallelism

Python’s `threading` module is useful for handling I/O-bound tasks where the program needs to wait for external operations, such as reading files or network communication. However, due to the GIL, Python threads do not speed up CPU-bound tasks. For parallelism, you must use `multiprocessing` or other system-level approaches.

For example, running multiple threads for an I/O-bound task:
```python
import threading
import time

def slow_io():
    time.sleep(1)

threads = [threading.Thread(target=slow_io) for _ in range(5)]
for thread in threads:
    thread.start()
for thread in threads:
    thread.join()
```

---

#### Item 54: Use Locks to Prevent Data Races in Threads

Even though Python has the GIL, it is still possible to encounter race conditions when multiple threads access shared data. Using the `Lock` from the `threading` module ensures that only one thread can access a critical section of code at a time.

Example:
```python
import threading

lock = threading.Lock()
counter = 0

def increment_counter():
    global counter
    with lock:
        counter += 1

threads = [threading.Thread(target=increment_counter) for _ in range(100)]
for thread in threads:
    thread.start()
for thread in threads:
    thread.join()

print(counter)
```

---

#### Item 55: Use `Queue` to Coordinate Work Between Threads

The `queue.Queue` class helps in coordinating work between threads by implementing a thread-safe, producer-consumer pattern. Threads can add tasks to the queue (producer) and retrieve tasks from the queue (consumer).

Example:
```python
import queue
import threading

q = queue.Queue()

def worker():
    while True:
        item = q.get()
        if item is None:
            break
        print(f'Processing {item}')
        q.task_done()

threads = [threading.Thread(target=worker) for _ in range(5)]
for thread in threads:
    thread.start()

for item in range(10):
    q.put(item)

q.join()

for thread in threads:
    q.put(None)
for thread in threads:
    thread.join()
```

---

#### Item 56: Recognize When Concurrency is Necessary

Concurrency is essential for I/O-bound tasks or when managing many independent operations. For CPU-bound tasks, concurrency without parallelism (e.g., using threads) may not improve performance. Python's `asyncio` module allows you to write asynchronous programs that manage I/O-bound tasks concurrently, improving efficiency.

---

#### Item 57: Avoid Creating New `Thread` Instances for On-demand Fan-out

Creating a new `Thread` for each task can be costly in terms of memory and CPU overhead. Instead, use thread pools to manage and reuse a fixed number of threads for concurrent tasks.

For example, using `ThreadPoolExecutor`:
```python
from concurrent.futures import ThreadPoolExecutor

def task(n):
    return n * 2

with ThreadPoolExecutor(max_workers=4) as executor:
    results = list(executor.map(task, range(10)))
```

---

#### Item 58: Using `Queue` for Concurrency Requires Refactoring

When using `queue.Queue` for concurrency, it is essential to refactor your code to work asynchronously or in a producer-consumer fashion. It may require significant changes to your program's structure, but it provides more control over how tasks are handled.

#### Item 59: Consider `ThreadPoolExecutor` for Thread-based Concurrency

For easier thread management, consider using `ThreadPoolExecutor` from the `concurrent.futures` module. This class provides a simple way to manage a pool of worker threads and submit tasks to them.

Example:
```python
from concurrent.futures import ThreadPoolExecutor

def task(n):
    print(f"Processing {n}")
    return n * 2

with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(task, i) for i in range(10)]
    for future in futures:
        print(future.result())
```

---

#### Item 60: Achieve Highly Concurrent I/O with Coroutines

Coroutines, powered by the `asyncio` module, allow Python to manage a large number of concurrent I/O-bound tasks with minimal overhead. Coroutines are more lightweight than threads and can handle many tasks concurrently without the need for locking.

Example of asynchronous I/O:
```python
import asyncio

async def fetch_data():
    await asyncio.sleep(1)
    return "data"

async def main():
    tasks = [fetch_data() for _ in range(10)]
    results = await asyncio.gather(*tasks)
    print(results)

asyncio.run(main())
```

---

#### Item 61: Port Threaded I/O to `asyncio`

Migrating from threads to `asyncio` involves converting blocking I/O operations into asynchronous coroutines using the `await` keyword. For instance, converting a blocking socket operation to an asynchronous one involves using `asyncio.open_connection` instead of `socket.create_connection`.

---

#### Item 62: Mix Threads and Coroutines for a Gradual Transition to `asyncio`

When gradually transitioning from threads to coroutines, you may need to mix them. You can use `run_in_executor` from `asyncio` to run blocking code in threads while allowing coroutines to handle non-blocking I/O.

Example:
```python
import asyncio

async def async_task():
    loop = asyncio.get_event_loop()
    await loop.run_in_executor(None, blocking_task)

def blocking_task():
    print("Blocking task running in thread")

asyncio.run(async_task())
```

---

#### Item 63: Avoid Blocking the `asyncio` Event Loop

To maximize the responsiveness of an `asyncio`-based application, avoid blocking the event loop. If a task involves blocking I/O or CPU-bound work, offload it to a separate thread or process using `run_in_executor`.

---

#### Item 64: Consider `concurrent.futures` for True Parallelism

For CPU-bound tasks, `concurrent.futures.ProcessPoolExecutor` allows you to achieve parallelism by running tasks across multiple CPU cores. Unlike threads, processes are not constrained by the GIL, making them ideal for parallel computation.

Example:
```python
from concurrent.futures import ProcessPoolExecutor

def cpu_bound_task(n):
    return sum(i * i for i in range(10**6))

with ProcessPoolExecutor() as executor:
    results = list(executor.map(cpu_bound_task, range(10)))
    print(results)
```

This chapter emphasizes the different approaches Python provides for handling concurrency and parallelism. Choosing between threads, subprocesses, coroutines, and processes depends on the type of task (I/O-bound or CPU-bound) and the level of parallelism needed.