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

>NOTE: In most cases, it’s not necessary to make a copy of an existing `string`. All `string`s are immutable—their character contents cannot be changed after they’re created. Also, if there are one or more references to a `string` (or any reference-type object for that matter), the object cannot be reclaimed by the garbage collector.

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

## Comparing `sting`s ##

### Comparing `string`s with `Equals`, `CompareTo` and the Equality Operator (`==`) ###

```[C#]
 1   // Fig. 16.3: StringCompare.cs
 2   // Comparing strings
 3   using System;
 4
 5   class StringCompare
 6   {
 7      static void Main()
 8      {
 9         var string1 = "hello";
10         var string2 = "good bye";
11         var string3 = "Happy Birthday";
12         var string4 = "happy birthday";
13
14         // output values of four strings
15         Console.WriteLine($"string1 = \"{string1}\"" +
16            $"\nstring2 = \"{string2}\"" +
17            $"\nstring3 = \"{string3}\"" +
18            $"\nstring4 = \"{string4}\"\n");
19
20          // test for equality using Equals method
21          if (string1.Equals("hello"))
22          {
23             Console.WriteLine("string1 equals \"hello\"");
24          }
25          else
26          {
27             Console.WriteLine("string1 does not equal \"hello\"");
28          }
29
30          // test for equality with ==
31          if (string1 == "hello")
32          {
33             Console.WriteLine("string1 equals \"hello\"");
34          }
35          else
36          {
37             Console.WriteLine("string1 does not equal \"hello\"");
38          }
39
40          // test for equality comparing case
41          if (string.Equals(string3, string4)) // static method
42          {
43              Console.WriteLine("string3 equals string4");
44          }
45          else
46          {
47              Console.WriteLine("string3 does not equal string4");
48          }
49
50          // test CompareTo
51          Console.WriteLine(
52             $"\nstring1.CompareTo(string2) is {string1.CompareTo(string2)}");
53          Console.WriteLine(
54             $"string2.CompareTo(string1) is {string2.CompareTo(string1)}");
55          Console.WriteLine(
56             $"string1.CompareTo(string1) is {string1.CompareTo(string1)}");
57          Console.WriteLine(
58             $"string3.CompareTo(string4) is {string3.CompareTo(string4)}");
59          Console.WriteLine(
60             $"string4.CompareTo(string3) is {string4.CompareTo(string3)}");
61         }
62    }
```

Output

```[output]
string1 = "hello"
string2 = "good bye"
string3 = "Happy Birthday"
string4 = "happy birthday"

string1 equals "hello"
string1 equals "hello"
string3 does not equal string4

string1.CompareTo(string2) is 1
string2.CompareTo(string1) is -1
string1.CompareTo(string1) is 0
string3.CompareTo(string4) is 1
string4.CompareTo(string3) is -1
```

### `Equals` method ###

* `Equals` method is inherited from `object` and overridden in `string`
* Tests that two strings have *identical contents*
* is case sensitive
* `==` Equality Operator in c# also compares the *contents* of the two strings

### `CompareTo` method ###

* returns `0` if the strings are equal
* returns `1` if the `string` that invokes `CompareTo` is *greater* than the `string` arugment
* returns `-1` if the `string` that invokes `CompareTo` is *less* than the `string` arugment
* upper case is consider greater than lower

### `StartsWith` and `EndsWith` methods ###

* `name.StartsWith("Lu")` Returns `true` if `name` starts with `"Lu"`
* `name.EndsWith("cy")` Returns `true` if `name` ends with `"cy"`

## Locating Characters and Substrings in `string`s ##

* `string.IndexOf('c', 1, 4)` returns first index of c in `string` from index `1` to `1` + `4`
* `string.LastIndexOf('c', 7, 3)` returns last index of c in `string` from index `7` to index `7` - `3` (going in reverse)
* `string.IndexOfAny(charArray, 1, 4)` returns first index of any `char` in `charArray` in `string` from index `1` to index `1` + `4`
* `string.LastIndexOfAny(charArray, 7, 3)` returns first index of any `char` in `charArray` in `string` from index `7` to index `7` - `3` (going in reverse)

## Extracting Substrings from `string`s ##

* `letters.Subscrting(20)` returns a string of the `letters` from index `20` to the end of `letters`
* `letters.Subscrting(1, 4)` returns a string of the `letters` from index `1` to index `1` + `4`

## Miscellaneouse `string` methods ##

* `string.Replace('e', 'E')` returns string with all `"e"`s replaced with `"E"`s
* `string.ToUpper()` returns string with all letters uppercase
* `string.ToLower()` returns string with all letters lowercase
* `string.Trim()` returns string with all trailing and leading whitespace removed

## `StringBuilder` Class ##

* mutable string
* in the `System.Text` namespace
* has a capacity that when filled will cause it to expand
* can be used for *concatenation* without creating new `string` objects
* more effecient when manipulating a large number of `string`s than using immutable `string`s

Various Constructors for `StringBuilder`

```[C#]
var buffer1 = new StringBuilder();
var buffer2 = new StringBuilder(10);
var buffer3 = new StringBuilder("hello");
```

### `StringBuilder` Methods and Properties ###

* `Length` contains the current length of the SB
* `Capacity` contains the max capacity of the SB before needing to resize
* `EnsureCapacity(int)` will size the SB to the given int
* `Append(string)` will append a `string` or a `char` to the end of the SB
* `AppendFormat(string, objectArray`) will append a `string` and uses the array of `object`s as arguments for to format the `string`

### Other `StringBuilder` Methods ###

* `Insert()`
* `Remove()`
* `Replace()`

## `char`  Methods ###

* `char.IsDigit(character)`
* `char.IsLetter(character)`
* `char.IsLower(character)`
* `char.IsUpper(character)`
* `char.IsPunctuation(character)`
* `char.IsSymbol(character)`

## Introduction to Regex ##

* `System.Text.RegularExpressions` namespace
* `Regex rx = new Regex(<pattern>);`
* `rx.IsMatch(string);` returns `bool` if the `string` and `rx` is a match
* `MatchCollection matches = rx.Matches(string);` returns a collection of matches for rx in `string`