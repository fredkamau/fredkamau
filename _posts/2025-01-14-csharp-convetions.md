---
title: "C# Coding Best Practices"
comments: true
show_date: true
comments: true
classes: wide
image:
    path: /assets/images/csharp.png
tags: [CSharp]
categories: [Csharp]
---

## C# Coding conventions with examples.
### Write code that is readable, maintainable and easy to extend.

Coding conventions are a set of guidelines and standards that every developer should follow when writing code. Code written following the industry best practices is easier to read, understand, maintain and extend. It also improves the clarity of your code, minimizes bugs, and makes collaboration across teams easier.
In this article we will go through the best code conventions that you should follow as a C# developer.

### 1. Naming Conventions

**i) PascalCase(UpperCamelCase)**

PascalCase is used in naming C# types(Classes, Structures, Interfaces etc), Namespaces, Properties, Enums, Constants and read only fields. For example:

```csharp
✅ namespace Myapp{ }
✅ public class Bank { }
✅ public void GetCustomerById(Guid Id) { }
✅ public int BankBalance { get; set; }  
✅ public const int MaxRetryCount = 3;
✅ private readonly string DefaultPath = "/files";
```

**ii) camelCase(lowerCamelCase)**

CamelCase is used to name local variables, method parameters and private fields. You can prefix private fields with an underscore. For example:

```csharp
✅ int itemCount = 10;
✅ void AddCustomer(string customerName) { }
✅ private int _maxLimit;
```

**iii) Use meaningful names.**
All the names should be descriptive and meaningful. The following example is a car class and has a few properties and methods.

        ```csharp
        class Car 
        {
          string color;
          int maxSpeed;
        
          static void Main(string[] args)
          {
            Car myObj = new Car();
            myObj.color = "red";
            myObj.maxSpeed = 200;
            Console.WriteLine(myObj.color);
            Console.WriteLine(myObj.maxSpeed);
          }
        }
        ```

**iv)  Do prefix interfaces with the letter I.**

Interface names should be noun (phrases) or adjectives.
        
```csharp
//Correct
public interface IShape
{
}
public interface ICar
{
}

public interface Car
{
}

//Avoid
public interface Shape
{
}
public interface Car
{
}

public interface ICar
{
}
```

        
    



### 2. Code Formatting and Indentation

**i) Use Braces on a new line(the Allman style)**
   ```csharp
   //Follow this
   if (condition)
   {
      DoSomething();
   }
   // Avoid this
   if (condition) {
   DoSomething();
   }
```

**ii) Avoid Unnecessary blank lines**

  
   ```csharp
   //Follow this
   public void ProcessOrder()
   {
        ValidateOrder();
        SaveOrder();
        SendConfirmation();
   }
   // Avoid this
  public void ProcessOrder()
   {
        ValidateOrder();
        
        SaveOrder();
        
        SendConfirmation();
   }
```

**iii) Indentation**

Indentation refers to the spaces at the beginning of a code line. To enhance code readability use consistent indentation, use four spaces and avoid using tabs to maintain consistency across environments. Remember to keep method statements short by breaking long statements into multiple lines. The preferred length should be less than 15 lines. 


3. Comments 

Comments are excellent tools for explaining the purpose of your code, providing context, and clarifying complex parts of your program. They enable you to document code and clarify complex parts of your program.The following rules should be followed when writing comments:
* Use single-line comments (//) for brief explanations and multi-line comments for longer ones  (/* */) 
* use XML comments For describing methods, classes, fields, and all public members.
* Place comments on a separate line and not at the end of a line of code. 
* Comments should start with a uppercase letter and the text should end with a period.
* Avoid redundant comments as shown in the following example.

```csharp
// Assigns 10 to maxItems
int maxItems = 10;
```

4. General C# coding best practice

a)  Use Named Arguments in method calls

When calling a method, arguments are passed with the parameter name followed by a colon and a value. Named arguments improve code readability especially with methods with multiple parameters.

```csharp
    // Method
    public void DoSomething(string foo, int bar) 
    {
    ...
    }
    // Avoid
    DoSomething("someString", 1);
    // Correct
    DoSomething(foo: "someString", bar: 1);
```


b) Declare all member variables at the top of a class, with static variables at the very top, prevents the need to hunt for variable declarations.

```csharp
// Correct
public class Account
{
  public static string BankName;
  public static string BankBranch;      
  public DateTime DateOpened { get; set; }
  public DateTime DateClosed { get; set; }
  public decimal Balance { get; set; }     
  // Constructor
  public Account()
  {
    // ...
  }
}
```


c) Variable Declaration.
use var when the type is obvious and an explicit type when the type is not obvious
```csharp
//Correct - when the type is obvious
var customer = new Customer();
//Avoid
Customer customer = new Customer();
```

```csharp
//Correct - when the type is not obvious
Dictionary<int, string> customers = GetCustomers();
//Avoid
var customers = GetCustomers(); // Not clear
```

### Conclusion
Code isn't just written for machines, it's written for humans too. Following consistent code conventions leads to a readable, maintainable and extendable code that benefits both small teams and large open source projects. You can use tools like EditorConfig and StyleCop that automatically check and enforce code conventions.

## Thank You!

 I'd love to keep in touch! Feel free to follow me on Twitter at [ @codewithfed](https://twitter.com/codewithfed). If you enjoyed this article please consider sponsoring this blog for more. Your feedback is welcome anytime. Thanks again!
 
 [![][image_ref_zk1zbh8h]](https://ko-fi.com/fredkamau)

 [image_ref_zk1zbh8h]: data:image/png;base64,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

