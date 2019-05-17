# Chapter 16 - Strings and Characters #

## Fundamentals of Characters and Strings ##

### Characters ###

* Fundamental building blocks of C# source code
* When grouped together meaningfully create a instructions that the compiler understands
* character constant is a character that's represented as an integer value (*character code*)
* ie. `122` is 'z' and `10` is '\n'
* These codes are part of **Unicode**


### Strings ###

* A series of characters
* upper/lowercase letters, digits and special characters
* is an object of type `string`
* `string` is and alias for class `String` like `object` is an alias for class `Object` 
* **String literals** also called **string constants** as sequences of characters in double quotations marks

``` [C#]
// string color refers to the string literal object "blue"
string color = "blue";
```

Multiple copies of a string literal object in an app are stored as a single copy. So `string color = "blue";` and `string eyes = "blue"` actual point to the same place in memory. This conserves memory.

### Verbatim Strings ###

* `@` charcter denotes a verbatim string
* you don't need to escape characters in a verbatim string

```[C#]
string file = "C:\\MyFolder\\MySubFolder\\MyFile.txt";
// to
string file = @"C:\MyFolder\MySubFolder\MyFile.txt";
```

## `string` Constructors Examples ##

```[C#]
 1   // Fig. 16.1: StringConstructor.cs
 2   // Demonstrating string class constructors.
 3   using System;
 4
 5   class StringConstructor
 6   {
 7      static void Main()
 8      {
 9         // string initialization
10         char[] characterArray =
11            {'b', 'i', 'r', 't', 'h', ' ', 'd', 'a', 'y'};
12         var originalString = "Welcome to C# programming!";
13         var string1 = originalString;
14         var string2 = new string(characterArray);      
15         var string3 = new string(characterArray, 6, 3);
16         var string4 = new string('C', 5);              
17
18         Console.WriteLine($"string1 = \"{string1}\"\n" +
19            $"string2 = \"{string2}\"\n" +
20            $"string3 = \"{string3}\"\n" +
21            $"string4 = \"{string4}\"\n");
22      }
23   }
```

output

```[output]
string1 = "Welcome to C# programming!"
string2 = "birth day"
string3 = "day"
string4 = "CCCCC"
```

In most cases, it’s not necessary to make a copy of an existing string. All string s are immutable—their character contents cannot be changed after they’re created. Also, if there are one or more references to a string (or any reference-type object for that matter), the object cannot be reclaimed by the garbage collector.

## `string` Indexer, Length Property and CopyTo Method ##

* the `string` indexer (`[]`) for retrieving any character in a `string`,
* the `string` property `Length`, which returns a `string`’s length and
* the `string` method `CopyTo`, which copies a specified number of characters from a `string` into a `char` array.

```[C#]
 1   // Fig. 16.2: StringMethods.cs
 2   // Using the indexer, property Length and method CopyTo
 3   // of class string.
 4   using System;
 5
 6   class StringMethods
 7   {
 8      static void Main()
 9      {
10         var string1 = "hello there";
11         var characterArray = new char[5];
12
13         Console.WriteLine($"string1: \"{string1}\""); // output string1
14
15         // test Length property
16         Console.WriteLine($"Length of string1: {string1.Length}");
17
18         // loop through characters in string1 and display reversed
19         Console.Write("The string reversed is: ");
20
21         for (int i = string1.Length - 1; i >= 0; --i)
22         {
23            Console.Write(string1[i]);
24         }
25
26         // copy characters from string1 into characterArray
27         string1.CopyTo(0, characterArray, 0, characterArray.Length);
28         Console.Write("\nThe character array is: ");
29
30         foreach (var element in characterArray)
31         {
32            Console.Write(element);
33         }
34
35         Console.WriteLine("\n");
36      }
37   }
```

output

```[output]
string1: "hello there"
Length of string1: 11
The string reversed is: ereht olleh
The character array is: hello
```

lines 21-24 above could be changed to use the `string.Reverse()` method.

```[C#]
foreach (var element in string1.Reverse())
{
    Console.Write(element);
}
```

