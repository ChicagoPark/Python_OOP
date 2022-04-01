# Python_OOP
Object-Oriented Programming

## 1. Basic Class

[1] self: the scale of generated instance by BOSS class

[2] assert: Use it to suggest the condition for input parameters (Good to prevent the error at the beginning)

[3] _ _repr_ _: Represent and returns a string that describes the pointer of the object by default (if the programmer does not define it).

[4] _ _str_ _: represent the class object as a string. This method should be defined in a way that is easy to read and outputs all the members of the class. The _ _str_ _ method is called when the following functions(print() and str()) are invoked on the object and return a string. `If we have not defined` the _ _str_ _, then it will `call the _ _repr_ _ method`.

`The difference between _ _repr_ _ and _ _str_ _ is that when _ _str_ _ is defined without _ _repr_ _, CLASS._ _repr_ _() indicate the pointer of the object. Except for that situation, all the actions are the same.`

[5] _ _iter_ _: Define the behavior when the class is mentioned in iteration (e.g. for i in CLASS)
```python
def __str__ (self):
  return f"Item('{self.name}', {self.price}, {self.quantity})"

def __repr__(self):
  return f"Item('{self.name}', {self.price}, {self.quantity})"
 
def __iter__(self):
  node = self.head
  while node:
    yield node
    node = node.next
```
```bash
# print(Item.all)
# When we generate 5 objects
[Item('Phone', 100, 5), Item('Computer', 1000, 5), Item('Cable', 10, 5), Item('Mouse', 50, 5), Item('Keyboard', 75, 5)]
```


```python
  def __init__(self, name: str, price=0, quantity=0):
      # Run validations to the received arguments
      assert price >= 0, f"Price {price} is not greater than zero"
      assert quantity >= 0, f"quantity {price} is not greater than zero"
      
      self.__name = name      # by adding __ in front of variable, we can strongly prevent it to be changed .
                                # but we can edit __variable inside of the class by using function
```
print(CLASS_NAME._ _ dict _ _): Show all the attribute

## 2. Decorator
Install the Plugin named "CSV"

classmethod: send the class as first argument
staticmethod: send the value as first argument

### When to use class methods and when to use static methods?
```python
class Item:
  @staticmethod
  def is_integer(num): # staticmethod function could be same with the function outside of the class. But it looks natural to include inside of the class.
    '''
    This should do something that has a relationship
    with the class, but not something that must be unique
    per instance!
    '''
  @classmethod
  def instantiate_from_something(cls):
    '''
    This should also do something that has a relationship
    with the class, but usually, those are used to manipulate
    different structures of data to instantiate objects, like
    we have done with CSV.
    '''
```

## 3. Inheritance
```python
from item import Item

# inheritance
class Phone(Item):
    # super function is for inheritance. super().__init__() means we are going to inherit __init__ function of parent class
    def __init__(self, name: str, price=0, quantity=0, broken_phones=0):
        # Call to super function to have access to all attributes / methods
        super().__init__( # with __init__ we can call __init__ function in Item class
                          # We need to list the variable that parent class require as an input parameter
            name, price, quantity
        )
        assert broken_phones >= 0, f"quantity {broken_phones} is not greater than zero"
        # Assign to self object
        self.broken_phones = broken_phones
```



## 4. Abstract(Hide) function: add _ _ in front of function name
```python
    #1. Abstract: Variable
    @property
    # Property Decorator = Read-Only Attribute (We can set function name with variable name)
    def name(self):
        return self.__name

    # name.setter Decorator = Write-Could-Be setting
    @name.setter  # @VARIABLE_NAME.setter
    def name(self, value):
        if len(value) > 10:
            raise Exception("The name is too long!")
        self.__name = value


    #2. Abstract: Funcition
    def __connect(self, smpt_server):
        pass

    def __prepare_body(self):
        return f"""
        Hello Someone.
        Wd have {self.name} {self.quantity} times.
        Regards, JimShapedCoding
        """
    def __send(self):
        pass

    def send_email(self):
        self.__connect('')
        self.__prepare_body()
        self.__send()

```



## Exception: Advanced Python
### 1. map: apply the operation of function which has one variable to the list
```python
numbers = [x for x in range(21) if x >= 1]
squares = list(map(lambda x:x**2, numbers))
print(squares)
#[1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, 144, 169, 196, 225, 256, 289, 324, 361, 400]
```
