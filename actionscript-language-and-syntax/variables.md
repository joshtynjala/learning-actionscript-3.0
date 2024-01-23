# Variables

Variables allow you to store values that you use in your program. To declare a
variable, you must use the `var` statement with the variable name. In
ActionScript 3.0, use of the `var` statement is always required. For example,
the following line of ActionScript declares a variable named `i`:

    var i;

If you omit the `var` statement when declaring a variable, you get a compiler
error in strict mode and run-time error in standard mode. For example, the
following line of code results in an error if the variable `i` has not been
previously defined:

    i; // error if i was not previously defined

To associate a variable with a data type, you must do so when you declare the
variable. Declaring a variable without designating the variable’s type is legal,
but generates a compiler warning in strict mode. You designate a variable’s type
by appending the variable name with a colon (:), followed by the variable’s
type. For example, the following code declares a variable `i` that is of type
int:

    var i:int;

You can assign a value to a variable using the assignment operator (`=`). For
example, the following code declares a variable `i` and assigns the value 20 to
it:

    var i:int;
    i = 20;

You may find it more convenient to assign a value to a variable at the same time
that you declare the variable, as in the following example:

    var i:int = 20;

The technique of assigning a value to a variable at the time it is declared is
commonly used not only when assigning primitive values such as integers and
strings, but also when creating an array or instantiating an instance of a
class. The following example shows an array that is declared and assigned a
value using one line of code.

    var numArray:Array = ["zero", "one", "two"];

You can create an instance of a class by using the `new` operator. The following
example creates an instance of a named `CustomClass`, and assigns a reference to
the newly created class instance to the variable named `customItem`:

    var customItem:CustomClass = new CustomClass();

If you have more than one variable to declare, you can declare them all on one
line of code by using the comma operator (`,`) to separate the variables. For
example, the following code declares three variables on one line of code:

    var a:int, b:int, c:int;

You can also assign values to each of the variables on the same line of code.
For example, the following code declares three variables (`a`, `b,` and `c`) and
assigns each a value:

    var a:int = 10, b:int = 20, c:int = 30;

Although you can use the comma operator to group variable declarations into one
statement, doing so may reduce the readability of your code.

## Understanding variable scope

The _scope_ of a variable is the area of your code where the variable can be
accessed by a lexical reference. A _global_ variable is one that is defined in
all areas of your code, whereas a _local_ variable is one that is defined in
only one part of your code. In ActionScript 3.0, variables are always assigned
the scope of the function or class in which they are declared. A global variable
is a variable that you define outside of any function or class definition. For
example, the following code creates a global variable `strGlobal` by declaring
it outside of any function. The example shows that a global variable is
available both inside and outside the function definition.

    var strGlobal:String = "Global";
    function scopeTest()
    {
        trace(strGlobal); // Global
    }
    scopeTest();
    trace(strGlobal); // Global

You declare a local variable by declaring the variable inside a function
definition. The smallest area of code for which you can define a local variable
is a function definition. A local variable declared within a function exists
only in that function. For example, if you declare a variable named `str2`
within a function named `localScope()`, that variable is not available outside
the function.

    function localScope()
    {
        var strLocal:String = "local";
    }
    localScope();
    trace(strLocal); // error because strLocal is not defined globally

If the variable name you use for your local variable is already declared as a
global variable, the local definition hides (or shadows) the global definition
while the local variable is in scope. The global variable still exists outside
of the function. For example, the following code creates a global string
variable named `str1`, and then creates a local variable of the same name inside
the `scopeTest()` function. The `trace` statement inside the function outputs
the local value of the variable, but the `trace` statement outside the function
outputs the global value of the variable.

    var str1:String = "Global";
    function scopeTest ()
    {
        var str1:String = "Local";
        trace(str1); // Local
    }
    scopeTest();
    trace(str1); // Global

ActionScript variables, unlike variables in C++ and Java, do not have
block-level scope. A block of code is any group of statements between an opening
curly bracket (`{`) and a closing curly bracket (`}`). In some programming
languages, such as C++ and Java, variables declared inside a block of code are
not available outside that block of code. This restriction of scope is called
block-level scope, and does not exist in ActionScript. If you declare a variable
inside a block of code, that variable is available not only in that block of
code, but also in any other parts of the function to which the code block
belongs. For example, the following function contains variables that are defined
in various block scopes. All the variables are available throughout the
function.

    function blockTest (testArray:Array)
    {
        var numElements:int = testArray.length;
        if (numElements > 0)
        {
            var elemStr:String = "Element #";
            for (var i:int = 0; i < numElements; i++)
            {
                var valueStr:String = i + ": " + testArray[i];
                trace(elemStr + valueStr);
            }
            trace(elemStr, valueStr, i); // all still defined
        }
        trace(elemStr, valueStr, i); // all defined if numElements > 0
    }

    blockTest(["Earth", "Moon", "Sun"]);

An interesting implication of the lack of block-level scope is that you can read
or write to a variable before it is declared, as long as it is declared before
the function ends. This is because of a technique called _hoisting_, which means
that the compiler moves all variable declarations to the top of the function.
For example, the following code compiles even though the initial `trace()`
function for the `num` variable happens before the `num` variable is declared:

    trace(num); // NaN
    var num:Number = 10;
    trace(num); // 10

The compiler will not, however, hoist any assignment statements. This explains
why the initial `trace()` of `num` results in `NaN`(not a number), which is the
default value for variables of the Number data type. This means that you can
assign values to variables even before they are declared, as shown in the
following example:

    num = 5;
    trace(num); // 5
    var num:Number = 10;
    trace(num); // 10

## Default values

A _default value_ is the value that a variable contains before you set its
value. You _initialize_ a variable when you set its value for the first time. If
you declare a variable, but do not set its value, that variable is
_uninitialized_. The value of an uninitialized variable depends on its data
type. The following table describes the default values of variables, organized
by data type:

| Data type                                          | Default value |
| -------------------------------------------------- | ------------- |
| Boolean                                            | `false`       |
| int                                                | 0             |
| Number                                             | `NaN`         |
| Object                                             | `null`        |
| String                                             | `null`        |
| uint                                               | 0             |
| Not declared (equivalent to type annotation `*`)   | `undefined`   |
| All other classes, including user-defined classes. | `null`        |

For variables of type Number, the default value is `NaN`(not a number), which is
a special value defined by the IEEE-754 standard to mean a value that does not
represent a number.

If you declare a variable, but do not declare its data type, the default data
type `*` applies, which actually means that the variable is untyped. If you also
do not initialize an untyped variable with a value, its default value is
`undefined`.

For data types other than Boolean, Number, int, and uint, the default value of
any uninitialized variable is `null`. This applies to all the classes defined by
ActionScript 3.0, as well as any custom classes that you create.

The value `null` is not a valid value for variables of type Boolean, Number,
int, or uint. If you attempt to assign a value of `null` to a such a variable,
the value is converted to the default value for that data type. For variables of
type Object, you can assign a value of `null`. If you attempt to assign the
value `undefined` to a variable of type Object, the value is converted to
`null`.

For variables of type Number, there is a special top-level function named
`isNaN()` that returns the Boolean value `true` if the variable is not a number,
and `false` otherwise.
