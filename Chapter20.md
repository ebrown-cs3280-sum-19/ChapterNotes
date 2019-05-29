# Chapter 20 - Generics #

## Linked Data Structures Review ##

* Linked Lists - Nodes connected together
* Stacks - LIFO
* Queues - FIFO
* Binary Trees - Parent node linked to 2 children nodes

In order to use these structures we need to declare the types they will contain.
In order to make the code more reusable, C# uses the concept of **generics**.

## Introduction to Generics ##

* Allows general models to be created
* Generic methods allow a single method declaration to cover a set of related methods
* Generic classes allow you to declare a set of related classes with a single declaration
* ie. write a single sort method that can sort an arary of `int`s, `double`s and `strings`
* write a single generic stack class that can instantiate a `stack` of `int`, `double`s, `strings` and so on

## Motivation for Generic Methods ##

Overloaded methods are used to perform similar operations on different types of data

Code Example:

``` [c#]
 1   // Fig. 20.1: OverloadedMethods.cs
  2   // Using overloaded methods to display arrays of different types.
  3   using System;
  4
  5   class OverloadedMethods
  6   {
...
 21
 22       // output int array
 23       private static void DisplayArray(int[] inputArray)
 24       {
 25          foreach (var element in inputArray)
 26          {
 27             Console.Write($"{element} ");
 28          }
 29
 30          Console.WriteLine();
 31        }
 32
 33       // output double array
 34       private static void DisplayArray(double[] inputArray)
 35       {
 36          foreach (var element in inputArray)
 37          {
 38             Console.Write($"{element} ");
 39          }
 40
 41          Console.WriteLine();
 42       }
 43
 44       // output char array
 45       private static void DisplayArray(char[] inputArray)
 46       {
 47          foreach (var element in inputArray)
 48          {
 49             Console.Write($"{element} ");
 50          }
 51
 52          Console.WriteLine();
 53       }
 54   }
 ```

* This is a lot of code to have to write that is the exact same logic
* Generic methods will help us solve this

## Generic Method Implementation ##

```[c#]
  1   private static void DisplayArray<T>(T[] inputArray)
  2   {
  3      foreach (var element in inputArray)
  4      {
  5         Console.Write($"{element} ");
  6      }
  7
  8      Console.WriteLine();
  9   }
```

### Generic Method Details ###

* if operations performed by multiple methods are identical for each argument type, you can write a signle generic method declaration
* Actual type names are replaced by convention with `T`
* Calling these methods will be the same: `DisplayArray(inputArray)`

### Type Parameters ###

* All generic method declarations have a *type-parameter list* `<T>`
* Each type-parameter list contains one or more *type parameters* separated by commas
    * e.g. `Dictionary<K, V>`
* A type parameter is an identifier that's used in place of actual type names
* Type parameters can be used to declare the return type, parameter types and local variable types in a generic method declaration
* the type-parameter names in the method declaration must match those declared in the type-parameter list

### Explicit Type Arguments ###

* You can use *explicit type arguments* to idicate the exact type to be used in the function
    * `DisplayArray<int>(intArray)`
* This is required in the case that the compiler cannot infer the type from the method's arugment(s)

