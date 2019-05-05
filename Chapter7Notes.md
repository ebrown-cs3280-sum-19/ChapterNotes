# Chapter 7 - Methods #

## Packaging Code in C# ##

### Modularizing Programs ###

* Methods (functions or procedures) allow you to modularize an app by separating task into self-contained units
* Usually, **method** refers to a **function** associated with an object but for the most part **function** and **method** are interchangeable
* methods are essentially smaller programs inside a larger program that can be reused

### Calling Methods ###

* Methods are invoked by a method call
* When a method completes, it returns control and possibly a result to its caller

```[C#]
result = objectOne.Method1();
```

## `static` Keyword ##

### `static` Methods ###

* Not all methods are reliant on an object's data to perform it's task
* These methods can be `static` methods meaning you can call them in their `class` rather than in an instantiated object from that `class`

```[C#]
ClassName.MethodName(arguments);
```

### `static` Variables ###

* `static` variables are variables that associated with a class and not to any instances of that class
* If you have a static variable in a class then instantiate an instance of that class, that static variable will have the same value for all instances of the class

```[C#]
MyClass myClass = new MyClass();
Debug.Assert(myClass.SomeStaticVariable == MyClass.SomeStaticVariable); // is true
```

### `static` Class ###

* `static` classes are classes that can't be instantiated
* They can only contain static data members and methods
* they sealed, meaning you cannot inherit a static class from another class

### C# `Math` Class ###

* `Math` is part of the `System` namespace
* Provides a collection of methods that perform mathematical calculations

```[C#]
double value = Math.Sqrt(900.0); // Static method call
```

Some Static Methods in `Math`

* `Abs(x)` absolute value
* `Ceiling(x)` Rounds up to next int
* `Floor(x)` Round down to next int
* `Cos(x)`, `Sin(x)`, `Tan(x)` Trigonmetric functions
* `Pow(x, y)` raise x to power of y
* `Log(x)` natural log
* and more...

### Static Variables ###

* Static variables are associated with the class they are in not any object instantiated from that class
* All instances of the class will share the static variables in it
* `Math` has two static `double` constants that are common math values:
  * `Math.PI`
  * `Math.E`

### `static` Main ###

Why is main declared static?
During app startup, no objects of the class have been created, the `Main` method must be called to begin program execution.
Declaring `Main` as `static` allows the execution environment to call `Main` without creating an instance of the class

## Calling Methods ##

### Three Ways to Call a Method ###

1. Using a method name by itself to call a method of the same class
2. Using a reference to an object, followed by the member-access operator (`.`) and the method name to call non-`static` method of referenced object
3. Using the class name and the `.` operator to call a `static` method of a class

### Three Ways to Return from a Method ###

1. return type `void` with no `return` statement
2. `return;` with return type `void`
3. when the method returns a result and executes this statement `return <expression>;`

## Method Example ##

### Maximum Method ###

```[C#]
class Maximum Finder
{
    static void Main()
    {
        // static methods can directly call other static methods in the same clas
        double result = Maximum(2.0, 4.1, 1.1);
        Console.WriteLine(result); // prints 4.1
    }
    static double Maximum(double x, double y, double z)
    {
        double maximumValue = x;
        if (y > maximumValue)
        {
            maximumValue = y;
        }
        if (z > maximumValue)
        {
          maximumValue = z;
        }
        return maximumValue
    }
}
```

## Method-Call Stack ##

* LIFO - Last In First Out
* **Push** on top to add, **pop** off the top to remove
* Sometimes referred to as the program-execution stack
* Works behind the scenes to support the method call/return mechanism
* It holds each called method's local variables

### Stack Frames ###

* As a method is called it may call another method
* The last called method needs to return before the previously called method can finish
* When a method calls another method an entry is **pushed** on the stack
* This entry are called **stack frame** or **activation record**
* Contains the return address that the called method needs in order to return to the calling method
* When a method finishes the stack frame is **popped** and it transfers control to the return address in the popped stack frame
* A method always can find information it needs at the top of the call stack

### Local Variables and Stack Frames ###

* Stack frames contain local variables for the method
* Local variables only exist while a method is executing
* They persist on the stack when another method is called
* When a method finishes it's frame is **popped** and garbage collections reclaims the memory

### Stack Overflow ###

* You can run out of memory if too much is placed on the stack
* This is called **stack overflow**

## Method Overloading ##

* Methods of the same name in the same class, as long as they have different sets of parameters

### Declaring Overloaded Methods ###

```[C#]
// Fig. 7.14: MethodOverload.cs
// Overloaded method declarations.
using System;

class MethodOverload
{
    // test overloaded square methods
    static void Main()
    {
        Console.WriteLine($"Square of integer 7 is {Square(7)}");
        Console.WriteLine($"Square of double 7.5 is {Square(7.5)}");
    }

    // square method with int argument
    static int Square(int intValue)
    {
        Console.WriteLine($"Called square with int argument: {intValue}");
        return intValue * intValue;
    }

    // square method with double argument
    static double Square(double doubleValue)
    {
        Console.WriteLine(
            $"Called square with double argument: {doubleValue}");
        return doubleValue * doubleValue;
    }
}
```

```[output]
Called square with int argument: 7
Square of integer 7 is 49
Called square with double argument: 7.5
Square of double 7.5 is 56.25
```

* The compiler distiguishes overloaded methods by their **signature**.
* The signature is a combination of the method name and parameters (types and count).
* Its return type is not consider in distinguishing overloaded methods.

```[c#]
void Method1(int a, float b)
```

```[c#]
void Method1(float a, int b)
```

## Optional Parameters ##

* Allows a varying amount of arguments when calling a method
* Optional parameters have a default value that is assignged if the optional argument isn't passed in

```[C#]
static int Power(int baseValue, int exponentValue = 2)
```

### Named Parameters ###

```[C#]
public void SetTime(int hour = 0, int minute = 0, int second = 0)
```

* `t.SetTime() // SetTime(0, 0, 0)`
* `t.SetTime(12) // SetTime(12, 0, 0)`
* `t.SetTime(12, 30) // SetTime(12, 30, 0)`
* `t.SetTime(12, 30, 22) // SetTime 12, 30, 22`

How can you set just some of the arguments?

```[C#]
t.SetTime(12, , 22); // COMPILATION ERROR
```

* `t.SetTime(hour:12, second: 22) // SetTime(12, 0, 22)`
* `t.SetTime(minute: 30) // SetTime(0, 30, 0)`

## Expression Bodied Methods and Properties ##

```[C#]
static int Cube(int x)
{
    return x * x * x;
}
```

to

```[C#]
static int Cube(int x) => x * x * x;
```

* This can be with `static` and non-`static` methods
* `return` types are not required either

```[C#]
static void PrintSomething(string something) => Console.WriteLine(something);
```

## Recursion ##

A **recursive method** is a method that calls itself

### Base Cases and Recursive Calls ###

* Only capable of solving only the simplest case(s) (**base cases**)
* When solving more complex problems it divides the problem in two coneptual pieces (**divide and conquer**)
* A piece that the method knows how to do and piece it doesn't know yet
* The later piece must resemble the original problem just simpler and smaller
* Because it resembles the problem the method can call itself to solve it
* This is called the **recursion step** or **recursive call**
* The original call to the method is still active after the recursive call

### Recursive Factorial Calculation ###

* n! = `n * (n-1) * (n-2) * ... * 1`
* 1! is equal to 1
* 0! is equal to 1
* 5! is 5 * 4 * 3 * 2 * 1 = 120

Nonrecursive implemnation

```[C#]
long factorial = 1;

for (long counter = number; counter >= 1; --counter)
{
   factorial *= counter;
}
```

### Recursive Implementation of Factorial ###
```[C#]
  1   // Fig. 7.17: FactorialTest.cs
  2   // Recursive Factorial method.
  3   using System;
  4
  5   class FactorialTest
  6   {
  7      static void Main()
  8      {
  9         // calculate the factorials of 0 through 10
 10         for (long counter = 0; counter <= 10; ++counter)
 11         {
 12             Console.WriteLine($"{counter}! = {Factorial(counter)}");
 13         }
 14      }
 15
 16      // recursive declaration of method Factorial
 17      static long Factorial(long number)
 18      {
 19         // base case
 20         if (number <= 1)
 21         {
 22            return 1;
 23         }
 24         else // recursion step
 25         {
 26            return number * Factorial(number - 1);
 27         }
 28      }
 29   }
```

```[output]
0! = 1
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
```

## Value vs Reference ##

### Passing Arguments ###

* Pass arguments to method using **pass-by-value** or **pass-by-reference**
* by value 
  * a copy of its value is made and passed into the called method
  * changes made to the copy do not affect the original
* by reference
  * the caller gives the method the ability to access and modify the original variable
  * changes made affect the original

### Value vs Reference Types ###

* Value Types - `int`, `double` and `decimal`
* A variable of a value type contain a value of that type
* Reference Types - refers to an object
* A variable of a reference type contain a location where the data is stored

### `ref` and `out` Parameters ###

* `ref` keyword on a parameter declaration allows you to pass a varible by reference
* `out` creates an **output parameter** that allows the method to write to that variable

```[C#]
static void Square(ref int x) {
    x = x * x;
}

static void Square(out int x) {
    x = 6;
    x = x * x;
}

static void square(int x) {
    x = x * x;
}


static void Main() {
    // display original values of y and z
    Console.WriteLine($"Original value of y: {y}");
    Console.WriteLine("Original value of z: uninitialized\n");

    // pass y and z by reference
    SquareRef(ref y); // must use keyword ref
    SquareOut(out z); // must use keyword out

    // display values of y and z after they’re modified by
    // methods SquareRef and SquareOut, respectively
    Console.WriteLine($"Value of y after SquareRef: {y}");
    Console.WriteLine($"Value of z after SquareOut: {z}\n");

    // pass y and z by value
    Square(y);
    Square(z);

    // display values of y and z after they’re passed to method Square
    // to demonstrate that arguments passed by value are not modified
    Console.WriteLine($"Value of y after Square: {y}");
    Console.WriteLine($"Value of z after Square: {z}");
}
```

```[output]
Original value of y: 5
Original value of z: uninitialized

Value of y after SquareRef: 25
Value of z after SquareOut: 36

Value of y after Square: 25
Value of z after Square: 36
```