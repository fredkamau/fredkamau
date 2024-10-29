---
title: "Become a better developer by mastering SOLID Principles"
comments: true
show_date: true
comments: true
classes: wide
date: 2022-02-25 08:52
tags: [Solid priciples, csharp, .NET, OOP]
categories: [OOP, Solid priciples]
published: true
mermaid: true
---
#### The SOLID Principles using C# - Principles of Object Oriented Design
##### How to write code that is easy to maintain, extend and understand.


**Object-Oriented Programming(OOP)** brought a new design to software development.It organizes software design around data, or objects, rather than functions and logic. OOP focuses on the objects that developers want to manipulate rather than the logic required to manipulate them.This enables developers to combine data with the same functionality in one class to deal with the sole purpose there, regardless of the entire application. However, Object-oriented programming can be complex when creating programs based on interaction of objects which results to confusing and unmaintainable programs.

As such, five guidelines were developed by **Robert C. Martin** (Uncle Bob). These five guidelines/principles made it easy for developers to:
* ***Create more maintainable programs*** - SOLID principles makes programs easy to read and understand thus spending less time figuring what it does and focus on developing the solution
* ***Create Testable Programs*** - Test driven development is required when we design large scale systems which is important in an application life cycle.
* ***Flexibility and Extensibilty*** - Business requirement change often, SOLID principles will enable you to easily extend the system with new functionality without breaking the existing ones
* ***Create Loose Coupled Programs*** - Loose coupling is an approach where we interconnect components. Loosely coupled class objects minimize changes in your code, help in making code more reusable, maintainable, flexible, and stable.


These five principles were called the S.O.L.I.D principles:
*  Single Responsibility Principle
*  Open-Closed Principle
*  Liskov Substitution Principle
*  Interface Segregation Principle
* Dependency Inversion Principle

### 1. The Single Responsibility Principle
The Single Responsibility Principle states that: 
> *A class should have one, and only one, reason to change*

This simply means that a class should have one responsibility and therefore it should have only a single reason to change. This does not mean that a class should have one method, but instead all the methods should relate to a single purpose(high cohesion). This makes the classes smaller and cleaner.

Classes don't often start with low cohesion, but often after several releases and different developers adding data and more behaviors in a class, suddenly the class becomes a **monster or god class** as some people call it. This makes the code lengthy, complex and difficult to maintain.

Let's look at the code for a simple **Person** class as an example. This class should not have an Email validation method as it is not related to a **Person** behavior.
  ```
class Person
    {
        public string Name;
        public string Gender;
        public DateTime DOB;
        public string Email;


        public Person(string name, string gender, DateTime dob, string email)
        {
            this.Name = name;
            this.DOB = dob;
            this.Gender = gender;

            if (validateEmail(email))
            {
                this.Email = email;
            }
        }

        public static bool validateEmail(string email)
        {
            var trimmedEmail = email.Trim();

            if (trimmedEmail.EndsWith("."))
            {
                return false;
            }
            try
            {
                var addr = new System.Net.Mail.MailAddress(email);
                return addr.Address == trimmedEmail;
            }
            catch
            {
                return false;
            }
        }

        public void greetPerson()
        {
            Console.WriteLine($"Hello: {this.Name}");
        }
    }
  ```
We can purge the validateEmail Method from the Person Class and create an Email class that will have that responsibility.

```
class Person
    {
        public string Name;
        public string Gender;
        public DateTime DOB;
        public string email;


        public Person(string name, string gender, DateTime dob, string email)
        {
            this.Name = name;
            this.DOB = dob;
            this.Gender = gender;

            if (Email.validateEmail(email))
            {
                this.email = email;
            }
        }

        public void greetPerson()
        {
            Console.WriteLine($"Hello: {this.Name}");
        }
    }
    
    class Email
    {
        public string email;

        public Email(string email)
        {
            if (validateEmail(email))
            {
                this.email = email;
            }
        }

        public static bool validateEmail(string email)
        {
            var trimmedEmail = email.Trim();

            if (trimmedEmail.EndsWith("."))
            {
                return false;
            }
            try
            {
                var addr = new System.Net.Mail.MailAddress(email);
                return addr.Address == trimmedEmail;
            }
            catch
            {
                return false;
            }
        }

    }

```

Pay extra attention when creating a class to make sure it has one responsibility for easy understanding, maintenance and re usability.

### 2. The Open Close Principle - extending your entities correctly

The Open close principle is the most misunderstood solid principle mainly because it's definition is poorly phrased. However, when correctly applied it can save you more development time compared to others. The principle originally stated that:
> *"classes should be open for extension and closed to modification."*

Later on when Uncle Bob included it in his SOLID principles he put it much better:

> *"You should be able to extend the behavior of a system without having to modify that system."*


Modification simply means changing the code and extension means adding new functionality.



A class should be designed in such a way that it's easy to extend it through **inheritance** without modifying it. If you want to add additional functionality or change the existing class, create a child class instead of changing the original. This makes sure that anyone using the base class does not have to worry about it's purpose changing later on.

This principle can be applied when writing a software package or library that is used by many third parties. Ideally you would like the library to be used in the widest variety by it's consumers, that is, it should be open for extension. However, you wouldn't like to change the existing code functionality since this forces your library consumers to update their versions and also fix the breaking changes. This makes your package more reliable and stable because it ideally get tested over and over in different contexts.
The open/close principle is used to mitigate potential bugs when adding new features. When you don't touch existing code that works, you can be assured that your code will not break which reduces maintenance costs and improves product stability.

#### Example
Imagine you use an external library which contains a class Car. The Car has a method brake. In its base implementation, this method only slows down the car but you also want to turn on the brake lights. You would create a subclass of Car and override the method brake. After calling the original method of the super class, you can call your own turnOnBrakeLights method. This way you have extended the Car‘s behavior without touching the original class from the library.

### 3. Liskov Subtitution Principle
The Liskov subtitution principle states that:
> "Subtypes must be substitutable for their base types."

This principle was created by Barbara Liskov and it's main objective is to avoid throwing exceptions when inheritance is not used in the right way. Inheritance is an OOP paradigm that enables us to reuse the implementation of base classes; one class can inherit all the attributes and behaviors of another class. Inheritance is supposed to be used by classes that are similar. This requires the objects in your parent class to behave the same way as objects in your child class. An overridden method in a child class also needs to accept the same parameters as the parent class.

#### Example
A good example for illustrating the principle as given by Uncle Bob in a podcast recently is how something can sound right in the natural language but doesn't work correctly on code.

#### Typical Violation of the Principle 

```
  class Bird
    {
        public string Species { get; set; }
        public int Weight { get; set; }
        public int Color { get; set; }

        public void Fly()
        {
            Console.WriteLine("Bird Flies");
        }
    }

    class Pigeon : Bird { }

```

The Pigeon can fly because it's a bird.

```
    class Ostrich : Bird { }
```
An ostrich is a bird but it can't fly. Ostrich is a child class of class bird but it should not be able to use the fly() method which means it's breaking the LSK principle. 
```
    static void Main(string[] args)
    {
        Bird b = new Ostrich();
        b.Fly();
        Console.ReadKey();
    }
```

#### Compliance with the Principle

```
class Bird
    {
        public string Species { get; set; }
        public int Weight { get; set; }
        public int Color { get; set; }
    }

    class FlyingBird : Bird
    {
        public void Fly()
        {
            Console.WriteLine("Bird Flies");
        }

    }

    class Pigeon : FlyingBird 
    { 
        
    }

    class Ostrich : Bird 
    {

    }
```

A common code smell for the violation of this principle is when a parent class property or method is not applicable to a child class. If it behaves like a duck, it's certainly a bird. If it behaves like a duck but need batteries to fly - you probably have the wrong abstraction.

### 4. The Interface Segregation Principle

The interface segregation principle was developed by Uncle Bob when he was consulting for Xerox, a company that produces printers. He was assisting them to build new software for printer systems. The principle states that:

> *"Clients should not be forced to depend upon interfaces that they do not use"*

The principle relates to Single Responsibility Principle in that, ***Interfaces should also have a single purpose***.

Classes that should not be forced to implement interface members that they don't use.

##### **Typical violation of the principle**
Let's imagine you are responsible for developing a new printing software for **Xerox**. This is a new system developed from scratch. The modern printers should be able to print, scan and fax.

You define an IModernXerox interface that models the basic tasks performed by the printer.

 ```

 interface IModernXerox
{
    bool PrintContent(string content);
    bool ScanContent(string content);
    bool FaxContent(string content);
}
    
   ```

You define your printer class as follows:
  ```
 class Xerox3Printer : IModernXerox
    {
        public bool FaxContent(string content)
        {
            Console.WriteLine("Fax Done");
            return true;
        }

        public bool PrintContent(string content)
        {
            Console.WriteLine("Print Done");
            return true;
        }

        public bool ScanContent(string content)
        {
            Console.WriteLine("Scan Done");
            return true;
        }
    }
  ```
The new printing system becomes a big success, Xerox new three in one printer sales are impressive!
Your boss asks you to build a new economic printer that can only Print and Scan. Considering the printer falls under the same line of new modern printers you decide to use the same IModernXerox Interface. 
```
class Xerox4Printer : IModernXerox
    {
        

        public bool PrintContent(string content)
        {
            Console.WriteLine("Print Done");
            return true;
        }

        public bool ScanContent(string content)
        {
            Console.WriteLine("Scan Done");
            return true;
        }

        public bool FaxContent(string content)
        {
            throw new NotImplementedException();
        }
    }
    
   ```

 This is where the violation of the principle happens, since Xerox4Printer is forced to implement faxing method which it does not support.
 
##### **Compliance with the Principle**

The main problem with the IXerox3Printer is that we use one general 'god' interface instead of segregating the fat interface into basic tasks of a modern Xerox printer and advanced features such as faxing. 

   ```
  interface IModernXeroxBasicTasks
    {
        bool PrintContent(string content);
        bool ScanContent(string content);
    }

    interface FaxContent
    {
        bool FaxContent(string content);
    }
   ```

We modify the Xerox3Printer so that it can use the specialized interfaces:
   ```
 class Xerox3Printer : IModernXeroxBasicTasks, FaxContent
    {
        public bool FaxContent(string content)
        {
            Console.WriteLine("Fax Done");
            return true;
        }

        public bool PrintContent(string content)
        {
            Console.WriteLine("Print Done");
            return true;
        }

        public bool ScanContent(string content)
        {
            Console.WriteLine("Scan Done");
            return true;
        }
    }
   ```

Now Xerox4Printer can be defined without depending upon methods that they will never use.
 ```
class Xerox4Printer : IModernXeroxBasicTasks
    {

        public bool PrintContent(string content)
        {
            Console.WriteLine("Print Done");
            return true;
        }

        public bool ScanContent(string content)
        {
            Console.WriteLine("Scan Done");
            return true;
        }
    }
   ```

Finally our solution complies with Interface Segregation Principle.

#### When to apply the principle

The principle just like SRP is very difficult in the first iterations to identify parts that will violate the principle. My advice is to wait your code to evolve so that you can identify where to apply it. Do not try to guess future software requirements this may complicate your solutions.

### 5. The Dependency Inversion Principle 
This is the final SOLID principle and a very important one. Dependency inversion Principle forms the foundation of the most useful feature that a lot of modern frameworks use known as **Dependency Injection**. It gives your architecture the flexibility to achieve separation of concerns between the presentation, business and data layer.
Uncle Bob defines DI as follows:

> *"A. High-level modules should not depend on low-level modules. Both should depend on abstractions."*

#### High-level modules and Low-level modules
The concept of modules comes from Modular programming which is a software development technique that advocates the breaking down of a system into small programs/components which accomplishes a single purpose and contains everything to accomplish this.

A system is built using one more modules, which can grouped into different layers.For example a calculator system can be broken down into the following modules:

![][image_ref_t38dhks5]

In this example, there is the high and the low level modules.
High level modules are modules that are directly used in the presentation layer for example the Calculator class.On the other hand, low-level modules helps the high level modules to accomplish their work. Low level modules are also referred as **dependencies**.

Dependencies are established when one module needs another module to complete it's work. For example, the Calculator Modules needs the Add module to achieve it's goal and therefore a dependency is achieved.
The above design can be implemented as follows:
##### The Calculator class


```
class Calculator
    {

        public enum Operation
        {
            ADD, SUBTRACT, MULTIPLY, DIVIDE
        }

        //@param numA              First number.
        //@param numB              Second number.
        //@param operation         Type of operation.
        //@return                  Operation's result.

        public double calculate(double numA, double numB, Operation op)
        {
            double result = 0;
            switch (op.ToString())
            {
                case "ADD":
                    AddOperation addOp = new AddOperation();
                    result = addOp.add(numA, numB);
                    break;
                case "SUBTRACT":
                    SubtractOperation subOp = new SubtractOperation();
                    result = subOp.subtract(numA, numB);
                    break;
                case "MULTIPLY":
                    MultiplyOperation multOp = new MultiplyOperation();
                    result = multOp.multiply(numA, numB);
                    break;
                case "DIVIDE":
                    DivideOperation divOp = new DivideOperation();
                    result = divOp.divide(numA, numB);
                    break;
            }

            return result;
        }

    }

```
##### The Calculator Dependency classes - low level modules

```
class AddOperation
    {
        public double add(double numA, double numB)
        {
            return numA + numB;
        }
    }

    class SubtractOperation
    {
        public double subtract(double numA, double numB)
        {
            return numA - numB;
        }
    }

    class MultiplyOperation
    {
        public double multiply(double numA, double numB)
        {
            return numA * numB;
        }
    }

    class DivideOperation
    {
        public double divide(double numA, double numB)
        {
            return numA / numB;
        }
    }
```

The Calculator class violates the dependency inversion principle. If we want to add a new operation such as finding a modules, we must modify the class, which conflicts with Open/Close Principle.
#### Application of the Dependency Inversion Principle
In order to comply with dependency inversion and OCP principle, we must add an abstraction and modify the dependencies.

![][image_ref_x2qojmr6]

Now use can change one side of the dependency without affecting the other side, you can also add more operations without modifying the Calculator module.

```
class Calculator
    {

        //@param numA              First number.
        //@param numB              Second number.
        //@param operation         Type of operation.
        //@return                  Operation's result.
        private ICalculatorOperation _calculatorOperation;
        public Calculator(ICalculatorOperation calculatorOperation)
        {
            this._calculatorOperation = calculatorOperation;
        }

        public double calculate(double numA, double numB, ICalculatorOperation operation)
        {
            return operation.calculate(numA, numB);
        }

    }

    interface ICalculatorOperation
    {
        public double calculate(double numbA, double numB);
    }

    class AddOperation : ICalculatorOperation
    {

        public double calculate(double numbA, double numB)
        {
            return numbA + numB;
        }
    }

    class SubtractOperation : ICalculatorOperation
    {
        public double calculate(double numbA, double numB)
        {
            return numbA - numB;
        }

    }

    class MultiplyOperation : ICalculatorOperation
    {
        public double calculate(double numbA, double numB)
        {
            return numbA * numB;
        }
    }

    class DivideOperation : ICalculatorOperation
    {
        public double calculate(double numbA, double numB)
        {
            return numbA / numB;
        }

    }

```
```
 static void Main(string[] args)
{
    //create an object
    AddOperation addOperation = new AddOperation();
    //pass the dependancy
    Calculator calculator = new Calculator(addOperation);

    var number = calculator.calculate(2.3, 3.4, addOperation);
    Console.WriteLine(number);
    Console.ReadKey();
}
```

### Final thoughts on the SOLID principles
The SOLID principles are guidelines that helps you create code that is extendable, maintainable and understand. After finally getting some piece of code to work, you're only done with half the job; you should spend roughly the same amount of time cleaning it. No one writes clean code first because it's just too hard to get code to work. SOLID principles are not laws. They will however enable you write clean code.
Always remember that:
> "You are not done when it works, you are done when it's right." - *Uncle Bob*


## Thank You!

I'd love to keep in touch! Feel free to follow me on Twitter at [ @codewithfed](https://twitter.com/codewithfed). If you enjoyed this article please consider sponsoring me for more. Your feedback is welcome anytime. Thanks again! 

[![][image_ref_h8627dve]](https://ko-fi.com/fredkamau)


[image_ref_t38dhks5]: data:image/jpeg;base64,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AAAAAAAAAAAAAAAAARpZAAA/PD7gAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADB8Z+iAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAH//EAD0QAAADBAgEBAQHAQACAgMAAAACBgEDBAUREhUWIDE2VjA1VWETFFFUMzdQUgcQFyFAQVNiMkIiYCRwgP/aAAgBAQABCQD/APb7TMYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYKzBWYK5cRm0MEzmc9j56/lksfWatNy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdy2atdymli0azUkB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


[image_ref_x2qojmr6]: data:image/jpeg;base64,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


[image_ref_h8627dve]: data:image/png;base64,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
