## How does Python handle multithreading and multiprocessing?


### Multithreading and Multiprocessing in Python

Python provides support for both multithreading and multiprocessing, but they are used differently due to the Global Interpreter Lock (GIL) and the nature of the tasks (I/O-bound vs. CPU-bound) they are designed to handle.

### 1. **Multithreading in Python**

- **Definition:** Multithreading allows multiple threads (smaller units of a process) to run concurrently within the same process. Threads share the same memory space and resources, making them lightweight. However, due to the Global Interpreter Lock (GIL), multithreading in Python is limited in its ability to achieve true parallelism for CPU-bound tasks.

- **Global Interpreter Lock (GIL):**
  - The GIL is a mutex that protects access to Python objects, ensuring that only one thread executes Python bytecode at a time. This means that even in a multithreaded Python program, only one thread can execute Python code at any given time, which limits the effectiveness of multithreading for CPU-bound tasks.

- **Use Cases:**
  - Multithreading is effective for I/O-bound tasks, such as file I/O, network operations, or web scraping, where threads spend time waiting for external operations to complete.

- **Key Module:** `threading`
  - The `threading` module provides tools to create and manage threads.

- **Example:**
  ```python
  import threading
  import time

  def print_numbers():
      for i in range(5):
          print(i)
          time.sleep(1)

  def print_letters():
      for letter in 'abcde':
          print(letter)
          time.sleep(1)

  t1 = threading.Thread(target=print_numbers)
  t2 = threading.Thread(target=print_letters)

  t1.start()
  t2.start()

  t1.join()
  t2.join()

  print("Done")
  ```
  - **Explanation:** Two threads (`t1` and `t2`) run concurrently, executing `print_numbers` and `print_letters` functions simultaneously. The GIL allows them to switch context rapidly, making it appear as though they run in parallel.

- **When to Use Multithreading:**
  - Use multithreading for I/O-bound tasks where the program spends time waiting for input/output operations to complete.

### 2. **Multiprocessing in Python**

- **Definition:** Multiprocessing involves running multiple processes simultaneously, with each process having its own memory space and Python interpreter. Unlike threads, processes are independent, making multiprocessing ideal for CPU-bound tasks that require true parallelism.

- **No GIL Limitation:**
  - The GIL does not affect multiprocessing because each process runs its own Python interpreter and memory space, allowing true parallelism on multi-core systems.

- **Use Cases:**
  - Multiprocessing is effective for CPU-bound tasks, such as data processing, mathematical computations, and parallel execution of independent tasks.

- **Key Module:** `multiprocessing`
  - The `multiprocessing` module provides tools to create and manage separate processes.

- **Example:**
  ```python
  import multiprocessing
  import time

  def square(number):
      print(f'Square: {number * number}')
      time.sleep(1)

  def cube(number):
      print(f'Cube: {number * number * number}')
      time.sleep(1)

  if __name__ == "__main__":
      p1 = multiprocessing.Process(target=square, args=(5,))
      p2 = multiprocessing.Process(target=cube, args=(5,))

      p1.start()
      p2.start()

      p1.join()
      p2.join()

      print("Done")
  ```
  - **Explanation:** Two processes (`p1` and `p2`) run independently and in parallel, calculating the square and cube of a number. Each process operates in its own memory space, allowing them to run concurrently without interference.

- **When to Use Multiprocessing:**
  - Use multiprocessing for CPU-bound tasks where true parallelism is needed to fully utilize multiple CPU cores.

### Key Differences Between Multithreading and Multiprocessing

1. **Use Case:**
   - **Multithreading:** Best for I/O-bound tasks.
   - **Multiprocessing:** Best for CPU-bound tasks.

2. **Global Interpreter Lock (GIL):**
   - **Multithreading:** Affected by the GIL, which limits parallelism in CPU-bound tasks.
   - **Multiprocessing:** Not affected by the GIL; allows true parallelism.

3. **Memory:**
   - **Multithreading:** Threads share the same memory space.
   - **Multiprocessing:** Processes have separate memory spaces.

4. **Overhead:**
   - **Multithreading:** Lower overhead, faster context switching.
   - **Multiprocessing:** Higher overhead due to process creation and memory allocation.

5. **Communication:**
   - **Multithreading:** Threads can communicate easily via shared data.
   - **Multiprocessing:** Processes require inter-process communication (IPC) mechanisms like pipes, queues, or shared memory.

### Summary

- **Multithreading** is suitable for I/O-bound tasks where tasks spend time waiting for I/O operations, while **multiprocessing** is ideal for CPU-bound tasks that require heavy computation and can benefit from parallel execution across multiple CPU cores.
- The **Global Interpreter Lock (GIL)** affects multithreading by preventing true parallelism in CPU-bound tasks, but multiprocessing avoids this limitation by using separate processes, each with its own interpreter and memory space.