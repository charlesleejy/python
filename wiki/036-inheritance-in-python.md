## 36. What is inheritance, and how does it work in Python?


### Inheritance in Python

**Inheritance** is a fundamental concept in object-oriented programming (OOP) that allows a class to inherit attributes and methods from another class. The main purpose of inheritance is to promote code reuse and establish a relationship between classes that share common behavior.

### 1. **Basic Concept of Inheritance**

- **Parent Class (Super Class/Base Class):** The class from which attributes and methods are inherited.
- **Child Class (Sub Class/Derived Class):** The class that inherits attributes and methods from the parent class. The child class can also have additional attributes and methods, or it can override those inherited from the parent class.

### 2. **How Inheritance Works**

- Inheritance allows you to create a new class based on an existing class, so you don’t need to rewrite the code that is already available in the parent class.
- **Syntax:**
  ```python
  class ParentClass:
      # Parent class attributes and methods

  class ChildClass(ParentClass):
      # Child class attributes and methods
  ```

### 3. **Example of Inheritance**

```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

# Child class
class Dog(Animal):
    def speak(self):
        return f"{self.name} barks."

# Child class
class Cat(Animal):
    def speak(self):
        return f"{self.name} meows."

# Creating instances of the child classes
dog = Dog("Buddy")
cat = Cat("Whiskers")

print(dog.speak())  # Output: Buddy barks.
print(cat.speak())  # Output: Whiskers meows.
```

**Explanation:**
- `Animal` is the parent class with a constructor (`__init__`) and a method (`speak`).
- `Dog` and `Cat` are child classes that inherit from `Animal`. They override the `speak` method to provide specific behavior.

### 4. **Types of Inheritance in Python**

1. **Single Inheritance**
   - A child class inherits from a single parent class.
   - **Example:**
     ```python
     class Vehicle:
         def start(self):
             print("Starting vehicle")

     class Car(Vehicle):
         def drive(self):
             print("Driving car")

     car = Car()
     car.start()  # Inherited from Vehicle
     car.drive()  # Defined in Car
     ```

2. **Multiple Inheritance**
   - A child class inherits from more than one parent class.
   - **Example:**
     ```python
     class A:
         def method_a(self):
             print("Method A")

     class B:
         def method_b(self):
             print("Method B")

     class C(A, B):
         pass

     c = C()
     c.method_a()  # From class A
     c.method_b()  # From class B
     ```

3. **Multilevel Inheritance**
   - A class is derived from another derived class (a chain of inheritance).
   - **Example:**
     ```python
     class Animal:
         def eat(self):
             print("Eating")

     class Mammal(Animal):
         def breathe(self):
             print("Breathing")

     class Dog(Mammal):
         def bark(self):
             print("Barking")

     dog = Dog()
     dog.eat()     # Inherited from Animal
     dog.breathe() # Inherited from Mammal
     dog.bark()    # Defined in Dog
     ```

4. **Hierarchical Inheritance**
   - Multiple classes inherit from the same parent class.
   - **Example:**
     ```python
     class Shape:
         def area(self):
             pass

     class Circle(Shape):
         def area(self, radius):
             return 3.14 * radius * radius

     class Square(Shape):
         def area(self, side):
             return side * side

     circle = Circle()
     square = Square()
     print(circle.area(5))  # Output: 78.5
     print(square.area(4))  # Output: 16
     ```

5. **Hybrid Inheritance**
   - A combination of two or more types of inheritance.

### 5. **Method Overriding**
- A child class can override a method of the parent class to provide a specific implementation.
- **Example:**
  ```python
  class Animal:
      def speak(self):
          return "Some generic sound"

  class Dog(Animal):
      def speak(self):
          return "Bark"

  dog = Dog()
  print(dog.speak())  # Output: Bark
  ```

### 6. **Using the `super()` Function**
- The `super()` function is used to call a method from the parent class inside a child class. It’s commonly used in method overriding to extend or modify the behavior of the inherited method.
- **Example:**
  ```python
  class Animal:
      def __init__(self, name):
          self.name = name

      def speak(self):
          return "Sound"

  class Dog(Animal):
      def __init__(self, name, breed):
          super().__init__(name)  # Call the parent class constructor
          self.breed = breed

      def speak(self):
          return f"{self.name} barks."

  dog = Dog("Buddy", "Golden Retriever")
  print(dog.speak())  # Output: Buddy barks.
  ```

### Summary
- **Inheritance** allows a child class to inherit attributes and methods from a parent class, promoting code reuse and establishing a relationship between classes.
- Python supports single, multiple, multilevel, hierarchical, and hybrid inheritance.
- The `super()` function is useful for accessing methods of the parent class, especially when overriding methods in the child class.