# Object-oriented programming
There are three widely used programming paradigms: procedural programming, functional programming and object-oriented programming. C# supports both procedural and object-oriented programming.

## OOP definition
Object-oriented programming (OOP) is a programming paradigm that uses objects and their interactions to design applications and computer programs.

There are some basic programming concepts in OOP:
- Abstraction
- Polymorphism
- Encapsulation
- Inheritance

The abstraction is simplifying complex reality by modeling classes appropriate to the problem. The polymorphism is the process of using an operator or function in different ways for different data input. The encapsulation hides the implementation details of a class from other objects. The inheritance is a way to form new classes using classes that have already been defined.
### Objects
Objects are basic building blocks of a C# OOP program. An object is a combination of data and methods. The data and the methods are called members of an object. In an OOP program, we create objects. These objects communicate together through methods. Each object can receive messages, send messages and process data.

There are two steps in creating an object. First, we define a class. A class is a template for an object. It is a blueprint which describes the state and behavior that the objects of the class all share. A class can be used to create many objects. Objects created at runtime from a class are called instances of that particular class.

#### Program.cs
```cs
using System;

namespace Being
{
    class Being {}

    class Program
    {
        static void Main(string[] args)
        {
            var b = new Being();
            Console.WriteLine(b);
        }
    }
}
```
In our first example, we create a simple object.
```cs
class Being {}
```
This is a simple class definition. The body of the template is empty. It does not have any data or methods.
```cs
var b = new Being();
```
We create a new instance of the Being class. For this we have the new keyword. The b variable is the handle to the created object.
```cs
Console.WriteLine(b);
```
We print the object to the console to get some basic description of the object. What does it mean, to print an object? When we print an object, we in fact call its ToString() method. But we have not defined any method yet. It is because every object created inherits from the base object. It has some elementary functionality which is shared among all objects created. One of this is the ToString() method.

```cs
Being.Being
We get the object class name.
```
### Object attributes
Object attributes is the data bundled in an instance of a class. The object attributes are called instance variables or member fields. An instance variable is a variable defined in a class, for which each object in the class has a separate copy.

#### Program.cs
```cs
using System;

namespace ObjectAttributes
{
    class Person
    {
        public string name;
    }

    class Program
    {
        static void Main(string[] args)
        {
            var p1 = new Person();
            p1.name = "Jane";

            var p2 = new Person();
            p2.name = "Beky";

            Console.WriteLine(p1.name);
            Console.WriteLine(p2.name);
        }
    }
}
```
In the above C# code, we have a Person class with one member field.
```cs
class Person
{
    public string name;
}
```
We declare a name member field. The public keyword specifies that the member field will be accessible outside the class block.
```cs
var p1 = new Person();
p1.name = "Jane";
```
We create an instance of the Person class and set the name variable to "Jane". We use the dot operator to access the attributes of objects.
```cs
var p2 = new Person();
p2.name = "Beky";
```
We create another instance of the Person class. Here we set the variable to "Beky".
```cs
Console.WriteLine(p1.name);
Console.WriteLine(p2.name);
```
We print the contents of the variables to the console.

```cs
Jane
Beky
We see the output of the program. Each instance of the Person class has a separate copy of the name member field.
```
### Methods
Methods are functions defined inside the body of a class. They are used to perform operations with the attributes of our objects. Methods bring modularity to our programs.

Methods are essential in the encapsulation concept of the OOP paradigm. For example, we might have a Connect() method in our AccessDatabase class. We need not to be informed how exactly the method Connect() connects to the database. We only have to know that it is used to connect to a database. This is essential in dividing responsibilities in programming, especially in large applications.

Objects group state and behavior, methods represent the behavioral part of the objects.

#### Program.cs
```cs
using System;

namespace Methods
{
    class Circle
    {
        private int radius;

        public void SetRadius(int radius)
        {
            this.radius = radius;
        }

        public double Area()
        {
            return this.radius * this.radius * Math.PI;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var c = new Circle();
            c.SetRadius(5);

            Console.WriteLine(c.Area());
        }
    }
}
```cs
In the code example, we have a Circle class. We define two methods.
```cs
private int radius;
```
We have one member field. It is the radius of the circle. The private keyword is an access specifier. It tells that the variable is restricted to the outside world. If we want to modify this variable from the outside, we must use the publicly available SetRadius() method. This way we protect our data.
```cs
public void SetRadius(int radius)
{
    this.radius = radius;
}
```
This is the SetRadius() method. The this variable is a special variable which we use to access the member fields from methods. The this.radius is an instance variable, while the radius is a local variable, valid only inside the SetRadius() method.
```cs
var c = new Circle();
c.SetRadius(5);
```
We create an instance of the Circle class and set its radius by calling the SetRadius() method on the object of the circle. We use the dot operator to call the method.
```cs
public double Area()
{
    return this.radius * this.radius * Math.PI;
}
```
The Area() method returns the area of a circle. The Math.PI is a built-in constant.

```cs
78.5398163397448
Running the example gives this outcome.
```
### Access modifiers
Access modifiers set the visibility of methods and member fields. C# has four basic access modifiers: public, protected, private and internal. The public members can be accessed from anywhere. The protected members can be accessed only within the class itself and by inherited and parent classes. The private members are limited to the containing type, e.g. only within its class or interface. The internal members may be accessed from within the same assembly (exe or DLL).

There are also two combinations of modifiers: protected internal and private protected. The protected internal type or member can be accessed by any code in the assembly in which it is declared, or from within a derived class in another assembly. The private protected type or member can be accessed only within its declaring assembly, by code in the same class or in a type that is derived from that class.

Access modifiers protect data against accidental modifications. They make the programs more robust.



First Header  |  Class  | Current assembly | Derived types | Derived types in current assembly | Entire program
------------- | -------------| -------------| -------------| -------------| -------------
public|	+|	+|	+|	+|	+
protected|	+|	o|	+|	+|	o
internal|	+|	+|	o|	o|	o
private|	+|	o|	o|	o|	o
protected internal|	+|	+|	+|	+|	o
private protected|	+|	o|	o|	+|	o

The above table summarizes C# access modifiers (+ is accessible, o is not accessible).

#### Program.cs
```cs
using System;

namespace AccessModifiers
{
    class Person
    {
        public string name;
        private int age;

        public int GetAge()
        {
            return this.age;
        }

        public void SetAge(int age)
        {
            this.age = age;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var p = new Person();
            p.name = "Jane";

            p.SetAge(17);

            Console.WriteLine("{0} is {1} years old",
                p.name, p.GetAge());
            }
    }
}
```
In the above program, we have two member fields. One is declared public, the other private.
```cs
public int GetAge()
{
    return this.age;
}
```
If a member field is private, the only way to access it is via methods. If we want to modify an attribute outside the class, the method must be declared public. This is an important aspect of data protection.
```cs
public void SetAge(int age)
{
    this.age = age;
}
```
The SetAge() method enables us to change the private age variable from outside of the class definition.
```cs
var p = new Person();
p.name = "Jane";
```
We create a new instance of the Person class. Because the name attribute is public, we can access it directly. However, this is not recommended.
```cs
p.SetAge(17);
```
The SetAge() method modifies the age member field. It cannot be accessed or modified directly because it is declared private.
```cs
Console.WriteLine("{0} is {1} years old",
    p.name, p.GetAge());
```
Finally, we access both members to build a string.
```cs
$ dotnet run
Jane is 17 years old
Running the example gives this output.
```
Member fields with private access modifiers are not inherited by derived classes.

#### Program.cs
```cs
using System;

namespace Protected
{
    class Base
    {
        public string name = "Base";
        protected int id = 5323;
        private bool isDefined = true;
    }

    class Derived : Base
    {
        public void info()
        {
            Console.WriteLine("This is Derived class");
            Console.WriteLine("Members inherited");
            Console.WriteLine(this.name);
            Console.WriteLine(this.id);
            // Console.WriteLine(this.isDefined);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var derived = new Derived();
            derived.info();
        }
    }
}
```
In the preceding program, we have a Derived class which inherits from the Base class. The Base class has three member fields. All with different access modifiers. The isDefined member is not inherited. The private modifier prevents this.
```cs
class Derived : Base
```
The class Derived inherits from the Base class. To inherit from another class, we use the colon (:) operator.
```cs
Console.WriteLine(this.name);
Console.WriteLine(this.id);
// Console.WriteLine(this.isDefined);
```
The public and the protected members are inherited by the Derived class. They can be accessed. The private member is not inherited. The line accessing the member field is commented. If we uncommented the line, the code would not compile.

```cs
Program.cs(9,22): warning CS0414: The field 'Base.isDefined' is assigned but its value
is never used [C:\Users\Jano\Documents\csharp\tutorial\oop\Protected\Protected.csproj]
This is Derived class
Members inherited
Base
5323
Running the program, we receive this output.
```
### Constructor
A constructor is a special kind of a method. It is automatically called when the object is created. Constructors do not return values. The purpose of the constructor is to initiate the state of an object. Constructors have the same name as the class. The constructors are methods, so they can be overloaded too.

Constructors cannot be inherited. They are called in the order of inheritance. If we do not write any constructor for a class, C# provides an implicit default constructor. If we provide any kind of a constructor, then a default is not supplied.

#### Program.cs
```cs
using System;

namespace Constructor
{
    class Being
    {
        public Being()
        {
            Console.WriteLine("Being is created");
        }

        public Being(string being)
        {
            Console.WriteLine("Being {0} is created", being);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            new Being();
            new Being("Tom");
        }
    }
}
```
We have a Being class. This class has two constructors. The first one does not take parameters; the second one takes one parameter.
```cs
public Being(string being)
{
    Console.WriteLine("Being {0} is created", being);
}
```
This constructor takes one string parameter.
```cs
new Being();
```
An instance of the Being class is created. This time the constructor without a parameter is called upon object creation.
```cs
$ dotnet run
Being is created
Being Tom is created
This is the output of the program.
```
In the next example, we initiate data members of the class. Initiation of variables is a typical job for constructors.

#### Program.cs
```cs
using System;

namespace Constructor2
{
    class MyFriend
    {
        private DateTime born;
        private string name;

        public MyFriend(string name, DateTime born)
        {
            this.name = name;
            this.born = born;
        }

        public void Info()
        {
            Console.WriteLine("{0} was born on {1}",
                this.name, this.born.ToShortDateString());
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var name = "Lenka";
            var born = new DateTime(1990, 3, 5);

            var friend = new MyFriend(name, born);
            friend.Info();
        }
    }
}
```
We have a MyFriend class with data members and methods.
```cs
private DateTime born;
private string name;
```
We have two private variables in the class definition.
```cs
public MyFriend(string name, DateTime born)
{
    this.name = name;
    this.born = born;
}
```
In the constructor, we initiate the two data members. The this variable is a handler used to reference the object variables.

var friend = new MyFriend(name, born);
friend.Info();
We create a MyFriend object with two arguments. Then we call the Info() method of the object.

```cs
Lenka was born on 3/5/1990
This is the output.
```

### Constructor chaining
Constructor chaining is the ability of a class to call another constructor from a constructor. To call another constructor from the same class, we use the this keyword.

#### Program.cs
```cs
using System;

namespace ConstructorChaining
{
    class Circle
    {
        public Circle(int radius)
        {
            Console.WriteLine("Circle, r={0} is created", radius);
        }

        public Circle() : this(1)
        {

        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            new Circle(5);
            new Circle();
        }
    }
}
```
We have a Circle class. The class has two constructors. One that takes one parameter and one that does not take any parameters.
```cs
public Circle(int radius)
{
    Console.WriteLine("Circle, r={0} is created", radius);
}
```
This constructor takes one parameter — the radius.
```cs
public Circle() : this(1)
{

}
```
This is the constructor without a parameter. It simply calls the other constructor and gives it a default radius of 1.

```cs
Circle, r=5 is created
Circle, r=1 is created
This is the output.
```

### ToString method
Each object has a ToString() method. It returns a human-readable representation of an object. The default implementation returns the fully qualified name of the type of the Object. Note that when we call the Console.WriteLine() method with an object as a parameter, the ToString() is being called.

Program.cs
```cs
using System;

namespace ToStringMethod
{
    class Being
    {
        public override string ToString()
        {
            return "This is Being class";
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var b = new Being();
            var o = new Object();

            Console.WriteLine(o.ToString());
            Console.WriteLine(b.ToString());
            Console.WriteLine(b);
        }
    }
}
```
We have a Being class in which we override the default implementation of the ToString() method.
```cs
public override string ToString()
{
    return "This is Being class";
}
```
Each class created inherits from the base object. The ToString() method belongs to this object class. We use the override keyword to inform that we are overriding a method.
```cs
var b = new Being();
var o = new Object();
```
We create one custom defined object and one built-in object.
```cs
Console.WriteLine(o.ToString());
Console.WriteLine(b.ToString());
```
We call the ToString() method on these two objects.
```cs
Console.WriteLine(b);
```
As we have specified earlier, placing an object as a parameter to the Console.WriteLine() will call its ToString() method. This time, we have called the method implicitly.

```cs
System.Object
This is Being class
This is Being class
This is what we get when we run the example.
```
### Object initializers
Object initializers let us assign values to any accessible fields or properties of an object at creation time without having to invoke a constructor. The properties or fields are assigned inside the {} brackets. Also, we can specify arguments for a constructor or omit the arguments.

#### Program.cs
```cs
using System;

namespace ObjectInitializers
{
    class User
    {
        public User() {}

        public string Name { set; get; }
        public string Occupation { set; get; }

        public override string ToString()
        {
            return $"{Name} is a {Occupation}";
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var u = new User { Name = "John Doe", Occupation = "gardener" };
            Console.WriteLine(u);
        }
    }
}
```
In the example, we create a new user with the object initializer syntax.
```cs
public User() {}
```
We define an empty constructor.
```cs
public string Name { set; get; }
public string Occupation { set; get; }
```
We have two properties: Name and Occupation.

var u = new User { Name = "John Doe", Occupation = "gardener" };
We assign the values to the properties in the {} brackets.

```cs
John Doe is a gardener
This is the output.
```

C# class constants
C# enables to create class constants. These constants do not belong to a concrete object. They belong to the class. By convention, constants are written in uppercase letters.

### Program.cs
```cs
using System;

namespace ClassConstants
{
    class Math
    {
        public const double PI = 3.14159265359;
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(Math.PI);
        }
    }
}
```
We have a Math class with a PI constant.

```cs
public const double PI = 3.14159265359;
```
The const keyword is used to define a constant. The public keyword makes it accessible outside the body of the class.

```cs
3.14159265359
Running the example we see this output.
```
### Inheritance
The inheritance is a way to form new classes using classes that have already been defined. The newly formed classes are called derived classes, the classes that we derive from are called base classes. Important benefits of inheritance are code reuse and reduction of complexity of a program. The derived classes (descendants) override or extend the functionality of the base classes (ancestors).

#### Program.cs
```cs
using System;

namespace Inheritance
{
    class Being
    {
        public Being()
        {
            Console.WriteLine("Being is created");
        }
    }

    class Human : Being
    {
        public Human()
        {
            Console.WriteLine("Human is created");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            new Human();
        }
    }
}
```
In this program, we have two classes. A base Being class and a derived Human class. The derived class inherits from the base class.
```cs
class Human : Being
```
In C#, we use the colon (:) operator to create inheritance relations.
```cs
new Human();
```
We instantiate the derived Human class.

```cs
Being is created
Human is created
```
We can see that both constructors were called. First, the constructor of the base class is called, then the constructor of the derived class.

A more complex example follows.

#### Program.cs
```cs
using System;

namespace Inheritance2
{
    class Being
    {
        static int count = 0;

        public Being()
        {
            count++;
            Console.WriteLine("Being is created");
        }

        public void GetCount()
        {
            Console.WriteLine("There are {0} Beings", count);
        }
    }

    class Human : Being
    {
        public Human()
        {
            Console.WriteLine("Human is created");
        }
    }

    class Animal : Being
    {
        public Animal()
        {
            Console.WriteLine("Animal is created");
        }
    }

    class Dog : Animal
    {
        public Dog()
        {
            Console.WriteLine("Dog is created");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            new Human();

            var dog = new Dog();
            dog.GetCount();
        }
    }
}
```
We have four classes. The inheritance hierarchy is more complicated. The Human and the Animal classes inherit from the Being class. The Dog class inherits directly from the Animal class and indirectly from the Being class. We also introduce a concept of a static variable.

static int count = 0;
We define a static variable. Static members are members that are shared by all instances of a class.
```cs
Being()
{
    count++;
    Console.WriteLine("Being is created");
}
```
Each time the Being class is instantiated, we increase the count variable by one. This way we keep track of the number of instances created.
```cs
class Animal : Being
...

class Dog : Animal
...
```
The Animal inherits from the Being and the Dog inherits from the Animal. Indirectly, the Dog inherits from the Being as well.
```cs
new Human();
var dog = new Dog();
dog.GetCount();
```
We create instances from the Human and from the Dog classes. We call the GetCount() method of the Dog object.

```cs
Being is created
Human is created
Being is created
Animal is created
Dog is created
There are 2 Beings
```
The Human calls two constructors. The Dog calls three constructors. There are two Beings instantiated.

We use the base keyword to call the parent's constructor explicitly.

#### Program.cs
```cs
using System;

namespace Shapes
{
    class Shape
    {
        protected int x;
        protected int y;

        public Shape()
        {
            Console.WriteLine("Shape is created");
        }

        public Shape(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    class Circle : Shape
    {
        private int r;

        public Circle(int r, int x, int y) : base(x, y)
        {
            this.r = r;
        }

        public override string ToString()
        {
            return String.Format("Circle, r:{0}, x:{1}, y:{2}", r, x, y);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var c = new Circle(2, 5, 6);
            Console.WriteLine(c);
        }
    }
}
```
We have two classes: the Shape class and the Circle class. The Shape class is a base class for geometrical shapes. We can put into this class some commonalities of the common shapes, like the x and y coordinates.
```cs
public Shape()
{
    Console.WriteLine("Shape is created");
}

public Shape(int x, int y)
{
    this.x = x;
    this.y = y;
}
```
The Shape class has two constructors. The first one is the default constructor. The second one takes two parameters: the x, y coordinates.
```cs
public Circle(int r, int x, int y) : base(x, y)
{
    this.r = r;
}
```
This is the constructor for the Circle class. This constructor initiates the r member and calls the parent's second constructor, to which it passes the x, y coordinates. Have we not called the constructor explicitly with the base keyword, the default constructor of the Shape class would be called.

```cs
Circle, r:2, x:5, y:6
This is the output of the example.
```

### Abstract classes and methods
Abstract classes cannot be instantiated. If a class contains at least one abstract method, it must be declared abstract too. Abstract methods cannot be implemented; they merely declare the methods' signatures. When we inherit from an abstract class, all abstract methods must be implemented by the derived class. Furthermore, these methods must be declared with the same of less restricted visibility.

Unlike Interfaces, abstract classes may have methods with full implementation and may also have defined member fields. So abstract classes may provide a partial implementation. Programmers often put some common functionality into abstract classes. And these abstract classes are later subclassed to provide more specific implementation. For example, the Qt graphics library has a QAbstractButton, which is the abstract base class of button widgets, providing functionality common to buttons. Buttons Q3Button, QCheckBox, QPushButton, QRadioButton, and QToolButton inherit from this base abstract class.

Formally put, abstract classes are used to enforce a protocol. A protocol is a set of operations which all implementing objects must support.

#### Program.cs
```cs
using System;

namespace AbstractClass
{
    abstract class Drawing
    {
        protected int x = 0;
        protected int y = 0;

        public abstract double Area();

        public string GetCoordinates()
        {
            return string.Format("x: {0}, y: {1}", this.x, this.y);
        }
    }

    class Circle : Drawing
    {
        private int r;

        public Circle(int x, int y, int r)
        {
            this.x = x;
            this.y = y;
            this.r = r;
        }

        public override double Area()
        {
            return this.r * this.r * Math.PI;
        }

        public override string ToString()
        {
            return string.Format("Circle at x: {0}, y: {1}, radius: {2}",
                this.x, this.y, this.r);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var c = new Circle(12, 45, 22);

            Console.WriteLine(c);
            Console.WriteLine("Area of circle: {0}", c.Area());
            Console.WriteLine(c.GetCoordinates());
        }
    }
}
```
We have an abstract base Drawing class. The class defines two member fields, defines one method and declares one method. One of the methods is abstract, the other one is fully implemented. The Drawing class is abstract because we cannot draw it. We can draw a circle, a dot or a square. The Drawing class has some common functionality to the objects that we can draw.

abstract class Drawing
We use the abstract keyword to define an abstract class.
```cs
public abstract double Area();
```
An abstract method is also preceded with the abstract keyword.
```cs
class Circle : Drawing
```
A Circle is a subclass of the Drawing class. It must implement the abstract Area() method.
```cs
public override double Area()
{
    return this.r * this.r * Math.PI;
}
```
When we implement the Area() method, we must use the override keyword. This way we inform the compiler that we override an existing (inherited) method.

```cs
Circle at x: 12, y: 45, radius: 22
Area of circle: 1520.53084433746
x: 12, y: 45
This is the output of the program.
```
### Partial class
With the partial keyword, it is possible to split the definition of a class into several parts inside the same namespace. The class can also be defined in multiple files.

Partial classes are used when working with very large code base, which can be split into smaller units. Partial classes are also used with automatic code generators.

#### Program.cs
```cs
using System;

namespace PartialClass
{
    partial class Worker
    {
        public string DoWork()
        {
            return "Doing work";
        }
    }

    partial class Worker
    {
        public string DoPause()
        {
            return "Pausing";
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var worker = new Worker();

            Console.WriteLine(worker.DoWork());
            Console.WriteLine(worker.DoWork());
            Console.WriteLine(worker.DoPause());
        }
    }
}
```
In the example, we have the Worker class defined in two parts. The parts are joined together by the compiler to form a final class.

```cs
Doing work
Doing work
Pausing
This is the ouput.
```

##Methods

In object oriented programming, we work with objects. Objects are the basic building blocks of a program. Objects consists of data and methods. Methods change the state of the objects created. They are the dynamic part of the objects; data is the static part.


### Method definition
A method is a code block containing a series of statements. Methods must be declared within a class or a structure. It is a good programming practice that methods do only one specific task. Methods bring modularity to programs. Proper use of methods bring the following advantages:
- Reducing duplication of code
- Decomposing complex problems into simpler pieces
- Improving clarity of the code
- Reuse of code
- Information hiding

### Method characteristics
Basic characteristics of methods are:
- Access level
- Return value type
- Method name
- Method parameters
- Parentheses
- Block of statements

Access level of methods is controlled with access modifiers. They set the visibility of methods. They determine who can call the method. Methods may return a value to the -caller. In case our method returns a value, we provide its data type. If not, we use the void keyword to indicate that our method does not return values. Method parameters are surrounded by parentheses and separated by commas. Empty parentheses indicate that the method requires no parameters. The method block is surrounded with { } characters. The block contains one or more statements that are executed, when the method is invoked. It is legal to have an empty method block.

### Method signature
A method signature is a unique identification of a method for the C# compiler. The signature consists of a method name and the type and kind (value, reference, or output) of each of its formal parameters. Method signature does not include the return type.

Any legal character can be used in the name of a method. By convention, method names begin with an uppercase letter. The method names are verbs or verbs followed by adjectives or nouns. Each subsequent word starts with an uppercase character. The following are typical names of methods in C#:

- Execute
- FindId
- SetName
- GetName
- CheckIfValid
- TestValidity

### C# simple example
We start with a simple example.

#### Program.cs
```cs
using System;

namespace SimpleMethod
{
    class Base
    {
        public void ShowInfo()
        {
            Console.WriteLine("This is Base class");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Base bs = new Base();
            bs.ShowInfo();
        }
    }
}
```
We have a ShowInfo() method that prints the name of its class.
```cs
class Base
{
    public void ShowInfo()
    {
        Console.WriteLine("This is Base class");
    }
}
```
Each method must be defined inside a class or a structure. It must have a name. In our case the name is ShowInfo(). The keywords that precede the name of the method are access specifier and the return type. Parentheses follow the name of the method. They may contain parameters of the method. Our method does not take any parameters.
```cs
static void Main()
{
   ...
}
```
This is the Main() method. It is the entry point to each console or GUI application. It must be declared static. We will see later why. The return type for a Main() method may be void or int. The access specifier for the Main() method is omitted. In such a case a default one is used, which is private. It is not recommended to use public access specifier for the Main() method. It is not supposed to be called by any other methods in the assemblies. It is only the CLR that should be able to call it when the application starts.
```cs
Base bs = new Base();
bs.ShowInfo();
```
We create an instance of the Base class. We call the ShowInfo() method upon the object. We say that the method is an instance method, because it needs an instance to be called. The method is called by specifying the object instance, followed by the member access operator — the dot, followed by the method name.

### Method parameters
A parameter is a value passed to the method. Methods can take one or more parameters. If methods work with data, we must pass the data to the methods. We do it by specifying them inside the parentheses. In the method definition, we must provide a name and type for each parameter.

#### Program.cs
```cs
using System;

namespace MethodParameters
{
    class Addition
    {
        public int AddTwoValues(int x, int y)
        {
            return x + y;
        }

        public int AddThreeValues(int x, int y, int z)
        {
            return x + y + z;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Addition a = new Addition();
            int x = a.AddTwoValues(12, 13);
            int y = a.AddThreeValues(12, 13, 14);

            Console.WriteLine(x);
            Console.WriteLine(y);
        }
    }
}
```
In the above example, we have two methods. One of them takes two parameters, the other one takes three parameters.
```cs
public int AddTwoValues(int x, int y)
{
    return x + y;
}
```
The AddTwoValues() method takes two parameters. These parameters have int type. The method also returns an integer to the caller. We use the return keyword to return a value from the method.
```cs
public int AddThreeValues(int x, int y, int z)
{
    return x + y + z;
}
```
The AddThreeValues() is similar to the previous method. It takes three parameters.
```cs
int x = a.AddTwoValues(12, 13);
```
We call the AddTwoValues() method of the addition object. It takes two values. These values are passed to the method. The method returns a value which is assigned to the x variable.

### Variable number of arguments
A method can take variable number of arguments. For this we use the params keyword. No additional parameters are permitted after the params keyword. Only one params keyword is permitted in a method declaration.

#### Program.cs
```cs
using System;

namespace SumOfValues
{
    class Program
    {
        static void Main(string[] args)
        {
            Sum(1, 2, 3);
            Sum(1, 2, 3, 4, 5);
        }

        static void Sum(params int[] list)
        {
            Console.WriteLine("There are {0} items", list.Length);
        
            int sum = 0;

            foreach (int i in list) 
            {
                sum = sum + i;
            }
            
            Console.WriteLine("Their sum is {0}", sum);
        }
    }
}
```
We create a Sum() method which can take variable number of arguments. The method will calculate the sum of values passed to the method.
```cs
Sum(1, 2, 3);
Sum(1, 2, 3, 4, 5);
```
We call the Sum() method twice. In one case, it takes 3 arguments, in the second case 5. We call the same method.
```cs
static void Sum(params int[] list)
{
...
}
```
The Sum() method can take variable number of integer values. All values are added to the list array.

Console.WriteLine("There are {0} items", list.Length);
We print the length of the list array.
```cs
int sum = 0;
foreach (int i in list) 
{
    sum = sum + i;
}
```
We compute the sum of the values in the list.
```cs
$ dotnet run
There are 3 items
Their sum is 6
There are 5 items
Their sum is 15
This is the output of the example.
```
### Returning tuples
C# methods can return multiple values by using tuples.

#### Program.cs
```cs
using System;
using System.Collections.Generic;
using System.Linq;

namespace ReturingTuples
{
    class Program
    {
        static void Main(string[] args)
        {
            var vals = new List<int> { 11, 21, 3, -4, -15, 16, 5 };

            (int min, int max, int sum) = BasicStats(vals);

            Console.WriteLine($"Minimum: {min}, Maximum: {max}, Sum: {sum}");
        }

        static (int, int, int) BasicStats(List<int> vals)
        {
            int sum = vals.Sum();
            int min = vals.Min();
            int max = vals.Max();

            return (min, max, sum);
        }
    }
}
```
We have the BasicStats() method, which returns the basic statistics of a list of integers.

using System.Linq;
We need to import the System.Linq for the Sum(), Min(), and Max() extension methods.

var vals = new List<int> { 11, 21, 3, -4, -15, 16, 5 };
We have a list of integer values. We want to compute some basic statistics from these values.

(int min, int max, int sum) = BasicStats(vals);
We use a deconstruction operation to assign the tuple elements into three variables.
```cs
static (int, int, int) BasicStats(List<int> vals)
{
```
The method declaration specifies that we return a tuple.

return (min, max, sum); 
We return a tuple of three elements.

```cs
Minimum: -15, Maximum: 21, Sum: 37
This is the output.
```
C# anonymous methods
Anonymous methods are inline methods that do not have a name. Anonymous methods reduce the coding overhead by eliminating the need to create a separate method. Without anonymous methods developers often had to create a class just to call one method.

#### Program.cs
```cs
using System;
using System.Timers;

namespace AnonymousMethod
{
    class Program
    {
        static void Main(string[] args)
        {
            var timer = new Timer();

            timer.Elapsed += new ElapsedEventHandler(
                delegate(object source, ElapsedEventArgs e)
                {
                    Console.WriteLine("Event triggered at {0}", e.SignalTime);
                }
            );

            timer.Interval = 2000;
            timer.Enabled = true;

            Console.ReadLine();
        }
    }
}
```
We create a timer object and every 2 seconds we call an anonymous method.
```cs
var timer = new Timer();
A Timer class generates recurring events in an application.

timer.Elapsed += new ElapsedEventHandler(
    delegate(object source, ElapsedEventArgs e)
    {
        Console.WriteLine("Event triggered at {0}", e.SignalTime);
    }
);
```
Here we plug the anonymous method to the Elapsed event. The delegate keyword is used to denote an anonymous method.
```cs
Console.ReadLine();
```
At this moment, the program waits for an input from the user. The program ends when we hit the Return key. Otherwise, the program would finish immediately before the events could be generated.

#### Passing arguments by value, by reference
C# supports two ways of passing arguments to methods: by value and by reference. The default passing of arguments is by value. When we pass arguments by value, the method works only with the copies of the values. This may lead to performance overheads when we work with large amounts of data.

We use the ref keyword to pass a value by reference. When we pass values by reference, the method receives a reference to the actual values. The original values are affected when modified. This way of passing values is more time and space efficient. On the other hand, it is more error prone.

Which way of passing arguments should we use? It depends on the situation. Say we have a set of data, for example salaries of employees. If we want to compute some statistics of the data, we do not need to modify them. We can pass by values. If we work with large amounts of data and the speed of computation is critical, we pass by reference. If we want to modify the data, e.g. do some reductions or raises to the salaries, we might pass by reference.

The following example shows how we pass arguments by values.

#### Program.cs
```cs
using System;

namespace PassingByValues
{
    class Program
    {
        static int a = 4;
        static int b = 7;

        static void Main(string[] args)
        {
            Console.WriteLine("Outside Swap method");
            Console.WriteLine("a is {0}", a);
            Console.WriteLine("b is {0}", b);

            Swap(a, b);

            Console.WriteLine("Outside Swap method");
            Console.WriteLine("a is {0}", a);
            Console.WriteLine("b is {0}", b);
        }

        static void Swap(int a, int b)
        {
            int temp = a;
            a = b;
            b = temp;

            Console.WriteLine("Inside Swap method");
            Console.WriteLine("a is {0}", a);
            Console.WriteLine("b is {0}", b);
        }        
    }
}
```
The Swap() method swaps the numbers between the a and b variables. The original variables are not affected.
```cs
static int a = 4;
static int b = 7;
```
At the beginning, these two variables are initiated. The variables must be declared static, because they are used from static methods.

Swap(a, b);
We call the Swap() method. The method takes a and b variables as arguments.
```cs
int temp = a;
a = b;
b = temp;
```
Inside the Swap() method, we change the values. Note that the a and b variables are defined locally. They are valid only inside the Swap() method.
```cs
Outside Swap method
a is 4
b is 7
Inside Swap method
a is 7
b is 4
Outside Swap method
a is 4
b is 7
The output shows that the original variables were not affected.
```
The next code example passes values to the method by reference. The original variables are changed inside the Swap() method. Both the method definition and the method call must use the ref keyword.

#### Program.cs
```cs
using System;

namespace PassingByReference
{
    class Program
    {
        static int a = 4;
        static int b = 7;

        static void Main(string[] args)
        {
            Console.WriteLine("Outside Swap method");
            Console.WriteLine("a is {0}", a);
            Console.WriteLine("b is {0}", b);

            Swap(ref a, ref b);

            Console.WriteLine("Outside Swap method");
            Console.WriteLine("a is {0}", a);
            Console.WriteLine("b is {0}", b);
        }

        static void Swap(ref int a, ref int b)
        {
            int temp = a;
            a = b;
            b = temp;
            
            Console.WriteLine("Inside Swap method");
            Console.WriteLine("a is {0}", a);
            Console.WriteLine("b is {0}", b);
        }
    }
}
```
In this example, calling the Swap() method will change the original values.

Swap(ref a, ref b);
We call the method with two arguments. They are preceded by the ref keyword to indicate that we are passing arguments by reference.
```cs
static void Swap(ref int a, ref int b)
{
...
}
```
Also in the method declaration, we use the ref keyword to inform the compiler that we accept references to the parameters and not the values.

```cs
Outside Swap method
a is 4
b is 7
Inside Swap method
a is 7
b is 4
Outside Swap method
a is 7
b is 4
Here we see that the Swap() method really changed the values of the variables.
```
The out keyword is similar to the ref keyword. The difference is that when using the ref keyword, the variable must be initialized before it is being passed. With the out keyword, it may not be initialized. Both the method definition and the method call must use the out keyword.

#### Program.cs
```cs
using System;

namespace OutKeyword
{
    class Program
    {
        static void Main(string[] args)
        {
            int val;
            SetValue(out val);

            Console.WriteLine(val);
        }

        static void SetValue(out int i)
        {
            i = 12;
        }        
    }
}
```
An example shows the usage of the out keyword.
```cs
int val;
SetValue(out val);
The val variable is declared, but not initialized. We pass the variable to the SetValue() method.
```
```cs
static void SetValue(out int i)
{
    i = 12;
}
```
Inside the SetValue() method it is assigned a value which is later printed to the console.

### Method overloading
Method overloading allows the creation of several methods with the same name which differ from each other in the type of the input.

What is method overloading good for? The Qt5 library gives a nice example for the usage. The QPainter class has three methods to draw a rectangle. Their name is drawRect() and their parameters differ. One takes a reference to a floating point rectangle object, another takes a reference to an integer rectangle object, and the last one takes four parameters: x, y, width, height. If the C++ language, which is the language in which Qt is developed, didn't have method overloading, the creators of the library would have to name the methods like drawRectRectF(), drawRectRect(), drawRectXYWH(). The solution with method overloading is more elegant.

#### Program.cs
```cs
using System;

namespace Overloading
{
    class Sum
    {
        public int GetSum()
        {
            return 0;
        }

        public int GetSum(int x)
        {
            return x;
        }

        public int GetSum(int x, int y)
        {
            return x + y;
        }
    }

    class Program
    {
        static void Main()
        {
            var s = new Sum();

            Console.WriteLine(s.GetSum());
            Console.WriteLine(s.GetSum(20));
            Console.WriteLine(s.GetSum(20, 30));
        }
    }
}
```
We have three methods called GetSum(). They differ in input parameters.
```cs
public int GetSum(int x)
{
    return x;
}
```
This one takes one parameter.
```cs
Console.WriteLine(s.GetSum());
Console.WriteLine(s.GetSum(20));
Console.WriteLine(s.GetSum(20, 30));
We call all three methods.
```
```cs
0
20
50
And this is what we get when we run the example.
```
### Recursion
Recursion, in mathematics and computer science, is a way of defining methods in which the method being defined is applied within its own definition. In other words, a recursive method calls itself to do its job. Recursion is a widely used approach to solve many programming tasks.

A typical example is the calculation of a factorial.

#### Program.cs
```cs
using System;

namespace Recursion
{
    class Program
    {
        static void Main(string[] args)
        {        
            Console.WriteLine(Factorial(6));
            Console.WriteLine(Factorial(10));
        }

        static int Factorial(int n)
        {
            if (n == 0)
            {
                return 1;
            } else
            {
                return n * Factorial(n-1);
            }
        }
    }
}
```
In this code example, we calculate the factorial of two numbers.
```cs
return n * Factorial(n-1);
```
Inside the body of the factorial method, we call the factorial method with a modified argument. The function calls itself.

```cs
720
3628800
These are the results.
```
### Method scope
A variable declared inside a method has a method scope. The scope of a name is the region of program text within which it is possible to refer to the entity declared by the name without the qualification of the name. A variable which is declared inside a method has a method scope. It is also called a local scope. The variable is valid only in this particular method.

#### Program.cs
```cs
using System;

namespace MethodScope
{
    class Test
    {
        int x = 1;

        public void exec1()
        {
            Console.WriteLine(this.x);
            Console.WriteLine(x);
        }

        public void exec2()
        {
            int z = 5;

            Console.WriteLine(x);
            Console.WriteLine(z);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var ts = new Test();
            ts.exec1();
            ts.exec2();
        }
    }
}
```
In the preceding example, we have the x variable defined outside the exec1() and exec2() methods. The variable has a class scope. It is valid everywhere inside the definition of the Test class, e.g. between its curly brackets.
```cs
public void exec1() 
{        
    Console.WriteLine(this.x);
    Console.WriteLine(x);
}
```
The x variable, also called the x field, is an instance variable. And so it is accessible through the this keyword. It is also valid inside the exec1() method and can be referred by its bare name. Both statements refer to the same variable.
```cs
public void exec2() 
{        
    int z = 5;
    
    Console.WriteLine(x);
    Console.WriteLine(z);
}   
```
The x variable can be accessed also in the exec2() method. The z variable is defined in the exec2() method. It has a method scope. It is valid only in this method.

```cs
1
1
1
5
This is the output of the program.
```
A variable defined inside a method has a local/method scope. If a local variable has the same name as an instance variable, it shadows the instance variable. The class variable is still accessible inside the method by using the this keyword.

#### Program.cs
```cs
using System;

namespace Shadowing
{
    class Test
    {
        int x = 1;

        public void exec()
        {
            int x = 3;

            Console.WriteLine(this.x);
            Console.WriteLine(x);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var ts = new Test();
            ts.exec();
        }
    }
}
```
In the preceding example, we declare the x variable outside the exec() method and inside the exec() method. Both variables have the same name, but they are not in conflict because they live in different scopes.
```cs
Console.WriteLine(this.x);
Console.WriteLine(x);
```
The variables are accessed differently. The x variable defined inside the method, also called the local variable, is simply accessed by its name. The instance variable can be referred by using the this keyword.

```cs
1
3
This is the output of the program.
```
### Static methods
Static methods are called without an instance of the object. To call a static method, we use the name of the class and the dot operator. Static methods can only work with static member variables. Static methods are often used to represent data or calculations that do not change in response to object state. An example is a math library which contains static methods for various calculations. We use the static keyword to declare a static method. When no static modifier is present, the method is said to be an instance method. We cannot use the this keyword in static methods. It can be used in instance methods only.

The Main() method is an entry point to the C# console and GUI application. In C#, the Main() method is required to be static. Before the application starts, no object is created yet. To invoke non-static methods, we need to have an object instance. Static methods exist before a class is instantiated so static is applied to the main entry point.

#### Program.cs
```cs
using System;

namespace StaticMethod
{
    class Basic
    {
        static int Id = 2321;

        public static void ShowInfo()
        {
            Console.WriteLine("This is Basic class");
            Console.WriteLine("The Id is: {0}", Id);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Basic.ShowInfo();
        }
    }
}
```
In our code example, we define a static ShowInfo() method.
```cs
static int Id = 2321;
```
A static method can only work with static variables.
```cs
public static void ShowInfo()
{
    Console.WriteLine("This is Basic class");
    Console.WriteLine("The Id is: {0}", Id);
}
```
This is our static ShowInfo() method. It works with a static Id member.
```cs
Basic.ShowInfo();
```
To invoke a static method, we do not need an object instance. We call the method by using the name of the class and the dot operator.
```cs
$ dotnet run
This is Basic class
The Id is: 2321
This is the output of the example.
```
### Hiding methods
When a derived class inherits from a base class, it can define methods that are already present in the base class. We say that we hide the method of the class that we have derived from. To explicitly inform the compiler about our intention to hide a method, we use the new keyword. Without this keyword, the compiler issues a warning.

#### Program.cs
```cs
using System;

namespace HidingMethods
{
    class Base
    {
        public void Info()
        {
            Console.WriteLine("This is Base class");
        }
    }

    class Derived : Base
    {
        public new void Info()
        {
            base.Info();
            Console.WriteLine("This is Derived class");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var d = new Derived();
            d.Info();
        }
    }
}
```
We have two classes: the Derived and the Base class. The Derived class inherits from the Base class. Both have a method called Info().
```cs
class Derived : Base
{
...
}
```
The (:) character is used to inherit from a class.
```cs
public new void Info()
{    
    base.Info();
    Console.WriteLine("This is Derived class");
}
```
This is an implementation of the Info() method in the Derived class. We use the new keyword to inform the compiler that we are hiding a method from the base class. Note that we can still reach the original Info() method. With the help of the base keyword, we invoke the Info() method of the Base class too.
```cs
$ dotnet run 
This is Base class
This is Derived class
We have invoked both methods.
```
### Overriding methods
Now we will introduce two new keywords: the virtual keyword and the override keyword. They are both method modifiers. They are used to implement polymorphic behaviour of objects. The virtual keyword creates a virtual method. Virtual methods can be redefined in derived classes. Later in the derived class we use the override keyword to redefine the method in question. If the method in the derived class is preceded with the override keyword, objects of the derived class will call that method rather than the base class method.

#### Program.cs
```cs
using System;

namespace Overriding
{
    class Base
    {
        public virtual void Info()
        {
            Console.WriteLine("This is Base class");
        }
    }

    class Derived : Base
    {
        public override void Info()
        {
            Console.WriteLine("This is Derived class");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Base[] objs = { new Base(), new Derived(), new Base(),
                        new Base(), new Base(), new Derived() };

            foreach (Base obj in objs)
            {
                obj.Info();
            }
        }
    }
}
```
We create an array of the Base and Derived objects. We go through the array and invoke the Info() method upon all of them.
```cs
public virtual void Info()
{
    Console.WriteLine("This is Base class");
}
```
This is the virtual method of the Base class. It is expected to be overridden in the derived classes.
```cs
public override void Info()
{
    Console.WriteLine("This is Derived class");
}
```
We override the base Info() method in the Derived class. We use the override keyword.
```cs
Base[] objs = { new Base(), new Derived(), new Base(),
                new Base(), new Base(), new Derived() };
```
Here we create an array of Base and Derived objects. Note that we used the Base type in our array declaration. This is because a Derived class can be converted to the Base class because it inherits from it. The opposite is not true. The only way to have both objects in one array is to use a type which is top most in the inheritance hierarchy for all possible objects.
```cs
foreach (Base obj in objs)
{
    obj.Info();
}
```
We traverse the array and call Info() on all objects in the array.
```cs
$ dotnet run
This is Base class
This is Derived class
This is Base class
This is Base class
This is Base class
This is Derived class
This is the output.
```
Now change the override keyword for new keyword. Compile the example again and run it.

```cs
This is Base class
This is Base class
This is Base class
This is Base class
This is Base class
This is Base class
This time we have a different output.
```
C# local functions
C# 7.0 introduced local functions. These are functions defined inside other methods.

#### Program.cs
```cs
using System;

namespace LocalFunction
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter your name: ");

            string name = Console.ReadLine();
            string message = BuildMessage(name);

            Console.WriteLine(message);


            string BuildMessage(string value)
            {

                string msg = String.Format("Hello {0}!", value);

                return msg;
            }
        }
    }
}
```
In the example, we have a local function BuildMessage(), which is defined and called inside the Main() method.

### Sealed methods
A sealed method overrides an inherited virtual method with the same signature. A sealed method shall also be marked with the override modifier. Use of the sealed modifier prevents a derived class from further overriding the method. The word further is important. First, a method must be virtual. It must be later overridden. And at this point, it can be sealed.

#### Program.cs
```cs
using System;

namespace SealedMethods
{
    class A
    {
        public virtual void F()
        {
            Console.WriteLine("A.F");
        }

        public virtual void G()
        {
            Console.WriteLine("A.G");
        }
    }

    class B : A
    {
        public override void F()
        {
            Console.WriteLine("B.F");
        }

        public sealed override void G()
        {
            Console.WriteLine("B.G");
        }
    }

    class C : B
    {
        public override void F()
        {
            Console.WriteLine("C.F");
        }

        /*public override void G()
        {
            Console.WriteLine("C.G");
        }*/
    }

    class SealedMethods
    {
        static void Main(string[] args)
        {
            B b = new B();
            b.F();
            b.G();

            C c = new C();
            c.F();
            c.G();
        }
    }
}
```
In the preceding example, we seal the method G() in class B.
```cs
public sealed override void G()
{
    Console.WriteLine("B.G");
}
```
The method G() overrides a method with the same name in the ancestor of the B class. It is also sealed to prevent from further overriding the method.
```cs
/*public override void G()
{
    Console.WriteLine("C.G");
}*/
```
These lines are commented because otherwise the code example would not compile. The compiler would give the following error: Program.cs(38,30): error CS0239: 'C.G()': cannot override inherited member 'B.G()' because it is sealed
```cs
c.G();
```
This line prints "B.G()" to the console.
```cs
$ dotnet run 
B.F
B.G
C.F
B.G
This is the output.
```
### Expression body definitions for methods
Expression body definitions for methods allow us to define a method implementation in a very concise, readable form.

method declaration => expression
This is the general syntax.

#### Program.cs
```cs
using System;

namespace ExpBodyDef 
{
    class User 
    {
        public string Name { get; set; }
        public string Occupation { get; set; }

        public override string ToString() => $"{Name} is a {Occupation}";
    }

    class Program 
    {
        static void Main (string[] args) 
        {
            var user = new User();
            user.Name = "John Doe";
            user.Occupation = "gardener";

            Console.WriteLine(user);
        }
    }
}
```
In the example, we provide the body of the ToString() method with an expression body definition.

public override string ToString() => $"{Name} is a {Occupation}";
The expression body definition simplifies the syntax.


Interfaces
A remote control is an interface between the viewer and the TV. It is an interface to this electronic device. Diplomatic protocol guides all activities in the diplomatic field. Rules of the road are rules that motorists, cyclists and pedestrians must follow. Interfaces in programming are analogous to the previous examples.

Interfaces are:

- APIs
- Contracts
Objects interact with the outside world with the methods they expose. The actual implementation is not important to the programmer, or it also might be secret. A company might sell a library and it does not want to disclose the actual implementation. A programmer might call a Maximize() method on a window of a GUI toolkit but knows nothing about how this method is implemented. From this point of view, interfaces are ways through which objects interact with the outside world, without exposing too much about their inner workings.

From the second point of view, interfaces are contracts. If agreed upon, they must be followed. They are used to design an architecture of an application. They help organize the code.

Interfaces are fully abstract types. They are declared using the interface keyword. Interfaces can only have signatures of methods, properties, events, or indexers. All interface members implicitly have public access. Interface members cannot have access modifiers specified. Interfaces cannot have fully implemented methods, nor member fields. A C# class may implement any number of interfaces. An interface can also extend any number of interfaces. A class that implements an interface must implement all method signatures of an interface.

Interfaces are used to simulate multiple inheritance. A C# class can inherit only from one class but it can implement multiple interfaces. Multiple inheritance using the interfaces is not about inheriting methods and variables. It is about inheriting ideas or contracts, which are described by the interfaces.

There is one important distinction between interfaces and abstract classes. Abstract classes provide partial implementation for classes that are related in the inheritance hierarchy. Interfaces on the other hand can be implemented by classes that are not related to each other. For example, we have two buttons. A classic button and a round button. Both inherit from an abstract button class that provides some common functionality to all buttons. Implementing classes are related, since all are buttons. Another example might have classes Database and SignIn. They are not related to each other. We can apply an ILoggable interface that would force them to create a method to do logging.

### Simple interface
The following program uses a simple interface.

#### Program.cs
```cs
using System;

namespace SimpleInterface
{
    interface IInfo
    {
        void DoInform();
    }

    class Some : IInfo
    {
        public void DoInform()
        {
            Console.WriteLine("This is Some Class");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var some = new Some();
            some.DoInform();
        }
    }
}
```
This is a simple C# program demonstrating an interface.
```cs
interface IInfo
{
    void DoInform();   
}
```
This is an interface IInfo. It has the DoInform() method signature.
```cs
class Some : IInfo
```
We implement the IInfo interface. To implement a specific interface, we use the colon (:) operator.
```cs
public void DoInform()
{
    Console.WriteLine("This is Some Class");
}
```
The class provides an implementation for the DoInform() method.

### Multiple interfaces
The next example shows how a class can implement multiple interfaces.

#### Program.cs
```cs
using System;

namespace MultipleInterfaces
{
    interface Device
    {
        void SwitchOn();
        void SwitchOff();
    }

    interface Volume
    {
        void VolumeUp();
        void VolumeDown();
    }

    interface Pluggable
    {
        void PlugIn();
        void PlugOff();
    }

    class CellPhone : Device, Volume, Pluggable
    {
        public void SwitchOn()
        {
            Console.WriteLine("Switching on");
        }

        public void SwitchOff()
        {
            Console.WriteLine("Switching on");
        }

        public void VolumeUp()
        {
            Console.WriteLine("Volume up");
        }

        public void VolumeDown()
        {
            Console.WriteLine("Volume down");
        }

        public void PlugIn()
        {
            Console.WriteLine("Plugging In");
        }

        public void PlugOff()
        {
            Console.WriteLine("Plugging Off");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var cellPhone = new CellPhone();

            cellPhone.SwitchOn();
            cellPhone.VolumeUp();
            cellPhone.PlugIn();
        }
    }
}
```
We have a CellPhone class that inherits from three interfaces.
```cs
class CellPhone : Device, Volume, Pluggable
```
The class implements all three interfaces, which are divided by a comma. The CellPhone class must implement all method signatures from all three interfaces.

```cs
Switching on
Volume up
Plugging In
Running the program we get this output.
```
C# multiple interface inheritance
The next example shows how interfaces can inherit from multiple other interfaces.

#### Program.cs
```cs
using System;

namespace InterfaceInheritance
{
    interface IInfo
    {
        void DoInform();
    }

    interface IVersion
    {
        void GetVersion();
    }

    interface ILog : IInfo, IVersion
    {
        void DoLog();
    }

    class DBConnect : ILog
    {

        public void DoInform()
        {
            Console.WriteLine("This is DBConnect class");
        }

        public void GetVersion()
        {
            Console.WriteLine("Version 1.02");
        }

        public void DoLog()
        {
            Console.WriteLine("Logging");
        }

        public void Connect()
        {
            Console.WriteLine("Connecting to the database");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var db = new DBConnect();

            db.DoInform();
            db.GetVersion();
            db.DoLog();
            db.Connect();
        }
    }
}
```
We define three interfaces. We can organize interfaces in a hierarchy.
```cs
interface ILog : IInfo, IVersion
```
The ILog interface inherits from two other interfaces.
```cs
public void DoInform() 
{
    Console.WriteLine("This is DBConnect class");
}
```
The DBConnect class implements the DoInform() method. This method was inherited by the ILog interface, which the class implements.

```cs
This is DBConnect class
Version 1.02
Logging
Connecting to the database
This is the output.
```

### Polymorphism
The polymorphism is the process of using an operator or function in different ways for different data input. In practical terms, polymorphism means that if class B inherits from class A, it does not have to inherit everything about class A; it can do some of the things that class A does differently.

In general, polymorphism is the ability to appear in different forms. Technically, it is the ability to redefine methods for derived classes. Polymorphism is concerned with the application of specific implementations to an interface or a more generic base class.

Polymorphism is the ability to redefine methods for derived classes.

#### Program.cs
```cs
using System;

namespace Polymorphism
{
    abstract class Shape
    {
        protected int x;
        protected int y;

        public abstract int Area();
    }

    class Rectangle : Shape
    {
        public Rectangle(int x, int y)
        {
            this.x = x;
            this.y = y;
        }

        public override int Area()
        {
            return this.x * this.y;
        }
    }

    class Square : Shape
    {
        public Square(int x)
        {
            this.x = x;
        }

        public override int Area()
        {
            return this.x * this.x;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Shape[] shapes = { new Square(5), new Rectangle(9, 4), new Square(12) };

            foreach (Shape shape in shapes)
            {
                Console.WriteLine(shape.Area());
            }
        }
    }
}
```
In the above program, we have an abstract Shape class. This class morphs into two descendant classes: Rectangle and Square. Both provide their own implementation of the Area() method. Polymorphism brings flexibility and scalability to the OOP systems.
```cs
public override int Area()
{
    return this.x * this.y;
}
...
public override int Area()
{
    return this.x * this.x;
}
```
The Rectangle and the Square classes have their own implementations of the Area() method.
```cs
Shape[] shapes = { new Square(5), new Rectangle(9, 4), new Square(12) };
```
We create an array of three Shapes.
```cs
foreach (Shape shape in shapes)
{
    Console.WriteLine(shape.Area());
}
```
We go through each shape and call the Area() method on it. The compiler calls the correct method for each shape. This is the essence of polymorphism.

### Sealed classes
The sealed keyword is used to prevent unintended derivation from a class. A sealed class cannot be an abstract class.

#### Program.cs
```cs
using System;

namespace DerivedMath
{
    sealed class Math
    {
        public static double GetPI()
        {
            return 3.141592;
        }
    }

    class Derived : Math
    {
        public void Say()
        {
            Console.WriteLine("Derived class");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var dm = new Derived();
            dm.Say();
        }
    }
}
```
In the above program, we have a base Math class. The sole purpose of this class is to provide some helpful methods and constants to the programmer. (In our case we have only one method for simplicity reasons.) It is not created to be inherited from. To prevent uninformed other programmers to derive from this class, the creators made the class sealed. If you try to compile this program, you get the following error: 'Derived' cannot derive from sealed class `Math'.

### Deep copy vs shallow copy
Copying of data is an important task in programming. Object is a composite data type in OOP. Member field in an object may be stored by value or by reference. Copying may be performed in two ways.

The shallow copy copies all values and references into a new instance. The data to which a reference is pointing is not copied; only the pointer is copied. The new references are pointing to the original objects. Any changes to the reference members affect both objects.

The deep copy copies all values into a new instance. In case of members that are stored as references, a deep copy performs a deep copy of data that is being referenced. A new copy of a referenced object is created. And the pointer to the newly created object is stored. Any changes to those referenced objects will not affect other copies of the object. Deep copies are fully replicated objects.

If a member field is a value type, a bit-by-bit copy of the field is performed. If the field is a reference type, the reference is copied but the referred object is not; therefore, the reference in the original object and the reference in the clone point to the same object. (a clear explanation from programmingcorner.blogspot.com)

### Shallow copy
The following program performs shallow copy.

#### Program.cs
```cs
using System;

namespace ShallowCopy
{
    class Color
    {
        public int red;
        public int green;
        public int blue;

        public Color(int red, int green, int blue)
        {
            this.red = red;
            this.green = green;
            this.blue = blue;
        }
    }

    class MyObject : ICloneable
    {
        public int id;
        public string size;
        public Color col;

        public MyObject(int id, string size, Color col)
        {
            this.id = id;
            this.size = size;
            this.col = col;
        }

        public object Clone()
        {
            return new MyObject(this.id, this.size, this.col);
        }

        public override string ToString()
        {
            var s = String.Format("id: {0}, size: {1}, color:({2}, {3}, {4})",
                this.id, this.size, this.col.red, this.col.green, this.col.blue);
            return s;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var col = new Color(23, 42, 223);
            var obj1 = new MyObject(23, "small", col);

            var obj2 = (MyObject) obj1.Clone();

            obj2.id += 1;
            obj2.size = "big";
            obj2.col.red = 255;

            Console.WriteLine(obj1);
            Console.WriteLine(obj2);
        }
    }
}
```
This is an example of a shallow copy. We define two custom objects: MyObject and Color. The MyObject object will have a reference to the Color object.
```cs
class MyObject : ICloneable
```
We should implement ICloneable interface for objects which we are going to clone.
```cs
public object Clone()
{
    return new MyObject(this.id, this.size, this.col);
}
```
The ICloneable interface forces us to create a Clone() method. This method returns a new object with copied values.
```cs
var col = new Color(23, 42, 223);  
```
We create an instance of the Color object.
```cs
var obj1 = new MyObject(23, "small", col);
```
An instance of the MyObject class is created. The instance of the Color object is passed to the constructor.
```cs
var obj2 = (MyObject) obj1.Clone();
```
We create a shallow copy of the obj1 object and assign it to the obj2 variable. The Clone() method returns an Object and we expect MyObject. This is why we do explicit casting.
```cs
obj2.id += 1;
obj2.size = "big";         
obj2.col.red = 255;
```
Here we modify the member fields of the copied object. We increment the id, change the size to "big" and change the red part of the color object.
```cs
Console.WriteLine(obj1);
Console.WriteLine(obj2);
```
The Console.WriteLine() method calls the ToString() method of the obj2 object which returns the string representation of the object.

```cs
id: 23, size: small, color:(255, 42, 223)
id: 24, size: big, color:(255, 42, 223)
```
We can see that the ids are different (23 vs 24). The size is different ("small" vs "big"). But the red part of the color object is same for both instances (255). Changing member values of the cloned object (id, size) did not affect the original object. Changing members of the referenced object (col) has affected the original object too. In other words, both objects refer to the same color object in memory.

### Deep copy
To change this behaviour, we will do a deep copy next.

#### Program.cs
```cs
using System;

namespace DeepCopy
{
    class Color : ICloneable
    {
        public int red;
        public int green;
        public int blue;

        public Color(int red, int green, int blue)
        {
            this.red = red;
            this.green = green;
            this.blue = blue;
        }

        public object Clone()
        {
            return new Color(this.red, this.green, this.blue);
        }
    }

    class MyObject : ICloneable
    {
        public int id;
        public string size;
        public Color col;

        public MyObject(int id, string size, Color col)
        {
            this.id = id;
            this.size = size;
            this.col = col;
        }

        public object Clone()
        {
            return new MyObject(this.id, this.size,
                (Color)this.col.Clone());
        }

        public override string ToString()
        {
            var s = String.Format("id: {0}, size: {1}, color:({2}, {3}, {4})",
                this.id, this.size, this.col.red, this.col.green, this.col.blue);
            return s;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var col = new Color(23, 42, 223);
            var obj1 = new MyObject(23, "small", col);

            var obj2 = (MyObject) obj1.Clone();

            obj2.id += 1;
            obj2.size = "big";
            obj2.col.red = 255;

            Console.WriteLine(obj1);
            Console.WriteLine(obj2);
        }
    }
}
```
In this program, we perform a deep copy on an object.
```cs
class Color : ICloneable
```
Now the Color class implements the ICloneable interface.
```cs
public object Clone()
{
    return new Color(this.red, this.green, this.blue);
}
```
We have a Clone() method for the Color class too. This helps to create a copy of a referenced object.
```cs
public object Clone()
{
    return new MyObject(this.id, this.size, 
        (Color) this.col.Clone());
}
```
When we clone the MyObject, we call the Clone() method upon the col reference type. This way we have a copy of a color value too.

```cs
id: 23, size: small, color:(23, 42, 223)
id: 24, size: big, color:(255, 42, 223)
```
Now the red part of the referenced Color object is not the same. The original object has retained its previous value (23).

C# exceptions
Exceptions are designed to handle the occurrence of exceptions, special conditions that change the normal flow of program execution. Exceptions are raised or thrown.

During the execution of our application many things might go wrong. A disk might get full and we cannot save our file. An Internet connection might go down while our application tries to connect to a site. All these might result in a crash of our application. It is a responsibility of a programmer to handle errors that can be anticipated.

The try, catch and finally keywords are used to work with exceptions.

#### Program.cs
```cs
using System;

namespace DivisionByZero
{
    class Program
    {
        static void Main(string[] args)
        {
            int x = 100;
            int y = 0;
            int z;

            try
            {
                z = x / y;
            } 
             catch (ArithmeticException e)
            {
                Console.WriteLine("An exception occurred");
                Console.WriteLine(e.Message);
            }
        }
    }
}
```
In the above program, we intentionally divide a number by zero. This leads to an error.
```cs
try
{
    z = x / y;
}
```
Statements that are error prone are placed in the try block.
```cs
 catch (ArithmeticException e)
{
    Console.WriteLine("An exception occurred");
    Console.WriteLine(e.Message);
}
```
Exception types follow the catch keyword. In our case we have an ArithmeticException. This exception is thrown for errors in an arithmetic, casting, or conversion operation. Statements that follow the catch keyword are executed when an error occurs. When an exception occurs, an exception object is created. From this object we get the Message property and print it to the console.

```cs
An exception occurred
Attempted to divide by zero.
Output of the code example.
```
### Uncaught exception
Any uncaught exception in the current context propagates to a higher context and looks for an appropriate catch block to handle it. If it can't find any suitable catch blocks, the default mechanism of the .NET runtime will terminate the execution of the entire program.

#### Program.cs
```cs
using System;

namespace UcaughtException
{
    class Program
    {
        static void Main(string[] args)
        {
            int x = 100;
            int y = 0;

            int z = x / y;

            Console.WriteLine(z);
        }
    }
}
```
In this program, we divide by zero. There is no no custom exception handling.

$ dotnet run

Unhandled Exception: System.DivideByZeroException: Division by zero
  at UncaughtException.Main () [0x00000]
The C# compiler gives the above error message.

### IOException
The IOException is thrown when an I/O error occurs. In the following example we read the contents of a file.

#### Program.cs
```
using System;
using System.IO;

namespace ReadFile
{
    class Program
    {
        static void Main(string[] args)
        {
            var fs = new FileStream("langs.txt", FileMode.OpenOrCreate);

            try
            {
                var sr = new StreamReader(fs);
                string line;

                while ((line = sr.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }

            }
            catch (IOException e)
            {
                Console.WriteLine("IO Error");
                Console.WriteLine(e.Message);
            }
            finally
            {
                Console.WriteLine("Inside finally block");

                if (fs != null)
                {
                    fs.Close();
                }
            }
        }
    }
}
```
The statements following the finally keyword are always executed. It is often used for clean-up tasks, such as closing files or clearing buffers.
```
} catch (IOException e)
{
    Console.WriteLine("IO Error");
    Console.WriteLine(e.Message);
} 
```cs
In this case, we catch for a specific IOException exception.
```cs
} finally
{
    Console.WriteLine("Inside finally block");

    if (fs != null)  
    {
        fs.Close();
    }
}
```
These lines guarantee that the file handler is closed.


```cs
C#
Java
Python
Ruby
PHP
JavaScript
These are the contents of the langs.txt file.
```
```cs
C#
Java
Python
Ruby
PHP
JavaScript
Inside finally block
This is the output of the program.
```
We show the contents of the langs file with the cat command and output of the program.

### Multiple exceptions
We often need to deal with multiple exceptions.
```cs
Program.cs
using System;
using System.IO;

namespace MultipleExceptions
{
    class Program
    {
        static void Main(string[] args)
        {
            int x;
            int y;
            double z;

            try
            {
                Console.Write("Enter first number: ");
                x = Convert.ToInt32(Console.ReadLine());

                Console.Write("Enter second number: ");
                y = Convert.ToInt32(Console.ReadLine());

                z = x / y;
                Console.WriteLine("Result: {0:N} / {1:N} = {2:N}", x, y, z);

            }
            catch (DivideByZeroException e)
            {
                Console.WriteLine("Cannot divide by zero");
                Console.WriteLine(e.Message);

            }
            catch (FormatException e)
            {
                Console.WriteLine("Wrong format of number.");
                Console.WriteLine(e.Message);
            }
        }
    }
}
```
In this example, we catch for various exceptions. Note that more specific exceptions should precede the generic ones. We read two numbers from the console and check for zero division error and for wrong format of number.

```cs
Enter first number: we
Wrong format of number.
Input string was not in a correct format.
Running the example we get this outcome.
```
### Custom exceptions
Custom exceptions are user defined exception classes that derive from the System.Exception class.

#### Program.cs
```cs
using System;

namespace CustomException
{
    class BigValueException : Exception
    {
        public BigValueException(string msg) : base(msg) { }
    }

    class Program
    {
        static void Main(string[] args)
        {
            int x = 340004;
            const int LIMIT = 333;

            try
            {
                if (x > LIMIT)
                {
                    throw new BigValueException("Exceeded the maximum value");
                }

            }
            catch (BigValueException e)
            {
                Console.WriteLine(e.Message);
            }
        }
    }
}
```
We assume that we have a situation in which we cannot deal with big numbers.
```cs
class BigValueException : Exception
```
We have a BigValueException class. This class derives from the built-in Exception class.
```cs
const int LIMIT = 333;
```
Numbers bigger than this constant are considered to be "big" by our program.
```cs
public BigValueException(string msg) : base(msg) {}
```
Inside the constructor, we call the parent's constructor. We pass the message to the parent.
```cs
if (x > LIMIT)
{
    throw new BigValueException("Exceeded the maximum value");
}
```
If the value is bigger than the limit, we throw our custom exception. We give the exception a message "Exceeded the maximum value".
```cs
} catch (BigValueException e)
{
    Console.WriteLine(e.Message);
}
```
We catch the exception and print its message to the console.
```cs
$ dotnet run
Exceeded the maximum value
This is the output of the program.
```
