# Looping

Looping statements allow you to perform a specific block of code repeatedly
using a series of values or variables. Adobe recommends that you always enclose
the block of code in curly brackets (`{}`). Although you can omit the curly
brackets if the block of code contains only one statement, this practice is not
recommended for the same reason that it is not recommended for conditionals: it
increases the likelihood that statements added later are inadvertently excluded
from the block of code. If you later add a statement that you want to include in
the block of code, but forget to add the necessary curly brackets, the statement
are not executed as part of the loop.

## for

The `for` loop allows you to iterate through a variable for a specific range of
values. You must supply three expressions in a `for` statement: a variable that
is set to an initial value, a conditional statement that determines when the
looping ends, and an expression that changes the value of the variable with each
loop. For example, the following code loops five times. The value of the
variable `i` starts at 0 and ends at 4, and the output is the numbers 0 through
4, each on its own line.

    var i:int;
    for (i = 0; i < 5; i++)
    {
        trace(i);
    }

## for..in

The `for..in` loop iterates through the properties of an object, or the elements
of an array. For example, you can use a `for..in` loop to iterate through the
properties of a generic object (object properties are not kept in any particular
order, so properties may appear in a seemingly random order):

    var myObj:Object = {x:20, y:30};
    for (var i:String in myObj)
    {
        trace(i + ": " + myObj[i]);
    }
    // output:
    // x: 20
    // y: 30

You can also iterate through the elements of an array:

    var myArray:Array = ["one", "two", "three"];
    for (var i:String in myArray)
    {
        trace(myArray[i]);
    }
    // output:
    // one
    // two
    // three

What you cannot do is iterate through the properties of an object if it is an
instance of a sealed class (including built-in classes and user-defined
classes). You can only iterate through the properties of a dynamic class. Even
with instances of dynamic classes, you can only iterate through properties that
are added dynamically.

## for each..in

The `for each..in` loop iterates through the items of a collection, which can be
tags in an XML or XMLList object, the values held by object properties, or the
elements of an array. For example, as the following excerpt shows, you can use a
`for each..in` loop to iterate through the properties of a generic object, but
unlike the `for..in` loop, the iterator variable in a `for each..in` loop
contains the value held by the property instead of the name of the property:

    var myObj:Object = {x:20, y:30};
    for each (var num in myObj)
    {
        trace(num);
    }
    // output:
    // 20
    // 30

You can iterate through an XML or XMLList object, as the following example
shows:

    var myXML:XML = <users>
        <fname>Jane</fname>
        <fname>Susan</fname>
        <fname>John</fname>
    </users>;

    for each (var item in myXML.fname)
    {
        trace(item);
    }
    /* output
    Jane
    Susan
    John
    */

You can also iterate through the elements of an array, as this example shows:

    var myArray:Array = ["one", "two", "three"];
    for each (var item in myArray)
    {
        trace(item);
    }
    // output:
    // one
    // two
    // three

You cannot iterate through the properties of an object if the object is an
instance of a sealed class. Even for instances of dynamic classes, you cannot
iterate through any fixed properties, which are properties defined as part of
the class definition.

## while

The `while` loop is like an `if` statement that repeats as long as the condition
is `true`. For example, the following code produces the same output as the `for`
loop example:

    var i:int = 0;
    while (i < 5)
    {
        trace(i);
        i++;
    }

One disadvantage of using a `while` loop instead of a `for` loop is that
infinite loops are easier to write with `while` loops. The `for` loop example
code does not compile if you omit the expression that increments the counter
variable, but the `while` loop example does compile if you omit that step.
Without the expression that increments `i`, the loop becomes an infinite loop.

## do..while

The `do..while` loop is a `while` loop that guarantees that the code block is
executed at least once, because the condition is checked after the code block is
executed. The following code shows a simple example of a `do..while` loop that
generates output even though the condition is not met:

    var i:int = 5;
    do
    {
        trace(i);
        i++;
    } while (i < 5);
    // output: 5
