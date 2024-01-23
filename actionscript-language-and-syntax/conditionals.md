# Conditionals

ActionScript 3.0 provides three basic conditional statements that you can use to
control program flow.

## if..else

The `if..else` conditional statement allows you to test a condition and execute
a block of code if that condition exists, or execute an alternative block of
code if the condition does not exist. For example, the following code tests
whether the value of `x` exceeds 20, generates a `trace()` function if it does,
or generates a different `trace()` function if it does not:

    if (x > 20)
    {
        trace("x is > 20");
    }
    else
    {
        trace("x is <= 20");
    }

If you do not want to execute an alternative block of code, you can use the `if`
statement without the `else` statement.

## if..else if

You can test for more than one condition using the `if..else if` conditional
statement. For example, the following code not only tests whether the value of
`x` exceeds 20, but also tests whether the value of `x` is negative:

    if (x > 20)
    {
        trace("x is > 20");
    }
    else if (x < 0)
    {
        trace("x is negative");
    }

If an `if` or `else` statement is followed by only one statement, the statement
does not need to be enclosed in curly brackets. For example, the following code
does not use curly brackets:

    if (x > 0)
        trace("x is positive");
    else if (x < 0)
        trace("x is negative");
    else
        trace("x is 0");

However, Adobe recommends that you always use curly brackets, because unexpected
behavior can occur if statements are later added to a conditional statement that
lacks curly brackets. For example, in the following code the value of
`positiveNums` increases by 1 whether or not the condition evaluates to `true`:

    var x:int;
    var positiveNums:int = 0;

    if (x > 0)
        trace("x is positive");
        positiveNums++;

    trace(positiveNums); // 1

## switch

The `switch` statement is useful if you have several execution paths that depend
on the same condition expression. It provides functionality similar to a long
series of `if..else if` statements, but is somewhat easier to read. Instead of
testing a condition for a Boolean value, the `switch` statement evaluates an
expression and uses the result to determine which block of code to execute.
Blocks of code begin with a `case` statement and end with a `break` statement.
For example, the following `switch` statement prints the day of the week, based
on the day number returned by the `Date.getDay()` method:

    var someDate:Date = new Date();
    var dayNum:uint = someDate.getDay();
    switch(dayNum)
    {
        case 0:
            trace("Sunday");
            break;
        case 1:
            trace("Monday");
            break;
        case 2:
            trace("Tuesday");
            break;
        case 3:
            trace("Wednesday");
            break;
        case 4:
            trace("Thursday");
            break;
        case 5:
            trace("Friday");
            break;
        case 6:
            trace("Saturday");
            break;
        default:
            trace("Out of range");
            break;
    }
