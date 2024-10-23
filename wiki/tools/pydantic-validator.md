## Pydantic Validator

In Pydantic, **validators** are functions that provide custom validation logic for individual fields or an entire model. Validators are used to enforce business rules, apply additional constraints beyond what Pydantic automatically validates (e.g., type checks), and transform data before it's stored in the model.

There are two main types of validators in Pydantic:
1. **Field Validators**: These apply to individual fields.
2. **Root Validators**: These apply to the entire model and can validate across multiple fields.

### 1. Field Validators

Field validators are defined using the `@validator` decorator and are attached to specific fields within a Pydantic model. These validators run after the automatic type validation but before the model is fully instantiated. You can use field validators to add custom logic for any specific field in the model.

#### Key Features of Field Validators:
- They apply to individual fields.
- They run **after** built-in validation for types and constraints (such as `min_length`, `max_length`, etc.).
- They can modify the data or raise errors to reject invalid inputs.
- You can define them to run **before** built-in validation by using `pre=True`.

#### Example: Basic Field Validator

```python
from pydantic import BaseModel, validator

class User(BaseModel):
    username: str
    age: int

    @validator('username')
    def check_username_not_empty(cls, value):
        if not value:
            raise ValueError('Username must not be empty')
        return value
```

**Explanation:**
- The `@validator('username')` decorator tells Pydantic that this function is a custom validator for the `username` field.
- The function `check_username_not_empty` checks that the `username` field is not empty. If the `username` is invalid (empty), it raises a `ValueError`.
- The `cls` argument is a reference to the model class itself, and `value` is the value of the field being validated.

#### Multiple Field Validators

You can also define multiple validators for a single field and specify their execution order.

```python
from pydantic import BaseModel, validator

class User(BaseModel):
    username: str
    password: str

    @validator('password')
    def check_password_length(cls, value):
        if len(value) < 8:
            raise ValueError('Password must be at least 8 characters long')
        return value

    @validator('password')
    def check_password_contains_digit(cls, value):
        if not any(char.isdigit() for char in value):
            raise ValueError('Password must contain at least one digit')
        return value
```

**Explanation:**
- Two validators for the `password` field are defined, one that checks the length of the password and another that ensures the password contains at least one digit.

#### Field Validators with Multiple Fields

You can also validate multiple fields together using the `@validator` with the `each_item` argument or by listing multiple fields in the decorator.

```python
from pydantic import BaseModel, validator

class Person(BaseModel):
    name: str
    age: int

    @validator('name', 'age')
    def check_not_empty(cls, value, field):
        if field.name == 'name' and not value:
            raise ValueError('Name cannot be empty')
        if field.name == 'age' and value <= 0:
            raise ValueError('Age must be greater than 0')
        return value
```

**Explanation:**
- This validator checks both the `name` and `age` fields in a single function. It uses the `field` argument to identify which field is being validated and applies specific rules for each.

#### Pre-Validation with `pre=True`

By default, validators run after the built-in validations for type checking and constraints. However, you can run a validator **before** these checks using the `pre=True` option. This is useful if you need to transform the input data before type checking.

```python
from pydantic import BaseModel, validator

class Product(BaseModel):
    price: float

    @validator('price', pre=True)
    def convert_price_to_float(cls, value):
        # Convert price to float before validation
        return float(value)
```

**Explanation:**
- Here, the `price` field is validated with `pre=True`, meaning the `convert_price_to_float` function will run before Pydantic’s built-in type validation. It ensures that the input is converted to a `float` before any further checks.

### 2. Root Validators

Root validators are used when you want to validate multiple fields or the entire model at once. They allow you to validate relationships between different fields or enforce more complex rules on the model as a whole.

#### Key Features of Root Validators:
- They apply to the whole model rather than individual fields.
- They are defined using the `@root_validator` decorator.
- They can access all the field values at once and modify them or raise validation errors.

#### Example: Basic Root Validator

```python
from pydantic import BaseModel, root_validator

class User(BaseModel):
    password: str
    confirm_password: str

    @root_validator
    def check_passwords_match(cls, values):
        password = values.get('password')
        confirm_password = values.get('confirm_password')
        if password != confirm_password:
            raise ValueError('Passwords do not match')
        return values
```

**Explanation:**
- The `check_passwords_match` function ensures that the `password` and `confirm_password` fields match. It accesses the field values through the `values` dictionary.
- If the passwords don’t match, a `ValueError` is raised.

#### Example: Root Validator with Precedence

You can control when the root validator runs in the validation process using the `pre=True` option. If set to `pre=True`, the root validator will run before any individual field validations. This is useful when you want to preprocess or validate fields together before other validations occur.

```python
from pydantic import BaseModel, root_validator

class User(BaseModel):
    name: str
    age: int

    @root_validator(pre=True)
    def validate_name_and_age(cls, values):
        if 'name' in values and 'age' in values:
            if values['age'] < 18 and values['name'] == 'admin':
                raise ValueError('Admins must be at least 18 years old')
        return values
```

**Explanation:**
- The `pre=True` flag means that this root validator will run before individual field validators.
- In this example, it checks a specific relationship between the `name` and `age` fields.

### How Validators Work Together

1. **Pre-Validation (`pre=True`)**: Validators marked with `pre=True` run first, before any other validation or type coercion.
2. **Field Validation**: Next, field-level validators are applied. These validators check specific fields and enforce their constraints.
3. **Automatic Type Coercion**: Pydantic then attempts to convert fields to the specified types (if they’re not already of that type) and validates type constraints.
4. **Root Validation**: Finally, root validators are run to check relationships between fields or apply validation to the entire model.

### Validators with Additional Parameters

You can pass additional parameters to validators, such as access to the model’s other field values or the configuration of the model itself.

#### Example: Using `values`

The `values` argument in a field validator gives you access to the values of other fields that have been validated so far.

```python
from pydantic import BaseModel, validator

class Product(BaseModel):
    price: float
    discount: float

    @validator('discount')
    def check_discount_valid(cls, discount, values):
        price = values.get('price')
        if price is not None and discount >= price:
            raise ValueError('Discount cannot be greater than or equal to the price')
        return discount
```

**Explanation:**
- The `values` argument provides access to other field values (`price` in this case) so that you can validate the `discount` field in relation to the `price`.

### Error Handling in Validators

If the data fails a validator's check, a `ValueError` is raised. Pydantic collects all the validation errors and raises a `ValidationError` with detailed error messages, making it easier to debug.

#### Example: Handling Validation Errors

```python
from pydantic import BaseModel, ValidationError

class Product(BaseModel):
    name: str
    price: float

    @validator('price')
    def check_price_positive(cls, value):
        if value <= 0:
            raise ValueError('Price must be positive')
        return value

try:
    product = Product(name='Laptop', price=-100)
except ValidationError as e:
    print(e)
```

**Explanation:**
- If a validation check fails (in this case, if the price is non-positive), Pydantic raises a `ValidationError` that provides detailed feedback on what went wrong.

### Summary

Pydantic validators are powerful tools that allow you to:
1. Enforce custom validation rules beyond simple type checks.
2. Apply validation logic to individual fields using `@validator` for field-specific checks.
3. Apply model-wide validation logic using `@root_validator` to check relationships between fields.
4. Use `pre=True` to run validators before the standard validation process.
5. Access the values of other fields using `values` for cross-field validation.
6. Customize data transformation and error handling during validation, ensuring your model data is clean and correct.

By using Pydantic validators effectively, you can build robust data models that automatically handle complex validation scenarios with minimal manual effort.