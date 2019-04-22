# Chapter 4 - Introduction Classes, Objects, Methods and strings #

## Class Review ##

* Each user defined class becomes a new `type` you can use to create objects
* This makes C# an **extensible programming language**
* Classes are encapsulated code segmants consisting of data (properties) and behaviors (methods)

## `AccountTest` Class ##

* We are going to create an `Account` class
* First we need a class to "drive" the `Account` class
* We'll use this test class to test the behavior and properties of the `Account` class
  
### The Code ###

```[c#]
using System;

class AccountTest
{
    static void Main()
    {
        // create an Account object and assign it to myAccount
        Account myAccount = new Accoutn();

        // display myAccount's initial name (there isn't one yet);
        Console.WriteLine($"Initial name is: {myAccount.GetName()}");

        // prompt for and read the name then put the name in the object
        Console.Write("Enter the name: "); // prompt
        string theName = Console.ReadLine(); // read the name
        myAccount.SetName(theName); // put theName in the myAccount object

        // display the name stored in the myAccount object
        Console.WriteLine($"myAccount's name is: {myAccount.GetName()}");
    }
}
```

Example Output:

```[output]
Initial name is:
Enter the name: Jane Green
myAccount's name is: Jane Green
```
