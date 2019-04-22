# Chapter 3 - Intro To C# #

## Basic C# ##

### Comments ###

* comments can help with readability and documentation
* compiler ignores comments
* single-line comments begin with //
* multi-line comments begin with /* and end with */
* xml comments /// show up in intelisense for * methods, classes and functions
  
### `using` directive ###

* allows the compiler to find types used in project
* like import statements in java, javascript and python
* this allows you to reuse your own code as well as code created by mircrosoft and others
* C#'s predefined namespaces are refferred to as the .NET Framework Class Library (FCL)

## Classes ##

### Class Declaration ###

* the class keyword begins a class declaration
* every app contains at least one class declaration defined by you
* these are known as user-defined classes

### Class Name Convention ###

* all class names begin with a capital letter and capitals for the first letter of each word after
* e.g., SampleClassName
* Known as Pascal Case
* must start with letter or `_`
* only contains letters, digits and `_`
* C# is case sensitive
* The class declaration's file is the same name as the class with `.cs` extension

### Class Body ###

* class body is between curly braces { }
* the body can contain variables and methods
* the variables and methods declared in the class are called class members
* the class members can have different access levels: private, public, protected
* more on this next chapter

## Creating a Console App in Visual Studio ##

### New Project ###

1. Open Visual Studio
2. **File** > **New** > **Project**
3. **Installed** > **Templates** > **Visual C#** select **Consople Application**
4. Fill in the name and select the location you want to save the project and click ok

Visual Studio will then create the project folder and all the files you need

### Main Method ###

* static void Main()
* entry point for app execution
* you must have a Main method or it won't execute

### Displaying Text ###

* Console.WriteLine("welcome to C# programming");
* Console is static class from the System namespace
* It can write a string
* Console.WriteLine() writes the string on a new line
* Console.Write writes the string on the current line

## Strings ##

### Escape Sequences ###

* strings are a sequence of characters between double quotes "
* they support escape sequences for special characters
  * \n - newline
  * \t - tab
  * \" - double quote
  * \r - carriage return
  * \\ - backlash

### String Interpolation ###

very nice feature that allows placing varialbes within a string without concatenation or formatting

```[c#]
string person = "Bruce";
Console.WriteLine($"Welcome to C# programming, {person}!")
```

the $ indicates a string for interpolation. Inside the string the `{ }` indicates a variable that's value needs to be inserted
