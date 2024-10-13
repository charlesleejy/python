### Example of Running Multiple Asynchronous Tasks Concurrently Using `asyncio`

In Python, you can use the `asyncio` module to run multiple asynchronous tasks concurrently. The most common way to achieve this is by using **`asyncio.gather()`** to schedule multiple **coroutines** (asynchronous functions) to run concurrently, allowing them to share the same event loop.

Here’s a simple example that demonstrates how to run multiple asynchronous tasks concurrently using `asyncio`.

---

### Example: Running Multiple Asynchronous Tasks with `asyncio.gather()`

```python
import asyncio

# Define an asynchronous function (coroutine) that simulates a task
async def task(name, duration):
    print(f"Task {name} started")
    await asyncio.sleep(duration)  # Simulate an I/O-bound operation (non-blocking)
    print(f"Task {name} finished after {duration} seconds")
    return f"Result of task {name}"

# Define the main coroutine
async def main():
    # Schedule multiple coroutines to run concurrently using asyncio.gather()
    results = await asyncio.gather(
        task("A", 2),
        task("B", 1),
        task("C", 3)
    )
    
    # Print the results returned by the tasks
    print(f"Results: {results}")

# Run the event loop and execute the main coroutine
asyncio.run(main())
```

---

### Explanation:

1. **Defining Coroutines**:
   - The **`task()`** coroutine takes two arguments: `name` (the name of the task) and `duration` (the time to simulate the task's delay).
   - The `await asyncio.sleep(duration)` line simulates a non-blocking delay, allowing other tasks to run concurrently during this time.

2. **Concurrent Execution**:
   - In the **`main()`** coroutine, **`asyncio.gather()`** is used to schedule three tasks (`task A`, `task B`, and `task C`) to run concurrently. These tasks run simultaneously, and the program waits for all of them to complete.
   
3. **Results**:
   - The **`asyncio.gather()`** function returns the results of the tasks as a list, and we print the results after all tasks have completed.

4. **Running the Event Loop**:
   - The **`asyncio.run(main())`** function is used to start the event loop and execute the `main()` coroutine. It takes care of setting up the event loop, running the main coroutine, and closing the loop once everything is done.

---

### Expected Output:

```
Task A started
Task B started
Task C started
Task B finished after 1 seconds
Task A finished after 2 seconds
Task C finished after 3 seconds
Results: ['Result of task A', 'Result of task B', 'Result of task C']
```

#### Explanation of Output:
- All tasks (`A`, `B`, and `C`) start concurrently.
- Task B finishes first after 1 second, followed by task A after 2 seconds, and task C finishes last after 3 seconds.
- The results are returned in the same order the tasks were passed to `asyncio.gather()`.

---

### Understanding `asyncio.gather()`

- **`asyncio.gather()`** is used to run multiple coroutines concurrently. It takes one or more coroutines (or other awaitable objects) as arguments and waits for all of them to complete.
- The return value is a list of results from the coroutines, with the results corresponding to the order in which the coroutines were passed to `gather()`.

#### Key Points:
- Coroutines run concurrently, not in parallel (they share the same event loop).
- The tasks will **yield control** whenever they encounter an `await` statement (e.g., `await asyncio.sleep()`) and allow other tasks to run in the meantime.

---

### Running Tasks with Different Durations

You can adjust the **duration** of each task to see how tasks overlap and run concurrently. For example:

```python
async def task(name, duration):
    print(f"Task {name} started")
    await asyncio.sleep(duration)  # Simulate a non-blocking delay
    print(f"Task {name} finished after {duration} seconds")
    return f"Result of task {name}"

async def main():
    results = await asyncio.gather(
        task("A", 5),  # Task A takes 5 seconds
        task("B", 2),  # Task B takes 2 seconds
        task("C", 3)   # Task C takes 3 seconds
    )
    print(f"Results: {results}")

asyncio.run(main())
```

#### Output:
```
Task A started
Task B started
Task C started
Task B finished after 2 seconds
Task C finished after 3 seconds
Task A finished after 5 seconds
Results: ['Result of task A', 'Result of task B', 'Result of task C']
```

- Task B finishes first after 2 seconds, Task C finishes next after 3 seconds, and Task A finishes last after 5 seconds.
- Even though the tasks are started at the same time, they complete based on the delay specified in `await asyncio.sleep()`.

---

### Conclusion

In this example, you learned how to use **`asyncio.gather()`** to run multiple asynchronous tasks concurrently. By leveraging the event loop and coroutines, `asyncio` allows you to write programs that handle **I/O-bound** operations efficiently, ensuring that tasks can run concurrently while waiting for other operations (e.g., network requests or file I/O) to complete.

- **`async def`** defines a coroutine that can contain `await` expressions.
- **`await`** pauses the execution of the coroutine, allowing other coroutines to run while waiting for the awaited task to complete.
- **`asyncio.gather()`** schedules multiple coroutines to run concurrently and waits for all of them to complete, returning their results in a list.

By running tasks concurrently using `asyncio`, you can achieve efficient concurrency without the need for multiple threads or processes.