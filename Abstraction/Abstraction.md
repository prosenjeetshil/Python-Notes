## Abstraction

### Abstraction:

- hiding the complexity and showing essential features only
- it is achieved by abstract class
- an abstract class is a class which is inherited by ABC(abtract base class) class and it contains atleast one abstract method
- abstract method is a method which have abstractmethod decrator on it
- abstract method can be implemented for unimplimented
- ABC class and abstractmethod decorator should be imported from abc module
- we cannot create object of abstract class
- we can access properties of it by creating child of abstract class
- while creating child we must implement all abstract methods of parent
- if child fails to implement any one method then child also becomes abstract class
- abstraction is used to design API(application programming interface)


```python
#syntax

from abc import  ABC,abstractmethod

class A(ABC):
    @abstractmethod
    def m1(self):
        pass
    
class B(A):
    pass
```


```python
#  Invalid synax
from abc import  ABC,abstractmethod

class A(ABC):
    @abstractmethod
    def m1(self):
        pass
    
a = A()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Input In [1], in <cell line: 8>()
          4     @abstractmethod
          5     def m1(self):
          6         pass
    ----> 8 a = A()
    

    TypeError: Can't instantiate abstract class A with abstract method m1


Note: we cannot create object of abstract class
hence, TypeError


```python
from abc import  ABC,abstractmethod

class A():
    @abstractmethod
    def m1(self):
        pass
    
a = A()
print(a)
```

    <__main__.A object at 0x000001F7B0B076D0>
    


```python
from abc import  ABC,abstractmethod

class A(ABC):
    
    def m1(self):
        pass
    
a = A()
print(a)
```

    <__main__.A object at 0x000001F7AF803DC0>
    

Note: if we dont put ABC in brackets or we dont put abstractmethod decorator in brackets then it is not an abstract class and object are created as shown in above 2 examples.


```python
# Example of abstract class

# import abc module
from abc import ABC, abstractmethod

# create a class which inherits ABC class
class A(ABC):

    # abstract class should contain atleasts one abstract method
    # to create a abstract method a decorator is use above method

    # abstarct method can be implimented or unimplimented
    # unimplimented abstract method -- pass
    @abstractmethod
    def m1(self):
        pass

    # implimented abstract method
    @abstractmethod
    def m2(self):
        print("m2 of A")

    # instance method
    def m3(self):
        print("m3 of A")

# we cannot create object of abstarct class
# to access properties of abstract class we create a child of abstract class

class B(A): # it is a simple class which has parent abstract class

    # we must implement all abstact method of parent ,
    # else the class will be an abstact class and we cannot create object

    def m1(self):
        print("m1 of B")

    def m2(self):
        print("m2 of B")
        super().m2()
        A.m2(self)
    
b = B()

b.m1()
b.m2()
b.m3()
```

    m1 of B
    m2 of B
    m2 of A
    m2 of A
    m3 of A
    

Note: in multiple inheritance
eg: class C(B,A):

if we put abstract class in 1st parameter/arg then it given 
TypeError


```python
class C(A,B): 

    def m1(self):
        print("m1 of C")

    def m2(self):
        print("m2 of C")

c = C()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Input In [5], in <cell line: 1>()
    ----> 1 class C(A,B): 
          3     def m1(self):
          4         print("m1 of C")
    

    File C:\ProgramData\Anaconda3\lib\abc.py:106, in ABCMeta.__new__(mcls, name, bases, namespace, **kwargs)
        105 def __new__(mcls, name, bases, namespace, **kwargs):
    --> 106     cls = super().__new__(mcls, name, bases, namespace, **kwargs)
        107     _abc_init(cls)
        108     return cls
    

    TypeError: Cannot create a consistent method resolution
    order (MRO) for bases A, B



```python
# in this multiple inherited class abstract class is not in first para 
#hence no error 

class C(B,A):

    def m1(Self):
        print("m1 of C")
        super().m1()
        super().m2()
c = C()
c.m1()
```

    m1 of C
    m1 of B
    m2 of B
    m2 of A
    m2 of A
    

Practice example:


```python
from abc import ABC, abstractmethod

class Car(ABC):

    @abstractmethod
    def mileage(self):
        pass

    @abstractmethod
    def fuel_type(self):
        pass

    @abstractmethod
    def car_type(self):
        pass

class TATA(Car):

    def car_name(Self):
        print("TATA Punch")

    def mileage(self):
        print("Mileage of TATA Punch is 19Km/l")

    def fuel_type(self):
        print("Petol")

    def car_type(self):
        print("SUV")

class Maruti(Car):

    def car_name(Self):
        print("MARUTI WagonR")

    def mileage(self):
        print("Mileage of MARUTI WagonR is 24 - 34Km/l")

    def fuel_type(self):
        print("Petol")

    def car_type(self):
        print("Hatchback")

punch = TATA()
punch.car_name()
punch.mileage()
punch.fuel_type()
punch.car_type()

wagonr = Maruti()
wagonr.car_name()
wagonr.mileage()
wagonr.fuel_type()
wagonr.car_type()
```

    TATA Punch
    Mileage of TATA Punch is 19Km/l
    Petol
    SUV
    MARUTI WagonR
    Mileage of MARUTI WagonR is 24 - 34Km/l
    Petol
    Hatchback
    

### Indirect subclass

We can create indirect subclass of an abstract class by registering it through our abstract class. The need of indirect subclass is when we do not want to implement all the abstract methods of an abstract class. In indirect subclass, it is not mandatory to implement all the abstract methods of abstract class.


```python
from abc import ABC,abstractmethod

class A(ABC): #abstract class

    @abstractmethod
    def m1(self):
        print("m1 of A")

    @abstractmethod
    def m2(self):
        print("m2 of A")

    def m3(self):
        print("m3 of A")

class B(A): #direct subclass
    
    def m1(self):
        print("m1 of B")

    def m2(self):
        print("m2 of B")
        super().m2()

b = B()
b.m1()
b.m2()
```

    m1 of B
    m2 of B
    m2 of A
    


```python
class C: #indirect subclass - you cannot use properties of inheritance like
         # super func and MRO

    def m1(self):
        print("m1 of C")
        #super().m1() #AttributeError: 'super' object has no attribute 'm1'

    def m4(self):
        print("m4 of C")
        
class D(A): #direct subclass
    
    def m1(self):
        print("m1 of D")

    def m2(self):
        print("m2 of D")
        super().m2()
        
c = C()
c.m1()
c.m4()
```

    m1 of C
    m4 of C
    


```python
#check - before register
print(issubclass(B,A))
print(issubclass(C,A))
```

    True
    False
    


```python
#check - after register
#to register --- abstract_classname.register(indirect_subclass)
A.register(C)
print(issubclass(C,A))
```

    True
    


```python
#to check the subclasses of class A (abstract class)
#note - C is not is subclass of A as it is indirect subclass of class A
print("printing the subclass of A --->")
print(A.__subclasses__())
```

    printing the subclass of A --->
    [<class '__main__.B'>, <class '__main__.D'>]
    

### Creating common interface for abstract methods(Duck typing):


```python
class Connect(ABC):
    @abstractmethod
    def commit(self):
        pass
    @abstractmethod
    def rollback(self):
        pass

class Oracle(Connect):

    def commit(self):
        print("Commit of Oracle")

    def rollback(self):
        print("rollback of Oracle")

class MySQL(Connect):

    def commit(self):
        print("Commit of MySQL")

    def rollback(self):
        print("rollback of MySQL")

class SQLite(Connect):

    def commit(self):
        print("Commit of SQLite")

    def rollback(self):
        print("rollback of SQLite")


#creating a funct which class common 
def common(obj):
    obj.commit()
    obj.rollback()
    
common(Oracle())
common(MySQL())
common(SQLite())
```

    Commit of Oracle
    rollback of Oracle
    Commit of MySQL
    rollback of MySQL
    Commit of SQLite
    rollback of SQLite
    


```python
# or you can also itrate
methods = [Oracle(),MySQL(),SQLite()]

for i in methods:
    common(i)

```

    Commit of Oracle
    rollback of Oracle
    Commit of MySQL
    rollback of MySQL
    Commit of SQLite
    rollback of SQLite
    

Practice example for common interface in abs methods:


```python
from abc import ABC,abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    l = 10
    h = 7

    def area(self):
        res = self.l*self.h
        print("Area of Rectangle is : ",res,"cm")

class Triangle(Shape):
    l = 4
    w = 6

    def area(self):
        res = 0.5 * self.w * self.l
        print("Area of Triangle is : ",res,"cm")

class Square(Shape):
    l = 5

    def area(self):
        res = (self.l**2)
        print("Area of Square is : ",res,"cm")

class Circle(Shape):
    r = 4

    def area(self):
        res = 3.14*(self.r**2)
        print("Area of Circle is : ",res,"cm")


def common(obj):
    obj.area()

methods = [Rectangle(),Triangle(),Square(),Circle()]
for i in methods:
    common(i)
```

    Area of Rectangle is :  70 cm
    Area of Triangle is :  12.0 cm
    Area of Square is :  25 cm
    Area of Circle is :  50.24 cm
    
