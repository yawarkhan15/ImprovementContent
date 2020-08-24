# Namespaces

## Introduction
Namespaces are used to organize code at the highest logical level. They classify and present programming elements that are exposed to other programs and applications. Within a namespace, we can declare another namespace, a class, an interface, a structure, an enumeration or a delegate.

## Scope
We cannot define items such as properties, variables and events. These items must be declared within containers such as structures or classes. Namespaces prevent ambiguity and simplify references when using large groups of objects such as class libraries.

Namespaces organize objects in an assembly. An assembly is a reusable, versionable and self-describing building block of a CLR application. Assemblies can contain multiple namespaces. Namespaces can contain other namespaces. An assembly provides a fundamental unit of physical code grouping. A namespace provides a fundamental unit of logical code grouping.

## Creating a namespace
The namespace keyword is used to declare a namescpace in C#. The name of the namespace must be a valid C# identifier name. Namespaces are delimited with the . operator. The using directive removes the requirement to specify the name of the namespace for every class.


### Built-in namespaces
The built-in libraries are organized within namespaces.


#### Program.cs
```cs
public class Program
{
    static void Main()
    {
        System.Console.WriteLine("Simple namespace example");
    }
}
```
For instance, the Console class is available within the System namespace. To call the static WriteLine() method of the Console class, we use its fully qualified name. Fully qualified names are object references that are prefixed with the name of the namespace where the object is defined.

#### Program.cs
```cs
using System;

public class Program
{
    static void Main()
    {
        Console.WriteLine("Simple namespace example");
    }
}
```
With the using statement, we include the System namespace into our program. Now we can call the Console.WriteLine() without explicitly specifying the System.

### Sharing namespace
In the following code, we have two files that share the same namespace.

#### Counter.cs
```cs
using System;

namespace Sharing
{
    class Counter
    {
        public int x = 0;
        
        public void Inc()
        {
            x += 100;
            Console.WriteLine(x);
        } 
    }
}
```
We have a Sharing namespace. In the namespace, we have an Counter class.
```cs

namespace Sharing
{
...
}
```
We declare a namespace called Sharing. The code goes inside the curly brackets of the Sharing namespace.
#### Program.cs

```cs
namespace Sharing
{
    public class Program
    {
        static void Main()
        {
            var counter = new Counter();
            
            counter.Inc();
            counter.Inc();
        }
    }
}
```
In the Program class, we work with the Counter class from the previous file. We invoke its Inc() method.
```cs
namespace Sharing
{
...
```
We work in the same namespace.
```cs
var counter = new Counter();
    
counter.Inc();
counter.Inc();
```
We create an instance of the Counter class. We call its Inc() method twice. Because we work with objects of the same namespace, we do not need to specify its name explicitly.

```
100
200
This is the example output.
```

### Distinct namespaces
The following code example has two distinct namespaces. We use the using keyword to import elements from a different namespace.

#### Basic.cs
```cs
namespace Mathematical
{
    public class Basic
    {
        public static double PI = 3.141592653589;
        
        public static double GetPi()
        {
            return PI;
        } 
    }
}
```
In the Basic class, we define a PI constant and a GetPi() method. The Basic class is defined within the Mathematical namespace.

#### Program.cs
```cs
using System;
using Mathematical;

namespace Distinct
{
    public class Program
    {
        static void Main()
        {
            Console.WriteLine(Basic.PI);
            Console.WriteLine(Basic.GetPi());

            Console.WriteLine(Mathematical.Basic.PI);
            Console.WriteLine(Mathematical.Basic.PI);
        }
    }
}
```
In this file, we use the elements from the MyMath namespace.
```cs
using Mathematical;
```
We import the elements from the MyMath namespace into our namespace.
```cs
Console.WriteLine(Basic.PI)
Console.WriteLine(Basic.GetPI())
```
Now we can use those elements. In our case it is the Basic class.
```cs
Console.WriteLine(Mathematical.Basic.PI);
Console.WriteLine(Mathematical.Basic.PI);
```
### Root namespace
The root namespace is the mainspace of the .NET Framework libraries. It may happen that someone creates a type or a namespace that will conflict with ones from the .NET Framework. In such cases, we can refer to the root namespace with the global:: prefix.

#### Program.cs
```cs
namespace ZetCode
{
    class System 
    {
        public override string ToString() 
        {
            return "This is System class";
        }
    }

    public class Program
    {
        static void Main()
        {
            var sys = new System();
            global::System.Console.WriteLine(sys); 
        }
    }    
}
```
In our ZetCode namespace, we create a System class that will clash with the one from the .NET Framework.
```cs
var sys = new System();
```
Here we refer to the System class from the ZetCode namespace.
```cs
global::System.Console.WriteLine(sys); 
```
With the global:: prefix, we point to the System class of the root namespace.

### Default namespace
The root namespace is also the default namespace for C# programs. Elements that are not included in a namespace are added to the unnamed default namespace.

#### Program.cs
```cs
using System;

struct Book 
{
    public override string ToString()
    {
        return "Book struct in a default namespace";
    }
}

namespace MainProgram
{
    struct Book 
    {
        public override string ToString()
        {
            return "Book struct in a MainProgram namespace";
        }
    }

    public class Program
    {
        static void Main()
        {
            Book book1;
            global::Book book2;

            Console.WriteLine(book1);
            Console.WriteLine(book2);
        }
    }
}
```
We have two Book structures; one is defined in the MainProgram namespace, the other is defined outside this namespace.

```cs
struct Book 
{
    public override string ToString()
    {
        return "Book struct in a default namespace";
    }
}
```
This Book structure is defined outside of the custom named MainProgram namespace. It belongs to the default namespace.

```cs
Book book1;
```
We refer to the structure defined inside the MainProgram namespace.

```cs
global::Book book2;
```
With the global:: prefix we point to the structure defined outside the MainProgram namespace.

```cs
Book struct in a MainProgram namespace
Book struct in a default namespace
This is the output of the program.
```
### C# namespace aliasing
The using keyword can be used to create an alias for a namespace. With nested namespaces, the fully qualified names might get long. We can shorten them by creating aliases.

#### Program.cs
```cs
namespace Adappt
{
    namespace Items
    {
        class Book 
        {
            public override string ToString()
            {
                return "This is a book";
            }
        }
    } 
}
```
```cs
namespace MainProgram
{
    using ZIB = Adappt.Items.Book;

    public class Aliases
    {
        static void Main()
        {
            Adappt.Items.Book book =  new Adappt.Items.Book();
            ZIB book2 = new ZIB();
 
            System.Console.WriteLine(book);
            System.Console.WriteLine(book2);
        }
    }
}
```
In the example, we create an alias for a Book class that is enclosed by two namespaces.

```cs
namespace Adappt
{
    namespace Items
    {
        class Book 
        {
        ...
        }
    } 
}
```
It is possible to nest a namespace into another namespace. The fully qualified name of the Book class is Adappt.Items.Book.

```cs
using ZIB = Adappt.Items.Book;
```
The using keyword createas a ZIB alias for the fully qualified name Adappt.Items.Book.

```cs
Adappt.Items.Book book =  new Adappt.Items.Book();
ZIB book2 = new ZIB();
```
We use both names to create a book instance.
