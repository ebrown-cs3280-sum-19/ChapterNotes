# Chapter 10 - Classes and Objects: A Deeper Look #

## `class` Observations ##

### Software Engineering Observation 10.1 ###

Classes simplify programming because the client can use only the public members exposed by the class.
Such members are usually client oriented rather than implementation oriented.
Clients are neither aware of, nor involved in, a class’s implementation.
Clients generally care about what the class does but not how the class does it.
Clients do, of course, care that the class operates correctly and efficientl

### Software Engineering Observation 10.2 ###

Interfaces change less frequently than implementations. When an implementation changes, implementation-dependent code must change accordingly.
Hiding the implementation reduces the possibility that other parts of the app become dependent on class-implementation details.

## Controlling Access to Members ##

* access modifiers `public` and `private`
* control access to class's variables, methods and properties
* `public` purpose is to present the class's clients a view of services
* Clients of the class need not be concerned with how the class accomplishes its tasks
* `private` variables, properties and methods are not accessible to the class's clients

## `this` Reference ##

* Objects access a *reference* to itself with `this`
* when a non-`static` method or property is called for an object the method's body *implicitly* uses `this`
* you may use `this` explicitly if you prefer

### Shadowing ###

If a method contains a local variable with the same name as an instance variable, the local variable is said to shadow (or hide) the instance variable in the method’s body

``` [C#]
public SimpleTime(int hour, int minute, int second)
{
    this.hour = hour;
    this.minute = minute;
    this.second = second;
}
```

### Software Engineering Observation 10.4 ###


Using properties throughout a class to access the class’s instance variables normally eliminates shadowing because property names use Pascal Case naming (capital first letter) and parameter names use Camel Case (lowercase first letter).

## Overloaded Constructors ##

```[C#]
1    // Fig. 10.5: Time2.cs
 2    // Time2 class declaration with overloaded constructors.
 3    using System; // for class ArgumentOutOfRangeException
 4
 5    public class Time2
 6    {
 7       private int hour; // 0 - 23
 8       private int minute; // 0 - 59
 9       private int second; // 0 - 59
10
11       // constructor can be called with zero, one, two or three arguments. Default parameters
12       public Time2(int hour = 0, int minute = 0, int second = 0)
13       {
14          SetTime(hour, minute, second); // invoke SetTime to validate time
15       }
16
17        // Time2 constructor: another Time2 object supplied as an argument. Constructor Initializer
18       public Time2(Time2 time)
19               this(time.Hour, time.Minute, time.Second) { }
20
21        // set a new time value using universal time; invalid values
22        // cause the properties' set accessors to throw exceptions
23       public void SetTime(int hour, int minute, int second)
24       {
25          Hour = hour; // set the Hour property
26          Minute = minute; // set the Minute property
27          Second = second; // set the Second property
28       }
29
30       // property that gets and sets the hour
31       public int Hour
32       {
33          get
34          {
35             return hour;
36          }
37          set
38          {
39              if (value < 0 || value > 23)
40              {
41                 throw new ArgumentOutOfRangeException(nameof(value),
42                    value, $"{nameof(Hour)} must be 0-23");
43              }
44
45              hour = value;
46           }
47      }
48
49       // property that gets and sets the minute
50       public int Minute
51      {
52          get
53         {
54          return minute;
55          }
56          set
57          {
58            if (value < 0 || value > 59)
59            {
60              throw new ArgumentOutOfRangeException(nameof(value),
61                 value, $"{nameof(Minute)} must be 0-59");
62            }
63
64              minute = value;
65         }
66       }
67
68       // property that gets and sets the second
69       public int Second
70       {
71          get
72          {
73             return second;
74          }
75          set
76          {
77             if (value < 0 || value > 59)
78             {
79                throw new ArgumentOutOfRangeException(nameof(value),
80                   value, $"{nameof(Second)} must be 0-59");
81             }
82
83             second = value;
84           }
85         }
86
87          // convert to string in universal-time format (HH:MM:SS)
88          public string ToUniversalString() =>
89             $"{Hour:D2}:{Minute:D2}:{Second:D2}";
90
91           // convert to string in standard-time format (H:MM:SS AM or PM)
92          public override string ToString() =>
93             $"{((Hour == 0 || Hour == 12) ? 12 : Hour % 12)}:" +
94             $"{Minute:D2} : {Second:D2}{(Hour < 12 ? "AM" : "PM")}";
95       }
```

### Good Programming Practice 10.1 ###

When you need to include an identifier in a string literal, use the nameof operator rather than hard coding the identifier’s name in the string.
If you right click an identifier in Visual Studio then use the Rename… option to change the identifier’s name throughout your code, the string that nameof returns will be updated automatically with the identifier’s new name.

## Composition ##



