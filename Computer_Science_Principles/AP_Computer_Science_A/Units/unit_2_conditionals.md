
# Overview

To be "Turing-complete," a programming language needs to be able to make decisions based on a condition: "if this is true, execute that block of code."

In this section we'll learn how to evaluate boolean expressions, and see how they can be used in a program to execute code conditionally.

Let's get started.

## Overview - Making Decisions; Boolean Expressions

The `if` and `if-else` statements are _the_ way for a program to make a decision: "if something is true, do these things; otherwise, do these other things."

The `if` statement consists of a _condition_ (an expression that evaluates to either `true` or `false`) and an instruction or _body_ of code to be executed in the event that the condition is true.

```java
if ( _Boolean expression_ )
    statement1;
statement2;

if ( _Boolean expression_ )
{
    statement1;
    statement2;
}
statement3;
```

Either way, after the `if` statement is executed, the program's execution proceeds to the instruction following the statement.

Look at these snippets of code from a `BarBouncer` program to see how this works. Note how we've indented the code to indicate that it is the _body_ of the conditional statement that is to be executed. This isn't required by Java's syntax, but it's smart to do, and required by just about anyplace you'll be that uses Java, including this course.

```java
// checking identity cards at the club
// the value of age has already been entered

int ageLimit = 21;
if (age >= ageLimit)
    System.out.println("You can enter the club.");
    
if (age < ageLimit)
    System.out.println("No admittance.");
```

These two sets of statements work fine, but it's more efficient and safer to write them using an `if-else` statement.

## The if-else statement

```java
if ( _Boolean expression_ )
{
    statement1;
    statement2;
}
else
{
    statement3;
    statement4;
}
statement5;
```

So,

```java
int ageLimit = 21;
if (age >= ageLimit)
    System.out.println("You can enter the club.");
else
    System.out.println("No admittance.");
```

Why is this "safer?" There's only a single comparison being made, as opposed to two separate comparisons (`<=` and `>`) that have to be coordinated.

If there's more than a single statement that's going to be executed as the body of an `if` statement, it needs to be enclosed in curly braces `{ }` to make it a code block:

```java
// checking identity cards at the club
// the value of age has already been entered
int ageLimit = 21;
double entranceFee = 0;
if (age >= ageLimit)
{
    entranceFee = 10.00;    // fee to be collected
    System.out.println("You can enter the club.");
}
else
{   
    entranceFee = -1;      // error code indicating no entrance
    System.out.println("No admittance.");
}
```

With this in mind, what's wrong with the following code?

```java
if (age >= ageLimit)
    entranceFee = 10.00;    // fee to be collected
    System.out.println("You can enter the club.");
```

Although it _looks_ like `System.out.println("You can enter the club.");` is part of the code block, it's not—it's just another statement in the program. When this runs, if `age` is less than `ageLimit`, the `entranceFee` will not be set to $10, and the under-age person will be told to enter the club with a fee of $0. That's probably not what we wanted to do.

How _should_ this snippet be written?

To make your code as clean and easy to understand as possible, _always_ use curly braces to enclose code for `if-else` statements, even if each block is only a single line:

```java
int ageLimit = 21;
if (age >= ageLimit)
{
    System.out.println("You can enter the club.");
}
else
{
    System.out.println("No admittance.");
}
```

## Comparing Numbers

How can we compare two numbers in our conditional programming?

## Comparing Numbers—Integers

We'll often want to perform operations conditionally based on comparing two numerical values. With integer values, this is easily done using one of the six relational operators.

The _relational operators_ are used to compare two values to each other, and have a value of `true` or `false`, depending on the relationship.

| Sign | Meaning                    |
| ---- | -------------------------- |
| `==` | "is equal to"              |
| `<`  | "less than"                |
| `>`  | "greater than"             |
| `<=` | "less than or equal to"    |
| `>=` | "greater than or equal to" |
| `!=` | "not equal to"             |

**Example:**

```java
Scanner in = new Scanner(System.in);
System.out.print("Enter your age: ");
double age = in.nextDouble();
if (age >= 18)
{
    System.out.println("You can vote!");
}
else
{
    System.out.println("You can't vote (yet).");
}
```

In addition to the _relational operators_ that compare two values there are _logical operators_ that allow you to form more complex logical relationships.

## Logical Operators

The _logical operators_ produce a value of `true` or `false` based on evaluating boolean values.

| Sign | Meaning                                                                     |
| ---- | --------------------------------------------------------------------------- |
| `&&` | "and": true if both expressions are true                                    |
| `\|` | "or": true if either expression is true                                     |
| `!`  | "not": true if the expression is false, and false if the expression is true |

**AND Example:**

```java
if (age >= 13 && age < 20)
    System.out.println("You're a teenager.");
```

**OR Example:**

```java
if (age < 0 || age > 110)
    System.out.println("I don't think I believe you.");
```

**NOT Example:**

```java
System.out.print("Enter a positive number");
double value = in.nextDouble();
if (!(value > 0))
    System.out.println("ERROR: Positive number expected");
```

You might notice that in the NOT example above we could have re-written the `if` statement so that it doesn't require a negation:

```java
if (value <= 0)...
```

While this is correct, and you may even choose to write it without the `!` in there, there will be occasions where using the _not_ operator will allow your code to make more sense, and be more readable to you and others.

## Common Mistakes

Common mistakes: you can't say `if (0 < age < 21)...`

and you can't say `if (roll == 7 || 11)...`

Each individual Boolean expression has be complete:

`if (0 < age && age < 21)....`

`if (roll == 7 || roll == 11)...`

## Comparing Numbers—Doubles

Comparing doubles can get tricky, as you already know. Look at this code segment:

```java
double root = Math.sqrt(2);
double square = root * root;
if (square == 2.0)
    System.out.println("We're good!");
else
    System.out.println("Uh-oh... The square of root 2 is " + square + " ???!");
```

The output produced by this code is `Uh-oh... The square of root 2 is 2.0000000000000004 ???!`

So what happened?

The decimal values that are stored as binary numbers in the computer suffer from rounding errors during some calculations. Ultimately, when working with floating-point (`double`) values, we're not trying to identify whether the values are _exactly_ the same. We just need to find out if they are _close enough_ to being equal, where "close enough" is determined by you and the needs of the program.

Here's a common strategy for comparing doubles, and one I use in evaluating your work: Define a constant `EPSILON` that is equal to some really small value like 1E-10. When you compare two values that are `double`s, then, you check to see if the two values are within `EPSILON` of each other. If they are, that's close enough!

```java
final double EPSILON = 1E-10; // defined at beginning of class 
                              // w/ instance variables
                              
if (Math.abs(x - y) <= EPSILON)
{
    // x is approximately = y
    System.out.println("That's close enough for me!");
}
```

## Comparing Strings

Because `Strings` are objects, you can't use the same relational operators that you can use with numbers. (Actually, you _can_, but it just checks to see if your strings are the same object, not whether their values are the same. And we usually want to compare _values_.)

Since `Strings` are objects, you might expect that the `String` class has some methods that allow you to compare them. And it does!

`if (string1.equals(string2))...`

`Strings` are case-sensitive, so if you want to check the letters regardless of case:

`if (string1.equalsIgnoreCase(string2))...`

If you want to find out their dictionary order:

`if (string1.compareTo(string2) < 0)...`

How does that last statement work? If it evaluates to `true`—if `string1.compareTo(string2)` has a negative value—then `string1` comes before `string2`, lexicographically.

Let's take a look at why you don't want to use `==` with Strings.

What happens when the user types in the string `Sarah` in this program?

```java
String name1 = "Sarah";
String name2 = in.nextLine(System.in);  // user types in "Sarah"
if (name1 == name2)
{
    System.out.println("You typed in the name Sarah!");
}
else
{
    System.out.println("You didn't type in the name Sarah.");
}
```

If this code is run and the user types in the String `Sarah`, the code will _not_ identify that those two strings are the same. When the comparison `==` is used with objects, it's comparing the objects themselves rather than the _values_ of those objects. Because `name1` and `name2` refer to different objects, it doesn't matter what the contents are—they're not the same.

To check to see if the name typed in is `Sarah`, the code should be written like this:

```java
if (name1.equals(name2))
{
    System.out.println("You typed in the name Sarah!");
}
else...
```

> [!WARNING]
> 
> **NEVER** use `==` to compare two string values! Always use `.equals()` or `.compareTo()`

Another practical construction is _nested_ `if-else` statements, when there are multiple _levels_ of decisions that have to be made.

```
if ( Boolean expression )
{
    statement;
    if ( Boolean expression )
    {
        statement;
        statement;
    }
    else
    {
        statement;
    }
    statement;
}
else
{
    statement;
    statement;
}
statement;
```

Write a program that has the user enter their age, and print one of four responses, based on where their age falls: < 18, between 18 and 20 (inclusive), between 21 - 30, and > 30.

What some advice? Here's how _not_ to do it:

```java
Scanner in = new Scanner(System.in);
System.out.print("Enter your age: ");
double age = in.nextDouble();
if (age < 18)
    System.out.println("You can't vote yet...");
if (age >= 18 && age < 21)
    System.out.println("You can't buy alcohol yet...");
if (age >= 21 && age < 31)
    System.out.println("These are the best years of your life...");
if (age >= 31)
    System.out.println("No, THESE are the best years of your life!");
```

The reason this is the wrong approach is that it involves multiple individual comparisons which are both harder to maintain as a coder and require more processing power/time from the computer. Additionally, it's easier to make a mistake here: if one statement checks for `<21` and the other one checks for `>21`, you've forgotten to take care of the case where the value `== 21`.

A better approach is to use either a sequential series or a nested series of `if-else` statements to help organize the decision process.

```java
Scanner in = new Scanner(System.in);
System.out.print("Enter your age: ");
double age = in.nextDouble();
if (age < 18)
    System.out.println("You can't vote yet...");
else if (age < 21)
    System.out.println("You can't buy alcohol yet...");
else if (age <= 31)
    System.out.println("These are the best years of your life...");
else
    System.out.println("No, THESE are the best years of your life!");
```

Even better would be enclose these statement in curly braces:

```java
Scanner in = new Scanner(System.in);
System.out.print("Enter your age: ");
double age = in.nextDouble();
if (age < 18)
{
    System.out.println("You can't vote yet...");
}
else if (age < 21)
{
    System.out.println("You can't buy alcohol yet...");
}
else if (age <= 31)
{
    System.out.println("These are the best years of your life...");
}
else
{
    System.out.println("No, THESE are the best years of your life!");
}
```

Now try this one.

When choosing a beverage, I sometimes like caffeinated drinks and sometimes non-caffeinated drinks. If I want caffeine and it's before noon, I'll have coffee, but if it's in the afternoon (anytime before 6pm) I'll have a coke. After 6pm I'll have tea. On the other hand, if I don't want caffeine, in the morning I like herbal tea, and in the afternoon I'll have water, and in the evening, I'll have herbal tea.

Develop a method `selectBeverage()` that takes two parameters: the time of day (an `int`, where 1800 = 6pm) and a `String` (either "caffeinated" or "non-caffeinated"). The method should return a `String` that indicates what beverage I should drink.

```java
public String selectBeverage(int timeOfDay, String typeOfBeverage)
{
    if (typeOfBeverage.equals("caffeinated"))
    {
        if (time < 1200))
        {
            return "coffee";
        }
        else if (time < 1800))
        {
            return "coke";
        }
        else
        {
            return "tea";
        }
    }
    else
    {
        if (time < 1200))
        {
            return "herbal tea";
        }
        else if (time < 1800))
        {
            return "water";
        }
        else
        {
            return "herbal tea";
        }
    }
}
```

## Boolean Issues

There are a number of common issues that can arise when programming with Boolean expressions.

## "Dangling Else" Problem

The _dangling else problem_ has to do with ambiguity about which if statement an else might be associated with. Consider this legal `if-else` statement:

```java
boolean adultStatus = false;   // assume not adult
if (age > 0)                   // Error trap
    if (age > 18)
        boolean adultStatus = true;
else
    System.out.println("Error: your age must be greater than 0.");
```

The problem is that the `else` statement, although it looks like it goes with the `(age > 0)` condition because of the way it's typed, it actually goes with the `(age > 18)` condition (an `else` goes with the nearest `if`). Here, an age < 0 won't get trapped, and an age of 17 will produce an "age must be greater than 0" error.

You fix the dangling else problem by using curly braces to correctly isolate the bodies of your `if-else` statements.

```java
boolean adultStatus = false;   // assume not adult
if (age > 0)                   // Error trap
{
    if (age > 18)
        boolean adultStatus = true;
}
else
{
    System.out.println("Error: your age must be greater than 0.");
}
```

## The `null` value

It's possible for a variable to have a `null` value, which simply means that the value hasn't been set. `null` is different from 0, and different from "", and different from being undefined. You can check to see if a value has been set for any variable by comparing the variable using `== null`:

```java
if (middleName != null)
        System.out.println("Middle name is: " + middleName);
```

## DeMorgan's Law

DeMorgan's Law is not a problem, but rather a strategy that you can use to help solve the problem of complex Boolean expressions.

DeMorgan's Law is concerned with simplifying Boolean expressions that include both the _not_ operator (`!`) and a _Boolean operator_. These can be confusing if they're awkwardly phrased, but you can use DeMorgan's Law to convert them to a different, more manageable, form.

Boolean expressions that include a _not_ operator ( `!` ) and boolean operators _and_ ( `&&` in Java ) or _or_ ( `||` in Java) can be simplified by using these conversions:

`!(A && B)  →   (!A || !B)`

and,

`!(A || B)  →   (!A && !B)`

In each case, a _not_ operation acting on a compound boolean expression is distributed over the expressions, and the comparator inside the parentheses is changed to its opposite, from _or_ to _and_ or from _and_ to _or_.

It may also be useful for you to simplify `not` expressions that have comparators.

```java
!(age < 0)  →  age >= 0
!(cost >= 1000) → cost < 1000
```

The game condition below allows a user to take 3 turns to play a game, and let's them play as many times as they want. (Not all of the code is shown.) The boolean expression for the `if` header is written a little confusingly. Rewrite it using DeMorgan's Law.

```java
if ( !(done || turns >=3) )
{
    ...
    ...
}
```

```java
if ( !done && turns < 3 ) ...
```