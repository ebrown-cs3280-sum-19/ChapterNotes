# Chapter 6 - Control Structures Part 2 #

## Counter-Controlled Iteration ##

Elements of counter-controlled iteration:

1. a control variable
2. the control variable's initial value
3. the control variables increment value
4. the loop-continuation condition that determines if looping should continue.

### `while` Iteration With Counter ###

```[C#]
// Counter-controlled iteration with the while iteration statement.

int counter = 1; // declare and initialize control variable

while (counter <= 10) // loop-continuation condition
{
    Console.Write($"{counter} ");
    ++counter; // increment control variable
}

Console.WriteLine();
```

### `for` Iteration Statement ###

* typically `for` loops are used for counter-controlled iteration
* `while` loops are used for sentinel-controlled iteration
* Both however can be used for either iteration type

```[C#]
// for statement header includes initialization,
// loop-continuation condition and increment
for (int counter = 1; counter <= 10; ++counter)
{
    Console.Write($"{counter} ");
}

Console.WriteLine();
```

General Format of a `for` Statement

```[C#]
for (initialization; loopContinuationCondition; increment)
{
  statement
}
```

* All three expressions in a `for` header are optional
* If the `loopContinuationCodition` is omitted C# assumes it's alway true
* you can obit the `initialization` expression if the app initializes the control variable before the loop
* you can omit the `increment` expression if the app calulates the increment with statements in the loop's body or if no increment is needed

## `do..while` Iteration Statement ##

* similar to the `while` statement but the continuation condition executes after the loop's body executes
* the body always executes at least once
* good for looping for user input

```[C#]
int counter = 1; // initialize counter

do
{
    Console.Write($"{counter}   ");
    ++counter;
} while (counter <= 10); // required semicolon

Console.WriteLine();
 ```

## `switch` Multiple-Selection Satement ##

Letter Grades Example Switch Statement

```[C#]
do
{
    input = Console.ReadLine()
    int grade = int.Parse(input); // read grade off user input
    total += grade; // add grade to total
    ++gradeCounter;
    switch (grade / 10)
    {
        case 9: // grade was in the 90s
        case 10: // grade was 100
            ++aCount; // increment aCount
            break; // necessary to exit switch
        case 8: // grade was between 80 and 89
            ++bCount; // increment bCount
            break; // exit switch
        case 7: // grade was between 70 and 79
            ++cCount; // increment cCount
            break; // exit switch
        case 6: // grade was between 60 and 69
            ++dCount; // increment dCount
            break; // exit switch
        default: // grade was less than 60
            ++fCount; // increment fCount
            break; // exit switch
    }
} while (input != null);

double average = (double) total / gradeCounter;
```

## `break` and `continue` Statements ##

### `break` Statement ###

## Logical Operators ##

## Structured-Programming Summary ##