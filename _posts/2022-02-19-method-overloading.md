---
layout: post
title: Method Overloading in Csharp
date: 2022-02-19 00:00:00
description: Deep dive to Polymorphism.
tags: [csharp, .NET, method overloading, polymorphism, OOP]
categories: [OOP]
published: true
mermaid: true
---

## Method Overloading in C#
In this article we will learn about Method Overloading which is an example of polymorphism, a pillar of object oriented programming.
Method overloading is the ability to redefine a method more than one times, that is creating a multiple methods in a class that share the same name. The overloaded methods can have the same name but with different signatures. Method signatures simply means that the number and type of parameters passed as arguments. Method overloading can be done by changing the following:

* The number of parameters
* The data types of the parameters
* The order of the parameters


### The number of parameters
```
class MultiplyNumbers
    {
        public int Product(int a, int b)
        {
            int product = a * b;
            return product;
        }
        public int Product(int a, int b, int c)
        {
            return a * b * c;
        }

        public static void Main(string[] args)
        {
            MultiplyNumbers multiplyNumbers = new MultiplyNumbers();
            int product = multiplyNumbers.Product(5, 6);

            Console.WriteLine($"The product of the two numbers is: {product}");

            MultiplyNumbers multiplyNumbers2 = new MultiplyNumbers();
            int product2 = multiplyNumbers2.Product(5, 6, 7);

            Console.WriteLine($"The product of the two numbers is: {product}");
        }

```
##### The output
>The product of the two numbers is: 30

>The product of the two numbers is: 210

### The data types of parameters

```
    class MultiplyNumbers
    {
        public float Product(float a, float b)
        {
            return a * b;
        }
        public int Product(int a, int b)
        {
            return a * b;
        }

        public static void Main(string[] args)
        {
            MultiplyNumbers multiplyNumbers = new MultiplyNumbers();
            float product = multiplyNumbers.Product(5.67F, 6.2F);

            Console.WriteLine($"The product of the two numbers is: {product}");

            MultiplyNumbers multiplyNumbers2 = new MultiplyNumbers();
            int product2 = multiplyNumbers2.Product(5, 6);

            Console.WriteLine($"The product of the two numbers is: {product}");
        }
    }
```
##### The output
>The product of the two numbers is: 35.154

>The product of the two numbers is: 30

### The number of parameters
```
// C# program to demonstrate the method
// overloading by changing the
// Order of the parameters

using System;

    // C# program to demonstrate the function
    // overloading by changing the
    // Order of the parameters

    class Employee
    {
        public void Identity(String name, int id)
        {

            Console.WriteLine($"Name:{name}, ID:{id}");
        }

        public void Identity(int id, String name)
        {

            Console.WriteLine($"Name:{name}, ID:{id}");
        }


        public static void Main(string[] args)
        {
            Employee emp1 = new Employee();
            emp1.Identity("John Doe", 1);

            Employee emp2 = new Employee();
            emp1.Identity(2, "Mary Doe");
        }
    }

```

>Name : John Doe, ID : 1

>ID : 2, Name : Mary Doe

#### Why we need Method Overloading

Coming up with different Method names that perform the same operation can be a challenge. Method overloading is important when we need to perform the same operation in different ways for different inputs.

## Thank You!

I'd love to keep in touch! Feel free to follow me on Twitter at [ @codewithfed](https://twitter.com/codewithfed). If you enjoyed this article please consider sponsoring me for more. Your feedback is welcome anytime. Thanks again!

[![][image_ref_h8627dve]](https://ko-fi.com/fredkamau)


[image_ref_zk1zbh8h]: data:image/png;base64,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
