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

