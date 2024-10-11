### Difference Between Association, Aggregation, and Composition

In object-oriented programming (OOP), **association**, **aggregation**, and **composition** describe relationships between objects. These concepts help model the real-world relationships between classes and objects, and they define how objects interact with each other. The main differences between them involve the **strength of the relationship** and the **lifetime dependency** between the related objects.

---

### 1. **Association**

**Association** is a general relationship between two or more objects where they are aware of each other and can interact, but they are **independent entities**. Association describes a relationship where objects are **related** to each other, but neither object owns the other.

#### Key Points:
- **Independence**: Both objects are independent of each other, meaning they can exist without one another.
- **Relationship Type**: Describes a general relationship (e.g., "uses," "interacts with").
- **Example**: A **Teacher** and a **Student** have an association. A teacher teaches students, and a student attends classes taught by the teacher, but both the teacher and the student can exist independently of one another.

#### Example of Association:

```python
class Teacher:
    def __init__(self, name):
        self.name = name

    def teach(self):
        return f"{self.name} is teaching."


class Student:
    def __init__(self, name):
        self.name = name

    def study(self):
        return f"{self.name} is studying."

# Association: A student can interact with a teacher, but both can exist independently
teacher = Teacher("Mr. Smith")
student = Student("Alice")

print(teacher.teach())  # Output: Mr. Smith is teaching.
print(student.study())  # Output: Alice is studying.
```

---

### 2. **Aggregation**

**Aggregation** is a **special type of association** that represents a **whole-part relationship** between two objects. The key distinction is that aggregation represents a **weaker relationship** than composition. The "whole" object can contain or own "part" objects, but the "parts" can still exist independently. If the whole is destroyed, the parts continue to exist.

#### Key Points:
- **Weak relationship**: The part (child) can exist independently of the whole (parent).
- **Whole-part relationship**: The parent object contains or holds references to child objects but does not own them.
- **Example**: A **Department** can contain multiple **Employees**. If the department is removed, the employees still exist independently.

#### Example of Aggregation:

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def work(self):
        return f"{self.name} is working."


class Department:
    def __init__(self, name):
        self.name = name
        self.employees = []

    def add_employee(self, employee):
        self.employees.append(employee)

    def get_employees(self):
        return [emp.name for emp in self.employees]

# Aggregation: A department can have employees, but employees can exist without the department
dept = Department("Engineering")
emp1 = Employee("Alice")
emp2 = Employee("Bob")

dept.add_employee(emp1)
dept.add_employee(emp2)

print(dept.get_employees())  # Output: ['Alice', 'Bob']
```

**Explanation**:
- The `Department` class aggregates `Employee` objects, but the `Employee` objects are independent and can exist even if the `Department` is deleted.

---

### 3. **Composition**

**Composition** is a **stronger form of aggregation**, representing a **strict whole-part relationship** where the "whole" object owns the "part" objects. The key difference is that in composition, the lifetime of the part is **dependent** on the lifetime of the whole. If the whole object is destroyed, the part objects are also destroyed.

#### Key Points:
- **Strong relationship**: The part (child) cannot exist without the whole (parent).
- **Ownership**: The parent object owns the child objects, and if the parent is destroyed, the child objects are destroyed as well.
- **Example**: A **House** and its **Rooms**. A room cannot exist without the house; if the house is destroyed, the rooms are destroyed as well.

#### Example of Composition:

```python
class Room:
    def __init__(self, name):
        self.name = name

    def describe(self):
        return f"This is the {self.name}."


class House:
    def __init__(self, address):
        self.address = address
        self.rooms = []  # The house "owns" the rooms

    def add_room(self, room_name):
        room = Room(room_name)
        self.rooms.append(room)

    def describe_house(self):
        return [room.describe() for room in self.rooms]

# Composition: A house is composed of rooms, and if the house is destroyed, the rooms are too
house = House("123 Main St")
house.add_room("Living Room")
house.add_room("Kitchen")

print(house.describe_house())  # Output: ['This is the Living Room.', 'This is the Kitchen.']
```

**Explanation**:
- The `House` class owns `Room` objects. If the `House` object is destroyed, the `Room` objects are also destroyed. Rooms cannot exist without a house.

---

### Key Differences Between Association, Aggregation, and Composition

| **Aspect**            | **Association**                                 | **Aggregation**                                     | **Composition**                                     |
|-----------------------|-------------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| **Relationship**       | General relationship between objects            | Whole-part relationship (weak)                      | Whole-part relationship (strong)                   |
| **Independence**       | Both objects can exist independently            | The part can exist independently of the whole       | The part cannot exist without the whole             |
| **Lifetime Dependency**| No lifetime dependency                          | The part exists independently of the whole’s lifetime | The part’s lifetime is dependent on the whole       |
| **Example**            | A teacher teaches a student, but both are independent | A department contains employees, but employees can exist without it | A house contains rooms, and rooms cannot exist without the house |
| **Deletion Impact**    | Deleting one does not affect the other          | Deleting the whole does not delete the parts        | Deleting the whole deletes the parts                |

---

### Summary:

1. **Association**: Describes a general relationship between objects where they are independent and can exist on their own (e.g., a teacher and a student).
2. **Aggregation**: Describes a whole-part relationship where the part can exist independently of the whole (e.g., a department and employees).
3. **Composition**: Describes a whole-part relationship where the part depends on the whole for its existence. If the whole is destroyed, the part is also destroyed (e.g., a house and its rooms).

Understanding these relationships helps you design better systems and models in object-oriented programming, reflecting real-world relationships more accurately and efficiently.