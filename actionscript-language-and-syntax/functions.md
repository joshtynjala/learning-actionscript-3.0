# Functions

_Functions_ are blocks of code that carry out specific tasks and can be reused
in your program. There are two types of functions in ActionScript 3.0: _methods_
and _function closures_. Whether a function is a called a method or a function
closure depends on the context in which the function is defined. A function is
called a method if you define it as part of a class definition or attach it to
an instance of an object. A function is called a function closure if it is
defined in any other way.

Functions have always been extremely important in ActionScript. In ActionScript
1.0, for example, the `class` keyword did not exist, so “classes” were defined
by constructor functions. Although the `class` keyword has since been added to
the language, a solid understanding of functions is still important if you want
to take full advantage of what the language has to offer. This can be a
challenge for programmers who expect ActionScript functions to behave similarly
to functions in languages such as C++ or Java. Although basic function
definition and invocation should not present a challenge to experienced
programmers, some of the more advanced features of ActionScript functions
require some explanation.

## Basic function concepts

#### Calling functions

You call a function by using its identifier followed by the parentheses operator
(`()`). You use the parentheses operator to enclose any function parameters you
want to send to the function. For example, the `trace()` function is a top-level
function in ActionScript 3.0:

    trace("Use trace to help debug your script");

If you are calling a function with no parameters, you must use an empty pair of
parentheses. For example, you can use the `Math.random()` method, which takes no
parameters, to generate a random number:

    var randomNum:Number = Math.random();

#### Defining your own functions

There are two ways to define a function in ActionScript 3.0: you can use a
function statement or a function expression. The technique you choose depends on
whether you prefer a more static or dynamic programming style. Define your
functions with function statements if you prefer static, or strict mode,
programming. Define your functions with function expressions if you have a
specific need to do so. Function expressions are more often used in dynamic, or
standard mode, programming.

#### Function statements

Function statements are the preferred technique for defining functions in strict
mode. A function statement begins with the `function` keyword, followed by:

- The function name

- The parameters, in a comma-delimited list enclosed in parentheses

- The function body—that is, the ActionScript code to be executed when the
  function is called, enclosed in curly brackets

For example, the following code creates a function that defines a parameter and
then calls the function using the string “ `hello"` as the parameter value:

    function traceParameter(aParam:String)
    {
        trace(aParam);
    }

    traceParameter("hello"); // hello

#### Function expressions

The second way to declare a function is to use an assignment statement with a
function expression, which is also sometimes called a function literal or an
anonymous function. This is a more verbose method that is widely used in earlier
versions of ActionScript.

An assignment statement with a function expression begins with the `var`
keyword, followed by:

- The function name

- The colon operator (`:`)

- The `Function` class to indicate the data type

- The assignment operator (`=`)

- The `function` keyword

- The parameters, in a comma-delimited list enclosed in parentheses

- The function body—that is, the ActionScript code to be executed when the
  function is called, enclosed in curly brackets

  For example, the following code declares the `traceParameter` function using a
  function expression:

      var traceParameter:Function = function (aParam:String)
      {
          trace(aParam);
      };
      traceParameter("hello"); // hello

  Notice that you do not specify a function name, as you do in a function
  statement. Another important difference between function expressions and
  function statements is that a function expression is an expression rather than
  a statement. This means that a function expression cannot stand on its own as
  a function statement can. A function expression can be used only as a part of
  a statement, usually an assignment statement. The following example shows a
  function expression assigned to an array element:

      var traceArray:Array = new Array();
      traceArray[0] = function (aParam:String)
      {
          trace(aParam);
      };
      traceArray[0]("hello");

#### Choosing between statements and expressions

As a general rule, use a function statement unless specific circumstances call
for the use of an expression. Function statements are less verbose, and they
provide a more consistent experience between strict mode and standard mode than
function expressions.

Function statements are easier to read than assignment statements that contain
function expressions. Function statements make your code more concise; they are
less confusing than function expressions, which require you to use both the
`var` and `function` keywords.

Function statements provide a more consistent experience between the two
compiler modes in that you can use dot syntax in both strict and standard mode
to call a method declared using a function statement. This is not necessarily
true for methods declared with a function expression. For example, the following
code defines a class named Example with two methods: `methodExpression()`, which
is declared with a function expression, and `methodStatement()`, which is
declared with a function statement. In strict mode, you cannot use dot syntax to
call the `methodExpression()` method.

    class Example
    {
        var methodExpression = function() {}
        function methodStatement() {}
    }

    var myEx:Example = new Example();
    myEx.methodExpression(); // error in strict mode; okay in standard mode
    myEx.methodStatement(); // okay in strict and standard modes

Function expressions are considered better suited to programming that focuses on
run-time, or dynamic, behavior. If you prefer to use strict mode, but also need
to call a method declared with a function expression, you can use either of two
techniques. First, you can call the method using square brackets (`[]`) instead
of the dot (`.`) operator. The following method call succeeds in both strict
mode and standard mode:

    myExample["methodLiteral"]();

Second, you can declare the entire class as a dynamic class. Although this
allows you to call the method using the dot operator, the downside is that you
sacrifice some strict mode functionality for all instances of that class. For
example, the compiler does not generate an error if you attempt to access an
undefined property on an instance of a dynamic class.

There are some circumstances in which function expressions are useful. One
common use of function expressions is for functions that are used only once and
then discarded. Another less common use is for attaching a function to a
prototype property. For more information, see The prototype object.

There are two subtle differences between function statements and function
expressions that you should take into account when choosing which technique to
use. The first difference is that function expressions do not exist
independently as objects with regard to memory management and garbage
collection. In other words, when you assign a function expression to another
object, such as an array element or an object property, you create the only
reference to that function expression in your code. If the array or object to
which your function expression is attached goes out of scope or is otherwise no
longer available, you no longer have access to the function expression. If the
array or object is deleted, the memory that the function expression uses becomes
eligible for garbage collection, which means that the memory is eligible to be
reclaimed and reused for other purposes.

The following example shows that for a function expression, once the property to
which the expression is assigned is deleted, the function is no longer
available. The class Test is dynamic, which means that you can add a property
named `functionExp` that holds a function expression. The `functionExp()`
function can be called with the dot operator, but once the `functionExp`
property is deleted, the function is no longer accessible.

    dynamic class Test {}
    var myTest:Test = new Test();

    // function expression
    myTest.functionExp = function () { trace("Function expression") };
    myTest.functionExp(); // Function expression
    delete myTest.functionExp;
    myTest.functionExp(); // error

If, on the other hand, the function is first defined with a function statement,
it exists as its own object and continues to exist even after you delete the
property to which it is attached. The `delete` operator only works on properties
of objects, so even a call to delete the function `stateFunc()` itself does not
work.

    dynamic class Test {}
    var myTest:Test = new Test();

    // function statement
    function stateFunc() { trace("Function statement") }
    myTest.statement = stateFunc;
    myTest.statement(); // Function statement
    delete myTest.statement;
    delete stateFunc; // no effect
    stateFunc();// Function statement
    myTest.statement(); // error

The second difference between function statements and function expressions is
that function statements exist throughout the scope in which they are defined,
including in statements that appear before the function statement. Function
expressions, by contrast, are defined only for subsequent statements. For
example, the following code successfully calls the `scopeTest()` function before
it is defined:

    statementTest(); // statementTest

    function statementTest():void
    {
        trace("statementTest");
    }

Function expressions are not available before they are defined, so the following
code results in a run-time error:

    expressionTest(); // run-time error

    var expressionTest:Function = function ()
    {
        trace("expressionTest");
    }

#### Returning values from functions

To return a value from your function, use the `return` statement followed by the
expression or literal value that you want to return. For example, the following
code returns an expression representing the parameter:

    function doubleNum(baseNum:int):int
    {
        return (baseNum * 2);
    }

Notice that the `return` statement terminates the function, so that any
statements below a `return` statement are not executed, as follows:

    function doubleNum(baseNum:int):int {
        return (baseNum * 2);
        trace("after return"); // This trace statement will not be executed.
    }

In strict mode, you must return a value of the appropriate type if you choose to
specify a return type. For example, the following code generates an error in
strict mode, because it does not return a valid value:

    function doubleNum(baseNum:int):int
    {
        trace("after return");
    }

#### Nested functions

You can nest functions, which means that functions can be declared within other
functions. A nested function is available only within its parent function unless
a reference to the function is passed to external code. For example, the
following code declares two nested functions inside the `getNameAndVersion()`
function:

    function getNameAndVersion():String
    {
        function getVersion():String
        {
            return "10";
        }
        function getProductName():String
        {
            return "Flash Player";
        }
        return (getProductName() + " " + getVersion());
    }
    trace(getNameAndVersion()); // Flash Player 10

When nested functions are passed to external code, they are passed as function
closures, which means that the function retains any definitions that are in
scope when the function is defined. For more information, see Function scope.

## Function parameters

ActionScript 3.0 provides some functionality for function parameters that may
seem novel for programmers new to the language. Although the idea of passing
parameters by value or reference should be familiar to most programmers, the
`arguments` object and the ... (rest) parameter may be new to many of you.

#### Passing arguments by value or by reference

In many programming languages, it’s important to understand the distinction
between passing arguments by value or by reference; the distinction can affect
the way code is designed.

To be passed by value means that the value of the argument is copied into a
local variable for use within the function. To be passed by reference means that
only a reference to the argument is passed instead of the actual value. No copy
of the actual argument is made. Instead, a reference to the variable passed as
an argument is created and assigned to a local variable for use within the
function. As a reference to a variable outside the function, the local variable
gives you the ability to change the value of the original variable.

In ActionScript 3.0, all arguments are passed by reference, because all values
are stored as objects. However, objects that belong to the primitive data types,
which includes Boolean, Number, int, uint, and String, have special operators
that make them behave as if they were passed by value. For example, the
following code creates a function named `passPrimitives()` that defines two
parameters named `xParam` and `yParam`, both of type int. These parameters are
similar to local variables declared inside the body of the `passPrimitives()`
function. When the function is called with the arguments `xValue` and `yValue`,
the parameters `xParam` and `yParam` are initialized with references to the int
objects represented by `xValue` and `yValue`. Because the arguments are
primitives, they behave as if passed by value. Although `xParam` and `yParam`
initially contain only references to the `xValue` and `yValue` objects, any
changes to the variables within the function body generate new copies of the
values in memory.

    function passPrimitives(xParam:int, yParam:int):void
    {
        xParam++;
        yParam++;
        trace(xParam, yParam);
    }

    var xValue:int = 10;
    var yValue:int = 15;
    trace(xValue, yValue);// 10 15
    passPrimitives(xValue, yValue); // 11 16
    trace(xValue, yValue);// 10 15

Within the `passPrimitives()` function, the values of `xParam` and `yParam` are
incremented, but this does not affect the values of `xValue` and `yValue`, as
shown in the last `trace`statement. This would be true even if the parameters
were named identically to the variables, `xValue` and `yValue`, because the
`xValue` and `yValue` inside the function would point to new locations in memory
that exist separately from the variables of the same name outside the function.

All other objects—that is, objects that do not belong to the primitive data
types—are always passed by reference, which gives you ability to change the
value of the original variable. For example, the following code creates an
object named `objVar` with two properties, `x` and `y`. The object is passed as
an argument to the `passByRef()` function. Because the object is not a primitive
type, the object is not only passed by reference, but also stays a reference.
This means that changes made to the parameters within the function affect the
object properties outside the function.

    function passByRef(objParam:Object):void
    {
        objParam.x++;
        objParam.y++;
        trace(objParam.x, objParam.y);
    }
    var objVar:Object = {x:10, y:15};
    trace(objVar.x, objVar.y); // 10 15
    passByRef(objVar); // 11 16
    trace(objVar.x, objVar.y); // 11 16

The `objParam` parameter references the same object as the global `objVar`
variable. As you can see from the `trace` statements in the example, changes to
the `x` and `y` properties of the `objParam` object are reflected in the
`objVar` object.

#### Default parameter values

In ActionScript 3.0, you can declare _default parameter values_ for a function.
If a call to a function with default parameter values omits a parameter with
default values, the value specified in the function definition for that
parameter is used. All parameters with default values must be placed at the end
of the parameter list. The values assigned as default values must be
compile-time constants. The existence of a default value for a parameter
effectively makes that parameter an _optional parameter_. A parameter without a
default value is considered a _required parameter_.

For example, the following code creates a function with three parameters, two of
which have default values. When the function is called with only one parameter,
the default values for the parameters are used.

    function defaultValues(x:int, y:int = 3, z:int = 5):void
    {
        trace(x, y, z);
    }
    defaultValues(1); // 1 3 5

#### The arguments object

When parameters are passed to a function, you can use the `arguments` object to
access information about the parameters passed to your function. Some important
aspects of the `arguments` object include the following:

- The `arguments` object is an array that includes all the parameters passed to
  the function.

- The `arguments.length` property reports the number of parameters passed to the
  function.

- The `arguments.callee` property provides a reference to the function itself,
  which is useful for recursive calls to function expressions.

  <div>

  Note: The `arguments` object is not available if any parameter is named
  `arguments` or if you use the ... (rest) parameter.

  </div>

  If the `arguments` object is referenced in the body of a function,
  ActionScript 3.0 allows function calls to include more parameters than those
  defined in the function definition, but generates a compiler error in strict
  mode if the number of parameters doesn’t match the number of required
  parameters (and optionally, any optional parameters). You can use the array
  aspect of the `arguments` object to access any parameter passed to the
  function, whether or not that parameter is defined in the function definition.
  The following example, which only compiles in standard mode, uses the
  `arguments` array along with the `arguments.length` property to trace all the
  parameters passed to the `traceArgArray()` function:

      function traceArgArray(x:int):void
      {
          for (var i:uint = 0; i < arguments.length; i++)
          {
              trace(arguments[i]);
          }
      }

      traceArgArray(1, 2, 3);

      // output:
      // 1
      // 2
      // 3

  The `arguments.callee` property is often used in anonymous functions to create
  recursion. You can use it to add flexibility to your code. If the name of a
  recursive function changes over the course of your development cycle, you need
  not worry about changing the recursive call in your function body if you use
  `arguments.callee` instead of the function name. The `arguments.callee`
  property is used in the following function expression to enable recursion:

      var factorial:Function = function (x:uint)
      {
          if(x == 0)
          {
              return 1;
          }
          else
          {
              return (x * arguments.callee(x - 1));
          }
      }

      trace(factorial(5)); // 120

  If you use the ... (rest) parameter in your function declaration,
  the` arguments` object is not available to you. Instead, you must access the
  parameters using the parameter names that you declared for them.

  You should also be careful to avoid using the string `"arguments"` as a
  parameter name, because it shadows the `arguments` object. For example, if the
  function `traceArgArray()`is rewritten so that an `arguments` parameter is
  added, the references to `arguments` in the function body refer to the
  parameter rather than the `arguments` object. The following code produces no
  output:

      function traceArgArray(x:int, arguments:int):void
      {
          for (var i:uint = 0; i < arguments.length; i++)
          {
              trace(arguments[i]);
          }
      }

      traceArgArray(1, 2, 3);

      // no output

  The `arguments` object in previous versions of ActionScript also contained a
  property named `caller`, which is a reference to the function that called the
  current function. The `caller` property is not present in ActionScript 3.0,
  but if you need a reference to the calling function, you can alter the calling
  function so that it passes an extra parameter that is a reference to itself.

#### The ... (rest) parameter

ActionScript 3.0 introduces a new parameter declaration called the ... (rest)
parameter. This parameter allows you to specify an array parameter that accepts
any number of comma- delimited arguments. The parameter can have any name that
is not a reserved word. This parameter declaration must be the last parameter
specified. Use of this parameter makes the `arguments` object unavailable.
Although the ... (rest) parameter gives you the same functionality as the
`arguments` array and `arguments.length` property, it does not provide
functionality similar to that provided by `arguments.callee`. You should ensure
that you do not need to use `arguments.callee` before using the ... (rest)
parameter.

The following example rewrites the `traceArgArray()` function using the ...
(rest) parameter instead of the `arguments` object:

    function traceArgArray(... args):void
    {
        for (var i:uint = 0; i < args.length; i++)
        {
            trace(args[i]);
        }
    }

    traceArgArray(1, 2, 3);

    // output:
    // 1
    // 2
    // 3

The ... (rest) parameter can also be used with other parameters, as long as it
is the last parameter listed. The following example modifies the
`traceArgArray()` function so that its first parameter, `x`, is of type int, and
the second parameter uses the ... (rest) parameter. The output skips the first
value, because the first parameter is no longer part of the array created by the
... (rest) parameter.

    function traceArgArray(x: int, ... args)
    {
        for (var i:uint = 0; i < args.length; i++)
        {
            trace(args[i]);
        }
    }

    traceArgArray(1, 2, 3);

    // output:
    // 2
    // 3

## Functions as objects

Functions in ActionScript 3.0 are objects. When you create a function, you are
creating an object that not only can be passed as a parameter to another
function, but also can have properties and methods attached to it.

Functions passed as arguments to another function are passed by reference and
not by value. When you pass a function as an argument, you use only the
identifier and not the parentheses operator that you use to call the method. For
example, the following code passes a function named `clickListener()` as an
argument to the `addEventListener()` method:

    addEventListener(MouseEvent.CLICK, clickListener);

Although it may seem strange to programmers new to ActionScript, functions can
have properties and methods, just as any other object can. In fact, every
function has a read-only property named `length` that stores the number of
parameters defined for the function. This is different from the
`arguments.length` property, which reports the number of arguments sent to the
function. Recall that in ActionScript, the number of arguments sent to a
function can exceed the number of parameters defined for that function. The
following example, which compiles only in standard mode because strict mode
requires an exact match between the number of arguments passed and the number of
parameters defined, shows the difference between the two properties:

    // Compiles only in standard mode
    function traceLength(x:uint, y:uint):void
    {
        trace("arguments received: " + arguments.length);
        trace("arguments expected: " + traceLength.length);
    }

    traceLength(3, 5, 7, 11);
    /* output:
    arguments received: 4
    arguments expected: 2 */

In standard mode, you can define your own function properties by defining them
outside your function body. Function properties can serve as quasi-static
properties that allow you to save the state of a variable related to the
function. For example, you may want to track the number of times a particular
function is called. Such functionality could be useful if you are writing a game
and want to track the number of times a user uses a specific command, although
you could also use a static class property for this. The following example,
which compiles only in standard mode because strict mode does not allow you to
add dynamic properties to functions, creates a function property outside the
function declaration and increments the property each time the function is
called:

    // Compiles only in standard mode
    var someFunction:Function = function ():void
    {
        someFunction.counter++;
    }

    someFunction.counter = 0;

    someFunction();
    someFunction();
    trace(someFunction.counter); // 2

## Function scope

A function’s scope determines not only where in a program that function can be
called, but also what definitions the function can access. The same scope rules
that apply to variable identifiers apply to function identifiers. A function
declared in the global scope is available throughout your code. For example,
ActionScript 3.0 contains global functions, such as `isNaN()` and `parseInt()`,
that are available anywhere in your code. A nested function—a function declared
within another function—can be used anywhere in the function in which it was
declared.

#### The scope chain

Any time a function begins execution, a number of objects and properties are
created. First, a special object called an _activation object_ is created that
stores the parameters and any local variables or functions declared in the
function body. You cannot access the activation object directly, because it is
an internal mechanism. Second, a _scope chain_ is created that contains an
ordered list of objects that the runtime checks for identifier declarations.
Every function that executes has a scope chain that is stored in an internal
property. For a nested function, the scope chain starts with its own activation
object, followed by its parent function’s activation object. The chain continues
in this manner until it reaches the global object. The global object is created
when an ActionScript program begins, and contains all global variables and
functions.

#### Function closures

A _function closure_ is an object that contains a snapshot of a function and its
_lexical environment_. A function’s lexical environment includes all the
variables, properties, methods, and objects in the function’s scope chain, along
with their values. Function closures are created any time a function is executed
apart from an object or a class. The fact that function closures retain the
scope in which they were defined creates interesting results when a function is
passed as an argument or a return value into a different scope.

For example, the following code creates two functions: `foo()`, which returns a
nested function named `rectArea()` that calculates the area of a rectangle, and
`bar()`, which calls `foo()` and stores the returned function closure in a
variable named `myProduct`. Even though the `bar()` function defines its own
local variable `x` (with a value of 2), when the function closure `myProduct()`
is called, it retains the variable `x` (with a value of 40) defined in function
`foo().`The `bar()` function therefore returns the value `160` instead of `8`.

    function foo():Function
    {
        var x:int = 40;
        function rectArea(y:int):int // function closure defined
        {
            return x * y
        }
        return rectArea;
    }
    function bar():void
    {
        var x:int = 2;
        var y:int = 4;
        var myProduct:Function = foo();
        trace(myProduct(4)); // function closure called
    }
    bar(); // 160

Methods behave similarly in that they also retain information about the lexical
environment in which they were created. This characteristic is most noticeable
when a method is extracted from its instance, which creates a bound method. The
main difference between a function closure and a bound method is that the value
of the `this` keyword in a bound method always refers to the instance to which
it was originally attached, whereas in a function closure the value of the
`this` keyword can change.
