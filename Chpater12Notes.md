# Chapter 12 - OOP: Polymorphism and Interfaces #

## Introduction ##

* Polymorphism enables us to program in the general rather than in the specific
* enables us to write apps that process objects that share the *same* base class
* You can send the same "message" to many different objects and each one will respond appropriately based on their implementation
* allows systems to be designed that are easily *extensible*
* Adding another sub class is simple, all the portions that process the base class remain the same

## Polymorphism Example ##

### **Quadrilateral** Inheritance Hierarchy ###

* if claa `Rectangle` is derived from a class `Quadrilateral` then `Rectangle` *is a* specific version of `Quadrilateral`
* Any operation (e.g., calculating perimeter or area) that can be performed on `Quadrilateral` also can be performed on `Rectangle`
* **Polymorphism** occurs when a program invokes a method through a base-class variable--at execution time
* the correct derived-class version of the class method is called, based on the type of the referenced object

### Software Engineering Observation 12.1 ###

Polymorphism promotes extensibility: Software that invokes polymorphic behavior is independent of the object types to which messages are sent.
New object types that can respond to existing method calls can be incorporated into a system without requiring modification of the polymorphic system logic.
Only client code that instantiates new objects must be modified to accommodate new types.

## Demonstrating Polymorphic Behavior ##

```[c#]
1   // Fig. 12.1: PolymorphismTest.cs
  2   // Assigning base-class and derived-class references to base-class and
  3   // derived-class variables.
  4   using System;
  5
  6   class PolymorphismTest
  7   {
  8     static void Main()
  9     {
 10        // assign base-class reference to base-class variable 
 11        var commissionEmployee = new CommissionEmployee(   
 12           "Sue", "Jones", "222-22-2222", 10000.00M, .06M);
 13  
 14        // assign derived-class reference to derived-class variable 
 15        var basePlusCommissionEmployee = new BasePlusCommissionEmployee(
 16           "Bob", "Lewis", "333-33-3333", 5000.00M, .04M, 300.00M);     
 17  
 18        // invoke ToString and Earnings on base-class object
 19        // using base-class variable 
 20        Console.WriteLine(
 21           "Call CommissionEmployee's ToString and Earnings methods " +
 22           "with base-class reference to base class object\n");
 23        Console.WriteLine(commissionEmployee.ToString());
 24        Console.WriteLine($"earnings: {commissionEmployee.Earnings()}\n");
 25  
 26        // invoke ToString and Earnings on derived-class object
 27        // using derived-class variable
 28        Console.WriteLine("Call BasePlusCommissionEmployee's ToString and" +
 29          " Earnings methods with derived class reference to" +
 30          " derived-class object\n");
 31        Console.WriteLine(basePlusCommissionEmployee.ToString());
 32        Console.WriteLine(
 33           $"earnings: {basePlusCommissionEmployee.Earnings()}\n");
 34  
 35        // invoke ToString and Earnings on derived-class object
 36        // using base-class variable 
 37        CommissionEmployee commissionEmployee2 = basePlusCommissionEmployee;
 38        Console.WriteLine(
 39           "Call BasePlusCommissionEmployee's ToString and Earnings " +
 40           "methods with base class reference to derived-class object");
 41        Console.WriteLine(commissionEmployee2.ToString());
 42        Console.WriteLine(
 43           $"earnings: {basePlusCommissionEmployee.Earnings()}\n");
 44     }
 45   }
```

Output

```[output]
Call CommissionEmployee's ToString and Earnings methods with base class
reference to base class object:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: $10,000.00
commission rate: 0.06
earnings: $600.00

Call BasePlusCommissionEmployee's ToString and Earnings methods with derived
class reference to derived class object:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
earnings: $500.00

Call BasePlusCommissionEmployee's ToString and Earnings methods with base
class reference to derived class object:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
earnings: $500.00
```

### Software Engineering Observation 12.3 ###

A base-class variable that contains a reference to a derived-class object and is used to call a virtual method actually calls the overriding derived-class version of the method

## Abstract Classes and Methods ##

* When we think of a class type, we assume that apps will create objects of that type
* In some cases, however, it’s useful to declare classes for which you never intend to instantiate objects
* These classes are called **abstract classes**
* They're only used as base classes
* They *cannot* be used to instantiate objects, because they are *incomplete*

### Purpose of an Abstract Class ###

* provide a base class from which other classes can inherit to *share a common design*
* common attributes and behviors are shared
* classes that can be used to instantiate objects are called **concrete classes**
* such classes provide implementations of *every* method they declare
* abstract classes are too *general* to create real objects
* We need more to be *specific* before we can create objects

### Client Code That Uses Only Abstract Base-Class Types ###

* You'll often write client code that uses only abstract base-class types to reduce client code dependencies on a range of specific derived-class types
* for example, you can write a method with a parameter of an abstract base-class type, then when called it can be passes an object of any concrete class that extends the abstract base class

### Creating an Abstract Class ###

* You make a class abstract by declaring it with the keyworkd `abstract`
* they normally contain one or more `abstract` methods
  * `public abstract void Draw(); // abstract method`
* *Abstract methods are implicitly virtual and do not provide implementations*
* A class that contains abstract methods must be declared as an abstract class even if it contains some concrete methods
* concrete derived class's must provide concrete implementations of the base class's abstract methods

### Abstract Properties ###

* Properties also can be declared `abstract` or `virtual`, then overridden in derived classes with the `override` keyword
* this allows abstract base class to spcify common properties of its derived classes
* `public abstract PropertyType MyProperty { get; set; }`
* the semicolons after `get` and `set` indicate we provide *no implementations* for the accessors
* Concrete derived classes must provide implementations for *every* accessor declared inthe abstract property

### Constructors and `static` Methods Cannot be `abstract` or `virtual` ###

* Constructors and static methods cannot be declared abstract or virtual.
* Constructors are not inherited, so such a constructor could never be implemented.
* Similarly, derived classes cannot override static methods, so such as static method could never be implemented.

### Common Programming Error 12.2 ###
Failure to implement a base class’s abstract methods and properties in a derived class is a compilation error unless the derived class is also declared abstract.

### Declaring Variables of Abstract Base Class Types ###

* Although we cannot instantiate objects of `abstract` base classes, you can use `abstract` base classes to declare variables
* these varibales can hold references to objects of any concrete classes derived from those `abstract` classes
* Apps typically use such variables to manipulate derived-class objects polymorphically
* You can use `abstract` base-class names to invoke `static` methods declared in those `abstract` base classes

## Case Study: Payroll System Using Polymorphism ##

### Class **Employee** ###

```[C#]
  1   // Fig. 12.4: Employee.cs
  2   // Employee abstract base class. 
  3   public abstract class Employee
  4   {
  5      public string FirstName { get; }
  6      public string LastName { get; }
  7      public string SocialSecurityNumber { get; }
  8  
  9     // three-parameter constructor
 10     public Employee(string firstName, string lastName,
 11       string socialSecurityNumber)
 12     {
 13       FirstName = firstName;
 14       LastName = lastName;
 15       SocialSecurityNumber = socialSecurityNumber;
 16     }
 17    
 18     // return string representation of Employee object, using properties
 19     public override string ToString() => $"{FirstName} {LastName}\n" +
 20        $"social security number: {SocialSecurityNumber}";
 21    
 22     // abstract method overridden by derived classes
 23     public abstract decimal Earnings(); // no implementation here
 24   }
```

### Class **SalariedEmployee** ###

```[C#]
  1   // Fig. 12.5: SalariedEmployee.cs
  2   // SalariedEmployee class that extends Employee.
  3   using System;
  4  
  5   public class SalariedEmployee : Employee
  6   {
  7      private decimal weeklySalary;
  8  
  9      // four-parameter constructor
 10      public SalariedEmployee(string firstName, string lastName,
 11         string socialSecurityNumber, decimal weeklySalary)
 12         : base(firstName, lastName, socialSecurityNumber)
 13      {
 14         WeeklySalary = weeklySalary; // validate salary
 15      }
 16  
 17      // property that gets and sets salaried employee's salary
 18      public decimal WeeklySalary
 19      {
 20          get
 21          {
 22              return weeklySalary;
 23          }
 24          set
 25          {
 26             if (value < 0) // validation
 27             {
 28                 throw new ArgumentOutOfRangeException(nameof(value),
 29                     value, $"{nameof(WeeklySalary)} must be >= 0");
 30             }
 31  
 32             weeklySalary = value;
 33          }
 34      }
 35  
 36      // calculate earnings; override abstract method Earnings in Employee 
 37      public override decimal Earnings() => WeeklySalary;
 38  
 39      // return string representation of SalariedEmployee object
 40      public override string ToString() =>
 41      $"salaried employee: {base.ToString()}\n" +
 42      $"weekly salary: {WeeklySalary:C}";
 43   }
```

### Class **HourlyEmployee** ###

```[C#]
  1   // Fig. 12.6: HourlyEmployee.cs
  2   // HourlyEmployee class that extends Employee.
  3   using System;
  4  
  5   public class HourlyEmployee : Employee
  6   {
  7      private decimal wage; // wage per hour
  8      private decimal hours; // hours worked for the week
  9  
 10      // five-parameter constructor
 11      public HourlyEmployee(string firstName, string lastName,
 12         string socialSecurityNumber, decimal hourlyWage,
 13         decimal hoursWorked)
 14         : base(firstName, lastName, socialSecurityNumber)
 15      {
 16         Wage = hourlyWage; // validate hourly wage
 17         Hours = hoursWorked; // validate hours worked
 18      }
 19  
 20      // property that gets and sets hourly employee's wage
 21      public decimal Wage
 22      {
 23          get
 24          {
 25              return wage;
 26          }
 27          set
 28          {
 29              if (value < 0) // validation
 30              {
 31                  throw new ArgumentOutOfRangeException(nameof(value),
 32                     value, $"{nameof(Wage)} must be >= 0");
 33              }
 34  
  3              wage = value;
 36          }
 37      }
 38  
 39      // property that gets and sets hourly employee's hours
 40      public decimal Hours
 41      {
 42         get
 43         {
 44            return hours;
 45         }
 46         set
 47         {
 48            if (value < 0 || value > 168) // validation
 49            {
 50               throw new ArgumentOutOfRangeException(nameof(value),
 51                  value, $"{nameof(Hours)} must be >= 0 and <= 168");
 52            }
 53  
 54            hours = value;
 55      }
 56    }
 57  
 58    // calculate earnings; override Employee’s abstract method Earnings 
 59    public override decimal Earnings()
 60    {
 61       if (Hours <= 40) // no overtime
 62       {
 63           return Wage * Hours;
 64       }
 65       else
 66       {
 67          return (40 * Wage) + ((Hours - 40) * Wage * 1.5M);
 68       }
 69     }
 70  
 71     // return string representation of HourlyEmployee object 
 72     public override string ToString() =>
 73        $"hourly employee: {base.ToString()}\n" +
 74        $"hourly wage: {Wage:C}\nhours worked: {Hours:F2}";
 75   }
```

### Polymorphic Processing, Operator *is* and Downcasting ###

There are 4 concrete classes in this processor, including 2 from above and 2 others.
The app manipulates these objects using a `List` of `Employee` variables

```[C#]
1   // Fig. 12.9: PayrollSystemTest.cs
  2   // Employee hierarchy test app.
  3   using System;
  4   using System.Collections.Generic;
  5  
  6   class PayrollSystemTest
  7   {
  8      static void Main()
  9      {
 10         // create derived-class objects 
 11         var salariedEmployee = new SalariedEmployee("John", "Smith",   
 12             "111-11-1111", 800.00M);                                   
 13         var hourlyEmployee = new HourlyEmployee("Karen", "Price",      
 14             "222-22-2222", 16.75M, 40.0M);                             
 15         var commissionEmployee = new CommissionEmployee("Sue", "Jones",
 16             "333-33-3333", 10000.00M, .06M);                           
 17         var basePlusCommissionEmployee =                               
 18            new BasePlusCommissionEmployee("Bob", "Lewis",              
 19            "444-44-4444", 5000.00M, .04M, 300.00M);                    
 20  
 21         Console.WriteLine("Employees processed individually:\n");
 22  
 23         Console.WriteLine($"{salariedEmployee}\nearned: " +
 24            $"{salariedEmployee.Earnings():C}\n");
 25         Console.WriteLine(
 26            $"{hourlyEmployee}\nearned: {hourlyEmployee.Earnings():C}\n");
 27         Console.WriteLine($"{commissionEmployee}\nearned: " +
 28            $"{commissionEmployee.Earnings():C}\n");
 29         Console.WriteLine($"{basePlusCommissionEmployee}\nearned: " +
 30            $"{basePlusCommissionEmployee.Earnings():C}\n");
 31  
 32         // create List<Employee> and initialize with employee objects 
 33         var employees = new List<Employee>() {salariedEmployee,             
 34            hourlyEmployee, commissionEmployee, basePlusCommissionEmployee}; 
 35  
  3         Console.WriteLine("Employees processed polymorphically:\n");
 37  
 38         // generically process each element in employees 
 39         foreach (var currentEmployee in employees)
 40         {
 41             Console.WriteLine(currentEmployee ); // invokes ToString
 42  
 43             // determine whether element is a BasePlusCommissionEmployee
 44             if (currentEmployee is BasePlusCommissionEmployee)
 45             {
 46                // downcast Employee reference to
 47                // BasePlusCommissionEmployee reference 
 48                var employee = (BasePlusCommissionEmployee) currentEmployee;
 49  
 50                employee.BaseSalary *= 1.10M;
 51                Console.WriteLine("new base salary with 10% increase is: " +
 52                   $"{employee.BaseSalary:C}");
 53             }
 54  
 55             Console.WriteLine($"earned: {currentEmployee.Earnings() :C}\n");
 56      }
 57  
  3      // get type name of each object in employees
 59      for (int j = 0; j < employees.Count; j++)
 60      {
 61         Console.WriteLine(
 62            $"Employee {j} is a {employees[j].GetType() }");
 63      }
 64    }
 65   }
```

Output

```[output]
Employees processed individually:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
earned: $800.00

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: $16.75
hours worked: 40.00
earned: $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: $10,000.00
commission rate: 0.06
earned: $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
earned: $500.00


Employees processed polymorphically:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
earned: $800.00
hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: $16.75
hours worked: 40.00
earned: $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: $10,000.00
commission rate: 0.06
earned: $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
new base salary with 10% increase is: $330.00
earned: $530.00

Employee 0 is a SalariedEmployee
Employee 1 is a HourlyEmployee
Employee 2 is a CommissionEmployee
Employee 3 is a BasePlusCommissionEmployee
```

### Common Programming Error 12.3 ###

Assigning a base-class variable to a derived-class variable (without an explicit downcast) is a compilation error

## `sealed` Methods and Classes ##

* Only methods declared `virtual`, `override` or `abstract` can be overridden in derived classes
* A method declared `sealed` in a base class cannot be overridden in a derivded class
* `private` methods are implicitly `sealed` because it's impossible to override them in a derived class
* the derived class can declare a new method with the same signature as the `private` method in the base class
* `static` also are implicitly `sealed`
* `sealed` methods declaration can never change so all derived calsses use the same implementation

## Interfaces ##


* An interface declaration begins with the keyword interface and can contain only
    * abstract methods
    * abstract properties
    * abstract indexers
    * abstract events
* Interface members are *implicitly* declared both `public` and `abstract`

### Good Programming Practice 12.1 ###

By convention, the name of an interface begins with I (e.g., IPayable). This helps distinguish interfaces from classes, improving code readability.

### Good Programming Practice 12.2 ###

When declaring a method in an interface, choose a name that describes the method’s purpose in a general manner, because the method may be implemented by a broad range of unrelated classes.
