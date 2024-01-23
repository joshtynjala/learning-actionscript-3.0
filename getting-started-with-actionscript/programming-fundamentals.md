# Programming fundamentals

Since ActionScript is a programming language, it can help you to learn
ActionScript if you first understand a few general computer programming
concepts.

## What computer programs do

First of all, it’s useful to have a conceptual idea of what a computer program
is and what it does. There are two main aspects to a computer program:

- A program is a series of instructions or steps for the computer to carry out.

- Each step ultimately involves manipulating some piece of information or data.

In a general sense, a computer program is just a list of step-by-step
instructions that you give to the computer, which it performs one by one. Each
individual instruction is known as a _statement_. In ActionScript, each
statement is written with a semicolon at the end.

In essence, all that a given instruction in a program does is manipulate some
bit of data that’s stored in the computer’s memory. A simple example is
instructing the computer to add two numbers and store the result in its memory.
A more complex example is if there is a rectangle drawn on the screen and you
want to write a program to move it somewhere else on the screen. The computer
remembers certain information about the rectangle: the x, y coordinates where
it’s located, how wide and tall it is, what color it is, and so on. Each of
those bits of information is stored somewhere in the computer’s memory. A
program to move the rectangle to a different location would have steps like
“change the x coordinate to 200; change the y coordinate to 150.” In other
words, it would specify new values for the x and y coordinates. Behind the
scenes, the computer does something with this data to actually turn those
numbers into the image that appears on the computer screen. However, at the
basic level of detail it’s enough to know that the process of “moving a
rectangle on the screen” just involves changing bits of data in the computer’s
memory.

## Variables and constants

Programming mainly involves changing pieces of information in the computer’s
memory. Consequently, it’s important to have a way to represent a single piece
of information in a program. A _variable_ is a name that represents a value in
the computer’s memory. As you write statements to manipulate values, you write
the variable’s name in place of the value. Any time the computer sees the
variable name in your program, it looks in its memory and uses the value it
finds there. For example, if you have two variables named `value1` and `value2`,
each containing a number, to add those two numbers you could write the
statement:

    value1 + value2

When it’s actually carrying out the steps, the computer looks to see the values
in each variable and adds them together.

In ActionScript 3.0, a variable actually consists of three different parts:

- The variable’s name

- The type of data that can be stored in the variable

- The actual value stored in the computer’s memory

You’ve seen how the computer uses the name as a placeholder for the value. The
data type is also important. When you create a variable in ActionScript, you
specify the specific type of data that it is meant to hold. From that point on,
your program’s instructions can store only that type of data in the variable.
You can manipulate the value using the particular characteristics associated
with its data type. In ActionScript, to create a variable (known as _declaring_
the variable), you use the `var` statement:

    var value1:Number;

This example tells the computer to create a variable named `value1`, which can
hold only Number data. (“Number” is a specific data type defined in
ActionScript.) You can also store a value in the variable right away:

    var value2:Number = 17;

#### Adobe Flash Professional

In Flash Professional, there is another way to declare a variable. When you
place a movie clip symbol, button symbol, or text field on the Stage, you can
give it an instance name in the Property inspector. Behind the scenes, Flash
Professional creates a variable with the same name as the instance name. You can
use that name in your ActionScript code to represent that Stage item. Suppose,
for example, that you have a movie clip symbol on the Stage and you give it the
instance name `rocketShip`. Whenever you use the variable `rocketShip` in your
ActionScript code, you are in fact manipulating that movie clip.

A _constant_ is similar to a variable. It is a name that represents a value in
the computer’s memory with a specified data type. The difference is that a
constant can only be assigned a value one time in the course of an ActionScript
application. Once a constant’s value is assigned, it is the same throughout the
application. The syntax for declaring a constant is almost the same as that for
declaring a variable. The only difference is that you use the `const` keyword
instead of the `var` keyword:

    const SALES_TAX_RATE:Number = 0.07;

A constant is useful for defining a value that is used in multiple places
throughout a project, which don’t change under normal circumstances. Using a
constant rather than a literal value makes your code more readable. For example,
consider two versions of the same code. One multiplies a price by
`SALES_TAX_RATE`. The other multiplies the price by `0.07`. The version that
uses the `SALES_TAX_RATE` constant is easier to understand. In addition, suppose
the value defined by the constant does change. If you use a constant to
represent that value throughout your project, you can change the value in one
place (the constant declaration). In contrast, you would have to change it in
various places if you used hard-coded literal values.

## Data types

In ActionScript, there are many data types that you can use as the data type of
the variables you create. Some of these data types can be thought of as “simple”
or “fundamental” data types:

- String: a textual value, like a name or the text of a book chapter

- Numeric: ActionScript 3.0 includes three specific data types for numeric data:

  - Number: any numeric value, including values with or without a fraction

  - int: an integer (a whole number without a fraction)

  - uint: an “unsigned” integer, meaning a whole number that can’t be negative

- Boolean: a true-or-false value, such as whether a switch is on or whether two
  values are equal

The simple data types represent a single piece of information: for example, a
single number or a single sequence of text. However, most of the data types
defined in ActionScript could are complex data types. They represent a set of
values in a single container. For example, a variable with the data type Date
represents a single value (a moment in time). Nevertheless, that date value is
represented as several values: the day, month, year, hours, minutes, seconds,
and so on, all of which are individual numbers. People generally think of a date
as a single value, and you can treat a date as a single value by creating a Date
variable. However, internally the computer thinks of it as a group of several
values that, put together, define a single date.

Most of the built-in data types, as well as data types defined by programmers,
are complex data types. Some of the complex data types you probably recognize
are:

- MovieClip: a movie clip symbol

- TextField: a dynamic or input text field

- SimpleButton: a button symbol

- Date: information about a single moment in time (a date and time)

Two words that are often used as synonyms for data type are class and object. A
_class_ is simply the definition of a data type. It’s like a template for all
objects of the data type, like saying “all variables of the Example data type
have these characteristics: A, B, and C.” An _object_, on the other hand, is
just an actual instance of a class. For example, a variable whose data type is
MovieClip could be described as a MovieClip object. The following are different
ways of saying the same thing:

- The data type of the variable `myVariable` is Number.

- The variable `myVariable` is a Number instance.

- The variable `myVariable` is a Number object.

- The variable `myVariable` is an instance of the Number class.

<div style="position: absolute; height: 1px; width: 1px; top: -1000px; left: -1000px;">

<span class="ygtvtm"> </span><span class="ygtvtmh"> </span><span class="ygtvtp"> </span><span class="ygtvtph"> </span><span class="ygtvln"> </span><span class="ygtvlm"> </span><span class="ygtvlmh"> </span><span class="ygtvlp"> </span><span class="ygtvlph"> </span><span class="ygtvloading"> </span>
