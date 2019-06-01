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

## Type Constraints ##

`Maximum` method example

* It uses the type parameter for both return type and parameters
* Normally would need to us the `>` operator
* `>` is not overloaded for every type
* generic code is restricted to operations that are guaranteed for every possible type
* generic code supports only the methods of class `object` by default

### `IComparable<T>` interface ###

* It's possible to compare to of the same type if that type implements `IComparable<T>` (namespace `System`)
* C# simple type types *all* implement `IComparable<T>`
    * `Double` for `double` implements `IComparable<Double>`
    * `Int32` for `int` implements `IComparable<Int32>`
* Types that implement `IComparable<T>` *must* declare a `CompareTo` method


### `CompareTo` Method ###

To compare two `int`s

```[C#]
int1.CompareTo(int2)
```

`CompareTo` must return:
* `0` if the objects are equal
* a negative integer if `int1` is less than `int2`
* a positive integer if `int1` is greater than `int2`

### Specifying Type Constraints ###

Type constarint of `IComparable<T>`

```[C#]
1   // Fig. 20.4: MaximumTest.cs
  2   // Generic method Maximum returns the largest of three objects.
  3   using System;
  4
  5   class MaximumTest
  6   {
  7      static void Main()
  8      {
  9         Console.WriteLine($"Maximum of 3, 4 and 5 is {Maximum(3, 4, 5)}\n");
 10         Console.WriteLine(
 11            $"Maximum of 6.6, 8.8 and 7.7 is {Maximum(6.6, 8.8, 7.7)}\n");
 12         Console.WriteLine("Maximum of pear, apple and orange is " +
 13            $"{Maximum("pear", "apple", "orange")}\n");
 14      }
 15
 16      // generic function determines the
 17      // largest of the IComparable<T> objects
 18      private static T Maximum<T>(T x, T y, T z) where T : IComparable<T>
 19      {
 20         var max = x; // assume x is initially the largest
 21
 22         // compare y with max
 23         if (y.CompareTo(max) > 0)
 24         {
 25             max = y; // y is the largest so far
 26         }
 27
 28         // compare z with max
 29         if (z.CompareTo(max) > 0)
 30         {
 31            max = z; // z is the largest
 32         }
 33
 34         return max; // return largest object
 35      }
 36   }
 ```

 ```[output]
Maximum of 3, 4 and 5 is 5
Maximum of 6.6, 8.8 and 7.7 is 8.8
Maximum of pear, apple and orange is pear
```

### `where` Clause ###

line 18 shows the generic method signature with a type constraint of `IComparable<T>`

```[C#]
18      private static T Maximum<T>(T x, T y, T z) where T : IComparable<T>
```

* Return type and parameter types are all generic `T` type but only `where` `T` has implemented `IComparable<T>`
* `where` can apply multiple type constraints with a comma separated list

## Generic Classes ##

* Generic data structures
* `Stack` of `double`, `Stack` of `int`, `Stack` of `char`

### Stack Class Declaration ###

```[C#]
  1   // Fig. 20.5: Stack.cs
  2   // Generic class Stack.
  3   using System;
  4
  5   public class Stack<T>
  6   {
  7      private int top; // location of the top element
  8      private T[] elements; // array that stores stack elements
  9
 10      // parameterless constructor creates a stack of the default size
 11      public Stack()
 12         : this(10) // default stack size
 13      {
 14         // empty constructor; calls constructor at line 18 to perform init
 15      }
 16
 17      // constructor creates a stack of the specified number of elements
 18      public Stack(int stackSize)
 19      {
 20         if (stackSize <= 0) // validate stackSize
 21         {
 22            throw new ArgumentException("Stack size must be positive.");
 23         }
 24
 25         elements = new T[stackSize]; // create stackSize elements
 26         top = -1; // stack initially empty
 27      }
 28
 29      // push element onto the stack; if unsuccessful,
 30      // throw FullStackException
 31      public void Push(T pushValue)
 32      {
 33         if (top == elements.Length - 1) // stack is full
 34         {
 35            throw new FullStackException(
 36               $"Stack is full, cannot push {pushValue}");
 37         }
 38
 39         ++top; // increment top
 40         elements[top] = pushValue; // place pushValue on stack
 41      }
 42
 43      // return the top element if not empty,
 44      // else throw EmptyStackException
 45      public T Pop()
 46      {
 47         if (top == -1) // stack is empty
 48         {
 49            throw new EmptyStackException("Stack is empty, cannot pop");
 50         }
 51
 52         --top; // decrement top
 53         return elements[top + 1]; // return top value
 54      }
 55   }
```
