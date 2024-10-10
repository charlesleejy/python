## What are some common design patterns used in Python?


Design patterns are reusable solutions to common problems in software design. They provide a standard way to tackle recurring issues, making code more modular, flexible, and maintainable. In Python, several design patterns are commonly used, thanks to the language’s dynamic nature and flexibility. Below are some of the most frequently encountered design patterns in Python:

### 1. **Singleton Pattern**

The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

**Example:**
```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
        return cls._instance

# Usage
s1 = Singleton()
s2 = Singleton()
print(s1 is s2)  # Output: True
```

- **Use Case:** Database connections, logging, configuration settings where only one instance is required.

### 2. **Factory Pattern**

The Factory pattern provides a way to create objects without specifying the exact class of object that will be created. It defines an interface for creating an object but lets subclasses alter the type of objects that will be created.

**Example:**
```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class PetFactory:
    @staticmethod
    def get_pet(pet_type):
        pets = dict(dog=Dog, cat=Cat)
        return pets[pet_type]()

# Usage
pet = PetFactory.get_pet("dog")
print(pet.speak())  # Output: Woof!
```

- **Use Case:** When the exact type of the object to be created is determined at runtime.

### 3. **Observer Pattern**

The Observer pattern defines a one-to-many dependency between objects. When one object changes state, all its dependents are notified and updated automatically.

**Example:**
```python
class Subject:
    def __init__(self):
        self._observers = []

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self, message):
        for observer in self._observers:
            observer.update(message)

class Observer:
    def update(self, message):
        print(f"Observer received: {message}")

# Usage
subject = Subject()
observer1 = Observer()
observer2 = Observer()

subject.attach(observer1)
subject.attach(observer2)
subject.notify("Hello, Observers!")  # Both observers receive the message
```

- **Use Case:** Event-driven systems, GUIs, or any system where changes in one part must automatically propagate to others.

### 4. **Strategy Pattern**

The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. This pattern allows the algorithm to vary independently from the clients that use it.

**Example:**
```python
class Strategy:
    def do_operation(self, a, b):
        pass

class AddStrategy(Strategy):
    def do_operation(self, a, b):
        return a + b

class SubtractStrategy(Strategy):
    def do_operation(self, a, b):
        return a - b

class Context:
    def __init__(self, strategy):
        self._strategy = strategy

    def execute_strategy(self, a, b):
        return self._strategy.do_operation(a, b)

# Usage
context = Context(AddStrategy())
print(context.execute_strategy(5, 3))  # Output: 8

context = Context(SubtractStrategy())
print(context.execute_strategy(5, 3))  # Output: 2
```

- **Use Case:** When you have multiple ways of doing something, and you want to choose which algorithm to use at runtime.

### 5. **Decorator Pattern**

The Decorator pattern allows behavior to be added to individual objects, dynamically, without affecting the behavior of other objects from the same class.

**Example:**
```python
def bold_decorator(func):
    def wrapper():
        return f"<b>{func()}</b>"
    return wrapper

def italic_decorator(func):
    def wrapper():
        return f"<i>{func()}</i>"
    return wrapper

@bold_decorator
@italic_decorator
def greet():
    return "Hello, World!"

# Usage
print(greet())  # Output: <b><i>Hello, World!</i></b>
```

- **Use Case:** Adding responsibilities to objects dynamically, like adding UI elements or extending functionalities.

### 6. **Adapter Pattern**

The Adapter pattern allows the interface of an existing class to be used as another interface. It’s used to make incompatible interfaces work together.

**Example:**
```python
class EuropeanSocket:
    def voltage(self):
        return 230

    def live(self):
        return 1

    def neutral(self):
        return -1

class AmericanSocket:
    def voltage(self):
        return 120

    def live(self):
        return 1

    def neutral(self):
        return 0

class Adapter:
    def __init__(self, european_socket):
        self.european_socket = european_socket

    def voltage(self):
        return self.european_socket.voltage() / 2

# Usage
european_socket = EuropeanSocket()
adapter = Adapter(european_socket)
print(adapter.voltage())  # Output: 115
```

- **Use Case:** Integrating legacy systems, converting interfaces.

### 7. **Facade Pattern**

The Facade pattern provides a simplified interface to a complex subsystem, making it easier to use.

**Example:**
```python
class CPU:
    def freeze(self):
        print("Freezing CPU")

    def jump(self, position):
        print(f"Jumping to {position}")

    def execute(self):
        print("Executing instructions")

class Memory:
    def load(self, position, data):
        print(f"Loading data to {position}")

class HardDrive:
    def read(self, lba, size):
        return "data"

class ComputerFacade:
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.hard_drive = HardDrive()

    def start(self):
        self.cpu.freeze()
        self.memory.load(0x00, self.hard_drive.read(0, 1024))
        self.cpu.jump(0x00)
        self.cpu.execute()

# Usage
computer = ComputerFacade()
computer.start()
```

- **Use Case:** Simplifying complex subsystems by providing a single point of interaction.

### Summary

- **Singleton:** Ensures a class has only one instance.
- **Factory:** Creates objects without specifying the exact class.
- **Observer:** Notifies dependent objects automatically when state changes.
- **Strategy:** Encapsulates algorithms and makes them interchangeable.
- **Decorator:** Dynamically adds behavior to objects.
- **Adapter:** Allows incompatible interfaces to work together.
- **Facade:** Simplifies interaction with complex systems.

Understanding and using these design patterns can make your Python code more robust, maintainable, and scalable. Each pattern solves a specific problem in software design, so knowing when and how to apply them is crucial.