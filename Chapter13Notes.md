# Chapter 13 - Exception Handling: A Deeper Look #

## Example: Divide by Zero ##

### Without Exception Handling ###

```[C#]
 1 // Fig. 13.1: DivideByZeroNoExceptionHandling.cs
 2 // Integer division without exception handling.
 3 using System;
 4
 5 class DivideByZeroNoExceptionHandling
 6 {
 7    static void Main()
 8    {
 9       // get numerator
10       Console.Write("Please enter an integer numerator: ");
11       var numerator = int.Parse(Console.ReadLine());
12
13       // get denominator
14       Console.Write("Please enter an integer denominator: ");
15       var denominator = int.Parse(Console.ReadLine());
16
17       // divide the two integers, then display the result
18       var result = numerator / denominator;
19       Console.WriteLine(
20          $"\nResult: {numerator} / {denominator} = {result}");
21    }
22 }
```

```[output]
Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

```[output]
Please enter an integer numerator: 100
Please enter an integer denominator: 0

Unhandled Exception: System.DivideByZeroException:
   Attempted to divide by zero.                   
   at DivideByZeroNoExceptionHandling.Main()
      in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_01\
      DivideByZeroNoExceptionHandling\DivideByZeroNoExceptionHandling\
      DivideByZeroNoExceptionHandling.cs: line 18
```

* The exception will terminate the program (if unhandled)
* it will output a stack trace
* it will tell you the exception name
* it will display a message about the exception
* `at` lines tell you the line that the exception occurred

### With Exception Handling ###

```[C#]
1   // Fig. 13.2: DivideByZeroExceptionHandling.cs
  2   // FormatException and DivideByZeroException handlers.
  3   using System;
  4
  5   class DivideByZeroExceptionHandling
  6   {
  7       static void Main(string[] args)
  8       {
  9          var continueLoop = true; // determines whether to keep looping
 10
 11          do
 12          {
 13               // retrieve user input and calculate quotient
 14               try                                                           
 15               {                                                             
 16                   // int.Parse generates FormatException                    
 17                   // if argument cannot be converted to an integer          
 18                   Console.Write("Enter an integer numerator: ");            
 19                   var numerator = int.Parse(Console.ReadLine());            
 20                   Console.Write("Enter an integer denominator: ");          
 21                   var denominator = int.Parse(Console.ReadLine());          
 22                                                                             
 23                   // division generates DivideByZeroException               
 24                   // if denominator is 0                                    
 25                   var result = numerator / denominator;
 26                                                                             
 27                   // display result                                         
 28                   Console.WriteLine(                                        
 29                      $"\nResult: {numerator} / {denominator} = {result}");  
 30                   continueLoop = false;                                     
 31               }                                                             
 32               catch (FormatException formatException)                       
 33               {                                                             
 34                  Console.WriteLine($"\n{formatException.Message}");         
 35                  Console.WriteLine(                                         
 36                     "You must enter two integers. Please try again.\n");    
 37               }
 38               catch (DivideByZeroException divideByZeroException)           
 39               {                                                             
 40                  Console.WriteLine($"\n{divideByZeroException.Message}");   
 41                  Console.WriteLine(
 42                     "Zero is an invalid denominator. Please try again.\n"); 
 43               }                                                             
 44            } while (continueLoop);
 45        }
 46   }
 ```

 ```[output]
Enter an integer numerator: 100
Enter an integer denominator: 0

Attempted to divide by zero.
Zero is an invalid denominator. Please try again.

Enter an integer numerator: 100
Enter an integer denominator: hello
Input string was not in a correct format.
You must enter two integers. Please try again.

Enter an integer numerator: 100
Enter an integer denominator: 7

Result: 100 / 7 = 14
```

>NOTE: `TryParse` is a more preferred method to validate input

* Exception-handling code appears in the `catch` block
* You can specify specific exception types in the catch block or use the base type `Exception`
* using `Exception` is known as a general `catch` clause
* you can have many `catch` blocks
* you can have 0 or 1 `finally` block
* Uncaught exceptions are ones that there is no matching `catch` black for
  
### Termination Model of Exception Handling ###

* The point in code at which an exception occurs is the *throw point*
* When a code encounters an exception it exits the `try` block and enters the `catch` block for handling
* once an exception is handled it does not return to the throw point, it instead exits the `try catch` block and continues execution
* if there is a `finally` block it will enter it
* `try` block refers the the block of code `{ }` after the `try` keyword
* `try` statement refers to all the code including the `try` block, any or all `catch` blocks and the `finally` block (if there is one)

## .NET Exception Hierarchy ##

### Class `SystemException` ###

* Class `Exception` (namespace `System`) is the base class of .NET's exception class hierarchy
* `SystemException` is a derived class of `Exception`
* The CLR generates `SystemException`s 
* Some derived classes of `SystemException`:
  * `IndexOutOfRangeException`
  * `NullReferenceException`
  * `DivideByZeroException`

### Common Programming Error 13.2 ###

The compiler issues an error if a catch block that catches a base-class exception is placed before a catch block for any of that class’s derived-class types. In this case, the base-class catch block would catch all base-class and derived-class exceptions, so the derived-class exception handler would never execute.

>Connected Concepts: Because of the `Exception` class hierarchy you can choose to catch general exceptions or more specific exceptions. This is thanks to inheritance and polymorphism.

### Software Engineering Observation 13.1 ###

If a method may throw exceptions, statements that invoke the method directly or indirectly should be placed in try blocks, and those exceptions should be caught and handled.

## Finally Block ##

* Used for "clean up" after a `try` block
* Programs that request and release resources at execution time should use `finally` blocks to release those resources
  * resources like: Files and Streams
* All resource-release code should be put in the `finally` block
* Three situations that cause the `finally` block to execute:
    1. The `try` block executed without exception
    2. The `try` block throws an exception that is caught in a `catch` block and handled
    3. The `try` block throws and uncaught exception

### Error-Prevention Tip 13.4 ###

When placing code that can throw an exception in a finally block, always enclose the code in a try statement that catches the appropriate exception types. This prevents the loss of any uncaught and rethrown exceptions that occur before the finally block executes.

### Software Engineering Observation 13.3 ###

Do not place try blocks around every statement that might throw an exception—this can make programs difficult to read. Instead, place one try block around a significant portion of code, and follow this try block with catch blocks that handle each possible exception. Then follow the catch blocks with a single finally block. Use separate try blocks to distinguish between multiple statements that can throw the same exception type.


## The `using` Statement ##

* not to be confused with `using` directive (importing namespaces)
* simplifies code that obtains a resource
* The resource must be an object that implements `IDisposable`

```[C#]
using (var exampleObject = new ExampleClass())
{
   exampleObject.SomeMethod(); // do something with exampleObject
}
```

**VS**

```[C#]
{
    var exampleObject = new ExampleClass();
    try
    {
        exampleObject.SomeMethod();
    }
    finally
    {
        if (exampleObject != null)
        {
            exampleObject.Dispose();
        }
    }
}
```



## Exception Properties ##

* `StackTrace` - string that represents the method-call stack
* `Message` - stores the string error message associated with an `Exception` object
* `InnerException` - If you are catching an exception that occurred in a library you can get the exception that caused the thrown exception.
* `HelpLink` - link to a help file
* `Source` - name of the assembly (app or library) that caused the exception
* `TargetSite` - Specifies the method where the exception originated

## User-Defined Exception Classes ##

* Should derive indirectly or directly from `Exception`

###  Good Programming Practice 13.1 ###

Associating each type of malfunction with an appropriately named exception class improves program clarity.

### Software Engineering Observation 13.4 ###

Before creating a user-defined exception class, investigate the existing exceptions in the .NET Framework Class Library to determine whether an appropriate exception type already exists.

## Checking for null References ##

### Null-Conditional Operator (`?.`) ###

```[C#]
if (exampleObject != null)
{
    exampleObject.Dispose();
}
```

VS

```[C#]
exampleObject?.Dispose();
```

* must be used on a nullable type
* nullable types are denoted with `?`
* ie `decimal? salary = employee?.BaseSalary;`

### Null Coalescing Operator (`??`) ###

```[C#]
decimal salary = employee?.BaseSalary ?? 0M;
```

if employee is not null, salary is assignment the employee's `BaseSalary` otherwise `salary` is assigned `0M`

## Exception Filters - `when` Clause ##

* allows for different `catch` blocks for the same exception type just with different conditions

```[C#]
catch(ExceptionType name) when(condition)
```