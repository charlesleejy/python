## 33. What are instance variables and class variables?


### Instance Variables vs. Class Variables in Python

**Instance variables** and **class variables** are two types of variables used in object-oriented programming in Python. They differ in scope, accessibility, and how they are used within a class.

### 1. **Instance Variables**

- **Definition:** Instance variables are attributes or properties that are specific to each object (instance) of a class. Each object has its own copy of the instance variables, and changes made to the instance variables of one object do not affect other objects.
- **How They Are Defined:** Instance variables are typically defined within the `__init__` method (the constructor) or other instance methods, using the `self` keyword.
- **Scope:** They belong to the specific instance of the class and are accessible only within the instance methods of the class or by accessing the instance directly.

- **Example:**
  ```python
  class Dog:
      def __init__(self, name, breed):
          self.name = name        # Instance variable
          self.breed = breed      # Instance variable

  dog1 = Dog("Buddy", "Golden Retriever")
  dog2 = Dog("Max", "Beagle")

  print(dog1.name)  # Output: Buddy
  print(dog2.name)  # Output: Max
  ```

  - **Explanation:** `name` and `breed` are instance variables. Each `Dog` object (instance) has its own values for these variables.

### 2. **Class Variables**

- **Definition:** Class variables are attributes that are shared among all instances of a class. They are defined within the class, outside of any instance methods. All instances of the class share the same value for a class variable unless it is overridden within an instance.
- **How They Are Defined:** Class variables are defined directly within the class body, outside of any methods, and they are accessed using the class name or an instance of the class.
- **Scope:** They belong to the class itself and are shared across all instances of the class.

- **Example:**
  ```python
  class Dog:
      species = "Canis familiaris"  # Class variable

      def __init__(self, name, breed):
          self.name = name          # Instance variable
          self.breed = breed        # Instance variable

  dog1 = Dog("Buddy", "Golden Retriever")
  dog2 = Dog("Max", "Beagle")

  print(dog1.species)  # Output: Canis familiaris
  print(dog2.species)  # Output: Canis familiaris

  # Changing the class variable
  Dog.species = "Canis lupus"
  print(dog1.species)  # Output: Canis lupus
  print(dog2.species)  # Output: Canis lupus
  ```

  - **Explanation:** `species` is a class variable shared by all instances of the `Dog` class. If the `species` variable is changed using the class name, the change is reflected in all instances.

### Key Differences Between Instance Variables and Class Variables

1. **Scope:**
   - **Instance Variable:** Specific to each object (instance) of the class.
   - **Class Variable:** Shared across all instances of the class.

2. **Memory Allocation:**
   - **Instance Variable:** Each object has its own separate copy of the instance variables.
   - **Class Variable:** A single copy of the class variable is shared among all instances.

3. **Access:**
   - **Instance Variable:** Accessed using the `self` keyword within instance methods.
   - **Class Variable:** Accessed using the class name or an instance, but typically modified using the class name.

4. **Usage:**
   - **Instance Variable:** Used for attributes that vary from one instance to another.
   - **Class Variable:** Used for attributes that should be consistent across all instances.

### Summary

- **Instance variables** are unique to each instance of a class, holding data that is specific to that particular object. They are defined within methods and accessed using `self`.
- **Class variables** are shared across all instances of a class, providing a common attribute that all objects of the class can access and modify. They are defined within the class body, outside of any methods.

Understanding the distinction between instance and class variables is crucial for effectively managing the state and behavior of objects in Python.