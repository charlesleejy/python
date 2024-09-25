## 21. What is the difference between a function and a method?


### Difference Between a Function and a Method in Python

1. **Definition**
   - **Function:**
     - A function is a block of reusable code that performs a specific task. It can be defined using the `def` keyword and can exist independently, outside of any class.
   - **Method:**
     - A method is a function that is associated with an object and is defined within a class. It is called on an instance of the class, and it typically operates on data contained within that object.

2. **Binding**
   - **Function:**
     - Functions are not bound to any object or class. They can be called directly, without needing to be associated with a class instance.
     - **Example:**
       ```python
       def greet(name):
           return f"Hello, {name}!"
       
       print(greet("Alice"))
       ```
   - **Method:**
     - Methods are bound to objects. They require an instance of the class (or the class itself for class methods) to be called.
     - **Example:**
       ```python
       class Greeter:
           def greet(self, name):
               return f"Hello, {name}!"
       
       greeter = Greeter()
       print(greeter.greet("Alice"))
       ```

3. **Invocation**
   - **Function:**
     - Functions are invoked by their name directly.
     - **Example:**
       ```python
       result = max(10, 20)  # max is a built-in function
       ```
   - **Method:**
     - Methods are invoked on an object using the dot notation.
     - **Example:**
       ```python
       text = "hello"
       print(text.upper())  # upper() is a string method
       ```

4. **Self Parameter**
   - **Function:**
     - Functions do not require the `self` parameter because they are not associated with any class or object.
   - **Method:**
     - Instance methods in classes require the first parameter to be `self`, which refers to the instance of the class. This allows the method to access or modify the object's attributes.
     - **Example:**
       ```python
       class Counter:
           def __init__(self, count=0):
               self.count = count
           
           def increment(self):
               self.count += 1
       
       c = Counter()
       c.increment()
       print(c.count)  # Output: 1
       ```

5. **Scope**
   - **Function:**
     - Functions can be defined globally and can be called anywhere in the code where they are in scope.
   - **Method:**
     - Methods are defined within a class and can only be called on instances (or the class itself for class methods) of that class.

6. **Types of Methods**
   - **Instance Method:**
     - Operates on an instance of the class and typically modifies object state.
   - **Class Method:**
     - Bound to the class and can modify class state that applies across all instances.
   - **Static Method:**
     - Does not access or modify object or class state. Defined with `@staticmethod` decorator and behaves like a regular function but belongs to the class’s namespace.

### Summary
- **Functions** are independent blocks of code that can be called without any object context.
- **Methods** are functions that are associated with an object and are called on instances of a class.
- The key difference is that methods operate within the context of an object or class, while functions operate independently.