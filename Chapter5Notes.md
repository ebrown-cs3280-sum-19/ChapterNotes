# Chapter 5 - Control Structures Part 1 #

## Problem Solving ##

### Algorithms ###

* Any computing problem can be solved by executing a series of **actions** in a specific **order**
* These actions in a specific order is called an algorithm

### Pseudocode ###

* informal language that helps you develop algorithms without worrying about syntax
* psuedocode isn't a formal language and you can define your own
* come up with whatever style helps you but try to be consistent
* you can use plain language or something that is closer to code

plain-English psudocode (no variable assignments)

```[psuedocode]
Prompt user for integer
Input the first integer

prompt the user for integer
Input the second integer

Add first integer and second integer
Display result
```

more "code-like" psudocode

```[psudocode]
integer1 = user input
integer2 = user input
result = integer1 + integer2
display result
```

## Control Statements ##

### Structural Programming ###

* in the 60s it was common to use `goto` statement
* ths cause a logt of difficulty among software developers
* a `goto` could transfer control almost anywhere in the code
* Bohm and Jacopini research showed that they could write code without `goto` statements
* this discipline of not using `goto` statements is called *structured programming*
* this sped up development times and kept budgets
* they also showed that you could write all programs with only 3 types of control structures

### Sequence Structure ###

Basic structure where each statement is executed one after the other in the order they are written.

### Selection Structures ###

* 3 different types of selection statements
* `if` statement performs the action if a condition is true
* `if` `else` performs an action if a condition is true or performs a different action if it's false
* `switch` statement performs one of many different actions depending on the value of an expression 
  * side note: these as well as big if else trees should be avoided higher level code

### Iteration Structures ###

* sometimes called repetition statements or looping statements
* `for`, `while` `do...while` and `foreach` statements
* loop statements have a body that will execute if their loop continuation condition is true

## Selection Statements ##

### If Single-Selection Statement ###

Psudocode if statement

```[psudocode]
If student’s grade is greater than or equal to 60
    Display “Passed”
```

c# if statement

```[C#]
if (studentGrade >= 60)
{
    Console.WriteLine("Passed");
}
```

### `if...else` Double-Selection Statement ###

Psudocode if...else statement

```[psudocode]
If student's grade is greater than or equal to 60
      Display "Passed"
Else
      Display "Failed"
```

C# if...else statement

```[C#]
if (grade >= 60)
{
   Console.WriteLine("Passed");
}
else
{
   Console.WriteLine("Failed");
}
```

## Iteration Statements ##

### `while` iteration statement ###

Psudocode while loop

```[psudocode]
While there are more items on my shopping list
    Purchase next item and cross it off my list
```

C# while loop

```[C#]
int product = 3;
while (product <= 100)
{
    product = 3 * product;
}
```

More on iteration statements in chapter 6

## Assignments ##

### Conditional Operator ###

* `?:` can be used in place of an `if..else` statement
* c#'s only ternary operator
* takes 3 operands
* `bool-expression ? true-value : false-value`

```[C#]
Console.WriteLine(studentGrade >= 60 ? "Passed" : "Failed");
```

### Compound Assignment Operators ###

Abbreviate assignment operations like this:

`variable = variable operator expression;`

to

`variable operator= expression;`

for example:

`c = c + 3;`

using the compound assignment operator

`c += 3`

The `+=` adds the value of the expression on its right to the variable on it's left and stores it in the variable on the left

other compound assignment operators:

* `+=`
* `-=`
* `*=`
* `/=`
* `%=`
