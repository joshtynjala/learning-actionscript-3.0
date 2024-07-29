# Data types

A _data type_ defines a set of values. For example, the Boolean data type is the
set of exactly two values: `true` and `false`. In addition to the Boolean data
type, ActionScript 3.0 defines several more commonly used data types, such as
String, Number, and Array. You can define your own data types by using classes
or interfaces to define a custom set of values. All values in ActionScript 3.0,
whether they are primitive or complex*,* are objects.

A _primitive value_ is a value that belongs to one of the following data types:
Boolean, int, Number, String, and uint. Working with primitive values is usually
faster than working with complex values, because ActionScript stores primitive
values in a special way that makes memory and speed optimizations possible.

> **Note:** For readers interested in the technical details, ActionScript stores
> primitive values internally as immutable objects. The fact that they are
> stored as immutable objects means that passing by reference is effectively the
> same as passing by value. This cuts down on memory usage and increases
> execution speed, because references are usually significantly smaller than the
> values themselves.

A _complex value_ is a value that is not a primitive value. Data types that
define sets of complex values include Array, Date, Error, Function, RegExp, XML,
and XMLList.

Many programming languages distinguish between primitive values and their
wrapper objects. Java, for example, has an int primitive and the
java.lang.Integer class that wraps it. Java primitives are not objects, but
their wrappers are, which makes primitives useful for some operations, and
wrapper objects better suited for other operations. In ActionScript 3.0,
primitive values and their wrapper objects are, for practical purposes,
indistinguishable. All values, even primitive values, are objects. The runtime
treats these primitive types as special cases that behave like objects but that
don’t require the normal overhead associated with creating objects. This means
that the following two lines of code are equivalent:

    var someInt:int = 3;
    var someInt:int = new int(3);

All the primitive and complex data types listed above are defined by the
ActionScript 3.0 core classes. The core classes allow you to create objects
using literal values instead of using the `new` operator. For example, you can
create an array using a literal value or the Array class constructor, as
follows:

    var someArray:Array = [1, 2, 3]; // literal value
    var someArray:Array = new Array(1,2,3); // Array constructor

## Type checking

Type checking can occur at either compile time or run time. Statically typed
languages, such as C++ and Java, do type checking at compile time. Dynamically
typed languages, such as Smalltalk and Python, handle type checking at run time.
As a dynamically typed language, ActionScript 3.0 has run-time type checking,
but also supports compile-time type checking with a special compiler mode called
_strict mode_. In strict mode, type checking occurs at both compile time and run
time, but in standard mode, type checking occurs only at run time.

Dynamically typed languages offer tremendous flexibility when you structure your
code, but at the cost of allowing type errors to manifest at run time.
Statically typed languages report type errors at compile time, but at the cost
of requiring that type information be known at compile time.

### Compile-time type checking

Compile-time type checking is often favored in larger projects because as the
size of a project grows, data type flexibility usually becomes less important
than catching type errors as early as possible. This is why, by default, the
ActionScript compiler in Flash Professional and Flash Builder is set to run in
strict mode.

#### Adobe Flash Builder

You can disable strict mode in Flash Builder through the ActionScript compiler
settings in the Project Properties dialog box.

To provide compile-time type checking, the compiler needs to know the data type
information for the variables or expressions in your code. To explicitly declare
a data type for a variable, add the colon operator (`:`) followed by the data
type as a suffix to the variable name. To associate a data type with a
parameter, use the colon operator followed by the data type. For example, the
following code adds data type information to the `xParam` parameter, and
declares a variable `myParam` with an explicit data type:

    function runtimeTest(xParam:String)
    {
        trace(xParam);
    }
    var myParam:String = "hello";
    runtimeTest(myParam);

In strict mode, the ActionScript compiler reports type mismatches as compiler
errors. For example, the following code declares a function parameter `xParam`,
of type Object, but later attempts to assign values of type String and Number to
that parameter. This produces a compiler error in strict mode.

    function dynamicTest(xParam:Object)
    {
        if (xParam is String)
        {
            var myStr:String = xParam; // compiler error in strict mode
            trace("String: " + myStr);
        }
        else if (xParam is Number)
        {
            var myNum:Number = xParam; // compiler error in strict mode
            trace("Number: " + myNum);
        }
    }

Even in strict mode, however, you can selectively opt of out compile-time type
checking by leaving the right side of an assignment statement untyped. You can
mark a variable or expression as untyped by either omitting a type annotation,
or using the special asterisk (`*`) type annotation. For example, if the
`xParam` parameter in the previous example is modified so that it no longer has
a type annotation, the code compiles in strict mode:

    function dynamicTest(xParam)
    {
        if (xParam is String)
        {
            var myStr:String = xParam;
            trace("String: " + myStr);
        }
        else if (xParam is Number)
        {
            var myNum:Number = xParam;
            trace("Number: " + myNum);
        }
    }
    dynamicTest(100)
    dynamicTest("one hundred");

### Run-time type checking

Run-time type checking occurs in ActionScript 3.0 whether you compile in strict
mode or standard mode. Consider a situation in which the value 3 is passed as an
argument to a function that expects an array. In strict mode, the compiler will
generate an error, because the value 3 is not compatible with the data type
Array. If you disable strict mode, and run in standard mode, the compiler does
not complain about the type mismatch, but run-time type checking results in a
run-time error.

The following example shows a function named `typeTest()` that expects an Array
argument but is passed a value of 3. This causes a run-time error in standard
mode, because the value 3 is not a member of the parameter’s declared data type
(Array).

    function typeTest(xParam:Array)
    {
        trace(xParam);
    }
    var myNum:Number = 3;
    typeTest(myNum);
    // run-time error in ActionScript 3.0 standard mode

There may also be situations where you get a run-time type error even when you
are operating in strict mode. This is possible if you use strict mode, but opt
out of compile-time type checking by using an untyped variable. When you use an
untyped variable, you are not eliminating type checking but rather deferring it
until run time. For example, if the `myNum` variable in the previous example
does not have a declared data type, the compiler cannot detect the type
mismatch, but the code will generate a run-time error because it compares the
run-time value of `myNum`, which is set to 3 as a result of the assignment
statement, with the type of `xParam`, which is set to the Array data type.

    function typeTest(xParam:Array)
    {
        trace(xParam);
    }
    var myNum = 3;
    typeTest(myNum);
    // run-time error in ActionScript 3.0

Run-time type checking also allows more flexible use of inheritance than does
compile-time checking. By deferring type checking to run time, standard mode
allows you to reference properties of a subclass even if you _upcast_. An upcast
occurs when you use a base class to declare the type of a class instance but use
a subclass to instantiate it. For example, you can create a class named
ClassBase that can be extended (classes with the `final` attribute cannot be
extended):

    class ClassBase
    {
    }

You can subsequently create a subclass of ClassBase named ClassExtender, which
has one property named `someString`, as follows:

    class ClassExtender extends ClassBase
    {
        var someString:String;
    }

Using both classes, you can create a class instance that is declared using the
ClassBase data type, but instantiated using the ClassExtender constructor. An
upcast is considered a safe operation, because the base class does not contain
any properties or methods that are not in the subclass.

    var myClass:ClassBase = new ClassExtender();

A subclass, however, does contain properties or methods that its base class does
not. For example, the ClassExtender class contains the `someString` property,
which does not exist in the ClassBase class. In ActionScript 3.0 standard mode,
you can reference this property using the `myClass` instance without generating
a compile-time error, as shown in the following example:

    var myClass:ClassBase = new ClassExtender();
    myClass.someString = "hello";
    // no error in ActionScript 3.0 standard mode

### The is operator

The `is` operator allows you to test whether a variable or expression is a
member of a given data type. In previous versions of ActionScript, the
`instanceof` operator provided this functionality, but in ActionScript 3.0 the
`instanceof` operator should not be used to test for data type membership. The
`is` operator should be used instead of the `instanceof` operator for manual
type checking, because the expression `x instanceof y`merely checks the
prototype chain of `x` for the existence of `y` (and in ActionScript 3.0, the
prototype chain does not provide a complete picture of the inheritance
hierarchy).

The `is` operator examines the proper inheritance hierarchy and can be used to
check not only whether an object is an instance of a particular class, but also
whether an object is an instance of a class that implements a particular
interface. The following example creates an instance of the Sprite class named
`mySprite` and uses the `is` operator to test whether `mySprite` is an instance
of the Sprite and DisplayObject classes, and whether it implements the
IEventDispatcher interface:

    var mySprite:Sprite = new Sprite();
    trace(mySprite is Sprite); // true
    trace(mySprite is DisplayObject);// true
    trace(mySprite is IEventDispatcher); // true

The `is` operator checks the inheritance hierarchy and properly reports that
`mySprite` is compatible with the Sprite and DisplayObject classes (the Sprite
class is a subclass of the DisplayObject class). The `is` operator also checks
whether `mySprite` inherits from any classes that implement the IEventDispatcher
interface. Because the Sprite class inherits from the EventDispatcher class,
which implements the IEventDispatcher interface, the `is` operator correctly
reports that `mySprite` implements the same interface.

The following example shows the same tests from the previous example, but with
`instanceof` instead of the `is` operator. The `instanceof` operator correctly
identifies that `mySprite` is an instance of Sprite or DisplayObject, but it
returns `false` when used to test whether `mySprite` implements the
IEventDispatcher interface.

    trace(mySprite instanceof Sprite); // true
    trace(mySprite instanceof DisplayObject);// true
    trace(mySprite instanceof IEventDispatcher); // false

### The as operator

The `as` operator also allows you to check whether an expression is a member of
a given data type. Unlike the `is` operator, however, the `as` operator does not
return a Boolean value. Rather, the `as` operator returns the value of the
expression instead of `true`, and `null` instead of `false`. The following
example shows the results of using the `as` operator instead of the `is`
operator in the simple case of checking whether a Sprite instance is a member of
the DisplayObject, IEventDispatcher, and Number data types.

    var mySprite:Sprite = new Sprite();
    trace(mySprite as Sprite);                 // [object Sprite]
    trace(mySprite as DisplayObject);                 // [object Sprite]
    trace(mySprite as IEventDispatcher);                 // [object Sprite]
    trace(mySprite as Number);                                       // null

When you use the `as` operator, the operand on the right must be a data type. An
attempt to use an expression other than a data type as the operand on the right
will result in an error.

## Dynamic classes

A _dynamic_ class defines an object that can be altered at run time by adding or
changing properties and methods. A class that is not dynamic, such as the String
class, is a _sealed_ class. You cannot add properties or methods to a sealed
class at run time.

You create dynamic classes by using the `dynamic` attribute when you declare a
class. For example, the following code creates a dynamic class named `Protean`:

    dynamic class Protean
    {
        private var privateGreeting:String = "hi";
        public var publicGreeting:String = "hello";
        function Protean()
        {
            trace("Protean instance created");
        }
    }

If you later instantiate an instance of the `Protean` class, you can add
properties or methods to it outside the class definition. For example, the
following code creates an instance of the `Protean` class and adds a property
named `aString` and a property named `aNumber` to the instance:

    var myProtean:Protean = new Protean();
    myProtean.aString = "testing";
    myProtean.aNumber = 3;
    trace(myProtean.aString, myProtean.aNumber); // testing 3

Properties that you add to an instance of a dynamic class are run-time entities,
so any type checking is done at run time. You cannot add a type annotation to a
property that you add in this manner.

You can also add a method to the `myProtean` instance by defining a function and
attaching the function to a property of the `myProtean` instance. The following
code moves the trace statement into a method named `traceProtean()`:

    var myProtean:Protean = new Protean();
    myProtean.aString = "testing";
    myProtean.aNumber = 3;
    myProtean.traceProtean = function ()
    {
        trace(this.aString, this.aNumber);
    };
    myProtean.traceProtean(); // testing 3

Methods created in this way, however, do not have access to any private
properties or methods of the Protean class. Moreover, even references to public
properties or methods of the `Protean` class must be qualified with either the
`this` keyword or the class name. The following example shows the
`traceProtean()` method attempting to access the private and public variables of
the `Protean` class.

    myProtean.traceProtean = function ()
    {
        trace(myProtean.privateGreeting); // undefined
        trace(myProtean.publicGreeting); // hello
    };
    myProtean.traceProtean();

## Data type descriptions

The primitive data types include Boolean, int, Null, Number, String, uint, and
void. The ActionScript core classes also define the following complex data
types: Object, Array, Date, Error, Function, RegExp, XML, and XMLList.

### Boolean data type

The Boolean data type includes two values: `true` and `false`. No other values
are valid for variables of Boolean type. The default value of a Boolean variable
that has been declared but not initialized is `false`.

### int data type

The int data type is stored internally as a 32-bit integer and includes the set
of integers from

-2,147,483,648 (-2<sup>31</sup>) to 2,147,483,647 (2<sup>31</sup> - 1),
inclusive. Previous versions of ActionScript offered only the Number data type,
which was used for both integers and floating-point numbers. In ActionScript
3.0, you now have access to low-level machine types for 32-bit signed and
unsigned integers. If your variable does not need floating-point numbers, using
the int data type instead of the Number data type is faster and more efficient.

For integer values outside the range of the minimum and maximum int values, use
the Number data type, which can handle values between positive and negative
9,007,199,254,740,992 (53-bit integer values). The default value for variables
that are of the data type int is 0.

### Null data type

The Null data type contains only one value, `null`. This is the default value
for the String data type and all classes that define complex data types,
including the Object class. None of the other primitive data types, such as
Boolean, Number, int, and uint, contain the value `null`. At run time, the value
`null` is converted to the appropriate default value if you attempt to assign
`null` to variables of type Boolean, Number, int, or uint. You cannot use this
data type as a type annotation.

### Number data type

In ActionScript 3.0, the Number data type can represent integers, unsigned
integers, and floating-point numbers. However, to maximize performance, you
should use the Number data type only for integer values larger than the 32-bit
`int` and `uint` types can store or for floating-point numbers. To store a
floating-point number, include a decimal point in the number. If you omit a
decimal point, the number is stored as an integer.

The Number data type uses the 64-bit double-precision format as specified by the
IEEE Standard for Binary Floating-Point Arithmetic (IEEE-754). This standard
dictates how floating-point numbers are stored using the 64 available bits. One
bit is used to designate whether the number is positive or negative. Eleven bits
are used for the exponent, which is stored as base 2. The remaining 52 bits are
used to store the _significand_ (also called the _mantissa_), which is the
number that is raised to the power indicated by the exponent.

By using some of its bits to store an exponent, the Number data type can store
floating-point numbers significantly larger than if it used all of its bits for
the significand. For example, if the Number data type used all 64 bits to store
the significand, it could store a number as large as 2<sup>65</sup> - 1. By
using 11 bits to store an exponent, the Number data type can raise its
significand to a power of 2<sup>1023</sup>.

The maximum and minimum values that the Number type can represent are stored in
static properties of the Number class called `Number.MAX_VALUE` and
`Number.MIN_VALUE`.

    Number.MAX_VALUE == 1.79769313486231e+308
    Number.MIN_VALUE == 4.940656458412467e-324

Although this range of numbers is enormous, the cost of this range is precision.
The Number data type uses 52 bits to store the significand, with the result that
numbers that require more than 52 bits to represent precisely, such as the
fraction 1/3, are only approximations. If your application requires absolute
precision with decimal numbers, you need to use software that implements decimal
floating-point arithmetic as opposed to binary floating-point arithmetic.

When you store integer values with the Number data type, only the 52 bits of the
significand are used. The Number data type uses these 52 bits and a special
hidden bit to represent integers from -9,007,199,254,740,992 (-2<sup>53</sup>)
to 9,007,199,254,740,992 (2<sup>53</sup>).

The `NaN` value is not only used as the default value for variables of type
`Number`, but also as the result of any operation that should return a number
but does not. For example, if you attempt to calculate the square root of a
negative number, the result is `NaN`. Other special Number values include
_positive infinity_ and _negative infinity_`.`

> **Note:** The result of division by `0` is only `NaN` if the divisor is also
> `0`. Division by `0` produces `infinity` when the dividend is positive or
> `-infinity` when the dividend is negative.

### String data type

The String data type represents a sequence of 16-bit characters. Strings are
stored internally as Unicode characters, using the UTF-16 format. Strings are
immutable values, just as they are in the Java programming language. An
operation on a String value returns a new instance of the string. The default
value for a variable declared with the String data type is `null`. The value
`null` is not the same as the empty string (`""`). The value `null` means that
the variable has no value stored in it, while the empty string means that the
variable has a value that is a String containing no characters.

### uint data type

The uint data type is stored internally as a 32-bit unsigned integer and
includes the set of integers from 0 to 4,294,967,295 (2<sup>32</sup> - 1),
inclusive. Use the uint data type for special circumstances that call for
non-negative integers. For example, you must use the uint data type to represent
pixel color values, because the int data type has an internal sign bit that is
not appropriate for handling color values. For integer values larger than the
maximum uint value, use the Number data type, which can handle 53-bit integer
values. The default value for variables that are of data type uint is 0.

### void data type

The void data type contains only one value, `undefined`. In previous versions of
ActionScript, `undefined` was the default value for instances of the Object
class. In ActionScript 3.0, the default value for Object instances is `null`. If
you attempt to assign the value `undefined` to an instance of the Object class,
the value is converted to `null`. You can only assign a value of `undefined` to
variables that are untyped. Untyped variables are variables that either lack any
type annotation, or use the asterisk (`*`) symbol for type annotation. You can
use `void` only as a return type annotation.

### Object data type

The Object data type is defined by the Object class. The Object class serves as
the base class for all class definitions in ActionScript. The ActionScript 3.0
version of the Object data type differs from that of previous versions in three
ways. First, the Object data type is no longer the default data type assigned to
variables with no type annotation. Second, the Object data type no longer
includes the value `undefined`, which used to be the default value of Object
instances. Third, in ActionScript 3.0, the default value for instances of the
Object class is `null`.

In previous versions of ActionScript, a variable with no type annotation was
automatically assigned the Object data type. This is no longer true in
ActionScript 3.0, which now includes the idea of a truly untyped variable.
Variables with no type annotation are now considered untyped. If you prefer to
make it clear to readers of your code that your intention is to leave a variable
untyped, you can use the asterisk (`*`) symbol for the type annotation, which is
equivalent to omitting a type annotation. The following example shows two
equivalent statements, both of which declare an untyped variable `x`:

    var x
    var x:*

Only untyped variables can hold the value `undefined`. If you attempt to assign
the value `undefined` to a variable that has a data type, the runtime converts
the value `undefined` to the default value of that data type. For instances of
the Object data type, the default value is `null`, which means that if you
attempt to assign `undefined` to an Object instance the value is converted to
`null`.

## Type conversions

A type conversion is said to occur when a value is transformed into a value of a
different data type. Type conversions can be either _implicit_ or _explicit_.
Implicit conversion, which is also called _coercion_, is sometimes performed at
run time. For example, if the value 2 is assigned to a variable of the Boolean
data type, the value 2 is converted to the Boolean value `true` before assigning
the value to the variable. Explicit conversion, which is also called _casting_,
occurs when your code instructs the compiler to treat a variable of one data
type as if it belongs to a different data type. When primitive values are
involved, casting actually converts values from one data type to another. To
cast an object to a different type, you wrap the object name in parentheses and
precede it with the name of the new type. For example, the following code takes
a Boolean value and casts it to an integer:

    var myBoolean:Boolean = true;
    var myINT:int = int(myBoolean);
    trace(myINT); // 1

#### Implicit conversions

Implicit conversions happen at run time in a number of contexts:

- In assignment statements

- When values are passed as function arguments

- When values are returned from functions

- In expressions using certain operators, such as the addition (`+`) operator

  For user-defined types, implicit conversions succeed when the value to be
  converted is an instance of the destination class or a class that derives from
  the destination class. If an implicit conversion is unsuccessful, an error
  occurs. For example, the following code contains a successful implicit
  conversion and an unsuccessful implicit conversion:

      class A {}
      class B extends A {}

      var objA:A = new A();
      var objB:B = new B();
      var arr:Array = new Array();

      objA = objB; // Conversion succeeds.
      objB = arr; // Conversion fails.

  For primitive types, implicit conversions are handled by calling the same
  internal conversion algorithms that are called by the explicit conversion
  functions.

#### Explicit conversions

It’s helpful to use explicit conversions, or casting, when you compile in strict
mode, because there may be times when you do not want a type mismatch to
generate a compile-time error. This may be the case when you know that coercion
will convert your values correctly at run time. For example, when working with
data received from a form, you may want to rely on coercion to convert certain
string values to numeric values. The following code generates a compile-time
error even though the code would run correctly in standard mode:

    var quantityField:String = "3";
    var quantity:int = quantityField; // compile time error in strict mode

If you want to continue using strict mode, but would like the string converted
to an integer, you can use explicit conversion, as follows:

    var quantityField:String = "3";
    var quantity:int = int(quantityField); // Explicit conversion succeeds.

#### Casting to int, uint, and Number

You can cast any data type into one of the three number types: int, uint, and
Number. If the number can’t be converted for some reason, the default value of 0
is assigned for the int and uint data types, and the default value of `NaN` is
assigned for the Number data type. If you convert a Boolean value to a number,
`true` becomes the value 1 and `false` becomes the value 0.

    var myBoolean:Boolean = true;
    var myUINT:uint = uint(myBoolean);
    var myINT:int = int(myBoolean);
    var myNum:Number = Number(myBoolean);
    trace(myUINT, myINT, myNum); // 1 1 1
    myBoolean = false;
    myUINT = uint(myBoolean);
    myINT = int(myBoolean);
    myNum = Number(myBoolean);
    trace(myUINT, myINT, myNum); // 0 0 0

String values that contain only digits can be successfully converted into one of
the number types. The number types can also convert strings that look like
negative numbers or strings that represent a hexadecimal value (for example,
`0x1A`). The conversion process ignores leading and trailing white space
characters in the string value. You can also cast strings that look like
floating-point numbers using `Number()`. The inclusion of a decimal point causes
`uint()` and `int()` to return an integer, truncating the decimal and the
characters following it. For example, the following string values can be cast
into numbers:

    trace(uint("5")); // 5
    trace(uint("-5")); // 4294967291. It wraps around from MAX_VALUE
    trace(uint(" 27 ")); // 27
    trace(uint("3.7")); // 3
    trace(int("3.7")); // 3
    trace(int("0x1A")); // 26
    trace(Number("3.7")); // 3.7

String values that contain non-numeric characters return 0 when cast with
`int()` or `uint()` and `NaN` when cast with `Number()`. The conversion process
ignores leading and trailing white space, but returns 0 or `NaN` if a string has
white space separating two numbers.

    trace(uint("5a")); // 0
    trace(uint("ten")); // 0
    trace(uint("17 63")); // 0

In ActionScript 3.0, the `Number()` function no longer supports octal, or base
8, numbers. If you supply a string with a leading zero to the ActionScript 2.0
`Number()` function, the number is interpreted as an octal number, and converted
to its decimal equivalent. This is not true with the `Number()` function in
ActionScript 3.0, which instead ignores the leading zero. For example, the
following code generates different output when compiled using different versions
of ActionScript:

    trace(Number("044"));
    // ActionScript 3.0 44
    // ActionScript 2.0 36

Casting is not necessary when a value of one numeric type is assigned to a
variable of a different numeric type. Even in strict mode, the numeric types are
implicitly converted to the other numeric types. This means that in some cases,
unexpected values may result when the range of a type is exceeded. The following
examples all compile in strict mode, though some generate unexpected values:

    var myUInt:uint = -3; // Assign int/Number value to uint variable
    trace(myUInt); // 4294967293

    var myNum:Number = sampleUINT; // Assign int/uint value to Number variable
    trace(myNum) // 4294967293

    var myInt:int = uint.MAX_VALUE + 1; // Assign Number value to uint variable
    trace(myInt); // 0

    myInt = int.MAX_VALUE + 1; // Assign uint/Number value to int variable
    trace(myInt); // -2147483648

The following table summarizes the results of casting to the Number, int, or
uint data type from other data types.

| Data type or value | Result of conversion to Number, int, or uint                                                                                        |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| Boolean            | If the value is `true`, 1; otherwise, 0.                                                                                            |
| Date               | The internal representation of the Date object, which is the number of milliseconds since midnight January 1, 1970, universal time. |
| `null`             | 0                                                                                                                                   |
| Object             | If the instance is `null` and converted to Number, `NaN`; otherwise, 0.                                                             |
| String             | A number if the string can be converted to a number; otherwise, `NaN` if converted to Number, or 0 if converted to int or uint.     |
| `undefined`        | If converted to Number, `NaN`; if converted to int or uint, 0.                                                                      |

#### Casting to Boolean

Casting to Boolean from any of the numeric data types (uint, int, and Number)
results in `false` if the numeric value is 0, and `true` otherwise. For the
Number data type, the value `NaN` also results in `false`. The following example
shows the results of casting the numbers -1, 0, and 1:

    var myNum:Number;
    for (myNum = -1; myNum<2; myNum++)
    {
        trace("Boolean(" + myNum +") is " + Boolean(myNum));
    }

The output from the example shows that, of the three numbers, only 0 returns a
value of `false`:

    Boolean(-1) is true
    Boolean(0) is false
    Boolean(1) is true

Casting to Boolean from a String value returns `false` if the string is either
`null` or an empty string (`""`). Otherwise, it returns `true`.

    var str1:String; // Uninitialized string is null.
    trace(Boolean(str1)); // false

    var str2:String = ""; // empty string
    trace(Boolean(str2)); // false

    var str3:String = " "; // white space only
    trace(Boolean(str3)); // true

Casting to Boolean from an instance of the Object class returns `false` if the
instance is `null`; otherwise, it returns `true`:

    var myObj:Object; // Uninitialized object is null.
    trace(Boolean(myObj)); // false

    myObj = new Object(); // instantiate
    trace(Boolean(myObj)); // true

Boolean variables get special treatment in strict mode in that you can assign
values of any data type to a Boolean variable without casting. Implicit coercion
from all data types to the Boolean data type occurs even in strict mode. In
other words, unlike almost all other data types, casting to Boolean is not
necessary to avoid strict mode errors. The following examples all compile in
strict mode and behave as expected at run time:

    var myObj:Object = new Object(); // instantiate
    var bool:Boolean = myObj;
    trace(bool); // true
    bool = "random string";
    trace(bool); // true
    bool = new Array();
    trace(bool); // true
    bool = NaN;
    trace(bool); // false

The following table summarizes the results of casting to the Boolean data type
from other data types:

| Data type or value   | Result of conversion to Boolean                                              |
| -------------------- | ---------------------------------------------------------------------------- |
| String               | `false` if the value is `null` or the empty string (`""`); `true` otherwise. |
| `null`               | `false`                                                                      |
| Number, int, or uint | `false` if the value is `NaN` or 0; `true` otherwise.                        |
| Object               | `false` if the instance is `null`; `true` otherwise.                         |

#### Casting to String

Casting to the String data type from any of the numeric data types returns a
string representation of the number. Casting to the String data type from a
Boolean value returns the string `"true"`if the value is `true`, and returns the
string `"false"` if the value is `false`.

Casting to the String data type from an instance of the Object class returns the
string` "null"` if the instance is `null`. Otherwise, casting to the String type
from the Object class returns the string `"[object Object]"`.

Casting to String from an instance of the Array class returns a string made up
of a comma-delimited list of all the array elements. For example, the following
cast to the String data type returns one string containing all three elements of
the array:

    var myArray:Array = ["primary", "secondary", "tertiary"];
    trace(String(myArray)); // primary,secondary,tertiary

Casting to String from an instance of the Date class returns a string
representation of the date that the instance contains. For example, the
following example returns a string representation of the Date class instance
(the output shows result for Pacific Daylight Time):

    var myDate:Date = new Date(2005,6,1);
    trace(String(myDate)); // Fri Jul 1 00:00:00 GMT-0700 2005

The following table summarizes the results of casting to the String data type
from other data types.

| Data type or value   | Result of conversion to string                                     |
| -------------------- | ------------------------------------------------------------------ |
| Array                | A string made up of all array elements.                            |
| Boolean              | "`true`" or "`false`"                                              |
| Date                 | A string representation of the Date object.                        |
| `null`               | `"null"`                                                           |
| Number, int, or uint | A string representation of the number.                             |
| Object               | If the instance is null, `"null"`; otherwise, `"[object Object]".` |
