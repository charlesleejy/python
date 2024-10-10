## What is the purpose of the `self` keyword in Python?


### Purpose of the `self` Keyword in Python

The `self` keyword is a fundamental concept in Python's object-oriented programming. It is used within a class to represent the instance of the class on which a method is being called. Essentially, `self` allows access to the attributes and methods of the class in Python.

### Key Purposes of `self`

1. **Refers to the Current Instance of the Class**
   - **Definition:** In Python, when a method is called on an object, `self` refers to that particular instance. It allows the method to access and modify the object's attributes and other methods.
   - **Example:**
     ```python
     class Dog:
         def __init__(self, name, breed):
             self.name = name
             self.breed = breed

         def bark(self):
             print(f"{self.name} says woof!")

     my_dog = Dog("Buddy", "Golden Retriever")
     my_dog.bark()  # Output: Buddy says woof!
     ```
   - **Explanation:** Here, `self.name` refers to the `name` attribute of the `my_dog` object. When `my_dog.bark()` is called, `self` inside the `bark` method refers to `my_dog`.

2. **Distinguishes Between Instance Variables and Local Variables**
   - **Purpose:** Inside a class, `self` is used to differentiate between instance variables and local variables or parameters. Without `self`, Python would not know whether you are referring to an instance variable or a local variable within a method.
   - **Example:**
     ```python
     class Car:
         def __init__(self, make, model):
             self.make = make  # Instance variable
             self.model = model  # Instance variable

         def set_model(self, model):
             self.model = model  # Sets the instance variable model
     ```
   - **Explanation:** In the `set_model` method, `self.model` refers to the instance variable, while `model` without `self` refers to the local parameter passed to the method.

3. **Allows Access to Other Methods in the Class**
   - **Purpose:** `self` is used to call other methods within the same class. This allows methods to interact and work together.
   - **Example:**
     ```python
     class Circle:
         def __init__(self, radius):
             self.radius = radius

         def area(self):
             return 3.14159 * self.radius ** 2

         def circumference(self):
             return 2 * 3.14159 * self.radius

         def display(self):
             print(f"Area: {self.area()}")
             print(f"Circumference: {self.circumference()}")

     c = Circle(5)
     c.display()
     ```
   - **Explanation:** The `display` method calls `self.area()` and `self.circumference()` to access the area and circumference of the circle instance.

4. **Mandatory First Parameter in Instance Methods**
   - **Definition:** In Python, every instance method must have `self` as its first parameter. This is how Python distinguishes instance methods from other functions. While `self` is not a keyword in Python, it is a strong convention, and it’s important to use it for consistency.
   - **Example:**
     ```python
     class Example:
         def method(self):
             print("This is an instance method.")
     ```

5. **`self` Is Passed Automatically by Python**
   - **Explanation:** When you call an instance method, you don't need to pass the `self` argument explicitly—Python automatically passes it for you.
   - **Example:**
     ```python
     obj = Example()
     obj.method()  # Python automatically passes obj as self to the method
     ```

### Summary

- The `self` keyword in Python is essential in object-oriented programming. It refers to the current instance of the class and is used to access instance variables, methods, and distinguish between instance and local variables.
- `self` must be explicitly defined as the first parameter in instance methods, but Python automatically handles it when the method is called.