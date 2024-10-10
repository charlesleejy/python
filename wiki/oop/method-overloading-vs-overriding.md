## What is method overloading and method overriding?


### Method Overloading vs. Method Overriding in Python

**Method overloading** and **method overriding** are two concepts related to object-oriented programming, but they serve different purposes and are used in different scenarios.

### 1. **Method Overloading**

- **Definition:** Method overloading is the ability to define multiple methods with the same name but different parameters (e.g., different types or numbers of arguments) within the same class. In many programming languages, method overloading allows a class to have multiple methods with the same name but different signatures.

- **Python and Overloading:**
  - Python does not support traditional method overloading as seen in languages like Java or C++. If you define multiple methods with the same name in a Python class, the most recent definition will override the previous ones.
  - However, similar behavior can be achieved using default arguments, variable-length arguments (`*args`, `**kwargs`), or conditional logic within a single method.

- **Example Using Default Arguments:**
  ```python
  class MathOperations:
      def add(self, a, b, c=0):
          return a + b + c

  obj = MathOperations()
  print(obj.add(2, 3))       # Output: 5
  print(obj.add(2, 3, 4))    # Output: 9
  ```

- **Example Using `*args`:**
  ```python
  class MathOperations:
      def add(self, *args):
          return sum(args)

  obj = MathOperations()
  print(obj.add(2, 3))       # Output: 5
  print(obj.add(2, 3, 4))    # Output: 9
  ```

### 2. **Method Overriding**

- **Definition:** Method overriding occurs when a subclass provides a specific implementation of a method that is already defined in its superclass. The method in the subclass overrides the one in the parent class, allowing the subclass to have different or extended behavior for that method.

- **Purpose:** Method overriding is used to modify or extend the behavior of inherited methods to fit the specific needs of the subclass.

- **Example:**
  ```python
  class Animal:
      def sound(self):
          return "Some generic sound"

  class Dog(Animal):
      def sound(self):
          return "Bark"

  class Cat(Animal):
      def sound(self):
          return "Meow"

  dog = Dog()
  cat = Cat()
  print(dog.sound())  # Output: Bark
  print(cat.sound())  # Output: Meow
  ```

  - **Explanation:** The `Dog` and `Cat` classes override the `sound` method of the `Animal` class to provide specific implementations.

- **Using `super()` with Overriding:**
  - The `super()` function can be used within the overriding method to call the parent class's version of the method.
  - **Example:**
    ```python
    class Animal:
        def sound(self):
            return "Some generic sound"

    class Dog(Animal):
        def sound(self):
            original_sound = super().sound()
            return f"{original_sound} But a dog barks."

    dog = Dog()
    print(dog.sound())  # Output: Some generic sound But a dog barks.
    ```

### Key Differences Between Method Overloading and Method Overriding

1. **Purpose:**
   - **Method Overloading:** Allows multiple methods with the same name but different signatures (not natively supported in Python).
   - **Method Overriding:** Allows a subclass to provide a specific implementation of a method that is already defined in its parent class.

2. **Implementation:**
   - **Method Overloading:** Achieved using default arguments or variable-length arguments (`*args`, `**kwargs`) in Python.
   - **Method Overriding:** Achieved by defining a method in the subclass with the same name and signature as a method in the parent class.

3. **Polymorphism:**
   - **Method Overloading:** Implements compile-time polymorphism (not directly supported in Python).
   - **Method Overriding:** Implements runtime polymorphism, allowing a subclass to modify the behavior of its superclass.

4. **Language Support:**
   - **Method Overloading:** Directly supported in many languages like Java and C++ but not natively in Python.
   - **Method Overriding:** Fully supported in Python and other object-oriented languages.

### Summary

- **Method overloading** allows defining multiple methods with the same name but different parameters. While Python does not support method overloading directly, similar behavior can be achieved using default or variable-length arguments.
- **Method overriding** allows a subclass to modify or extend the behavior of a method inherited from a parent class, providing a specific implementation for that method.

Method overriding is a key feature of polymorphism, enabling subclasses to behave differently from their parent classes.