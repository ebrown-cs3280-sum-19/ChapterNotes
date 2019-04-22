# Chapter 4 - Introduction Classes, Objects, Methods and strings #

## Class Review ##

* Each user defined class becomes a new `type` you can use to create objects
* This makes C# an **extensible programming language**
* Classes are encapsulated code segments consisting of data (properties) and behaviors (methods)

## `AccountDriver` Class ##

* We are going to create an `Account` class
* First we need a class to "drive" the `Account` class
* This driver class we'll use to instantiate the `Account` and try out it's functionality
* We'll also create a MS Test class to test the `Account`
  
### The Code ###

```[c#]
using System;

class AccountDriver
{
    static void Main()
    {
        // create an Account object and assign it to myAccount
        Account myAccount = new Account();

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

## The Account Class ##


### C# Getter and Setter Styles ###

Java style Getter and Setters:

```[c#]
class Account
{
    private string name;

    public string GetName()
    {
        return name;
    }

    public void SetName()
    {
        name = value;
    }
}
```

C# Getter and Setter:

```[c#]
class Account
{
    private string name;

    public string Name 
    { 
        get
        {
            return name;
        }
        set
        {
            name = value;
        }
    }
}
```

Syntactic Sugar:

```[c#]
class Account
{
    public string Name { get; set; }
}
```

All of the above getter and setter styles are valid in C#

### AccountTest Class ###

* Visual Studio has a testing framework built in called MS Test
* Since it's integrated into VS code it's very easy to get up and running
* There are other C# frameworks like NUnit and xUnit
* We'll use MS Test in this class but NUnit and xUnit are great frameworks especially if you are using .net core

```[c#]
class AccountTest
{
    
}
```