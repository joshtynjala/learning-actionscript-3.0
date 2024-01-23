# Syntax

The syntax of a language defines a set of rules that must be followed when
writing executable code.

## Case sensitivity

ActionScript 3.0 is a case-sensitive language. Identifiers that differ only in
case are considered different identifiers. For example, the following code
creates two different variables:

    var num1:int;
    var Num1:int;

## Dot syntax

The dot operator (`.`) provides a way to access the properties and methods of an
object. Using dot syntax, you can refer to a class property or method by using
an instance name, followed by the dot operator and name of the property or
method. For example, consider the following class definition:

    class DotExample
    {
        public var prop1:String;
        public function method1():void {}
    }

Using dot syntax, you can access the `prop1` property and the `method1()` method
by using the instance name created in the following code:

    var myDotEx:DotExample = new DotExample();
    myDotEx.prop1 = "hello";
    myDotEx.method1();

You can use dot syntax when you define packages. You use the dot operator to
refer to nested packages. For example, the EventDispatcher class resides in a
package named events that is nested within the package named flash. You can
refer to the events package using the following expression:

    flash.events

You can also refer to the EventDispatcher class using this expression:

    flash.events.EventDispatcher

## Slash syntax

Slash syntax is not supported in ActionScript 3.0. Slash syntax was used in
earlier versions of ActionScript to indicate the path of a movie clip or
variable.

## Literals

A _literal_ is a value that appears directly in your code. The following
examples are all literals:

    17
    "hello"
    -3
    9.4
    null
    undefined
    true
    false

Literals can also be grouped to form compound literals. Array literals are
enclosed in bracket characters (`[]`) and use the comma to separate array
elements.

An array literal can be used to initialize an array. The following examples show
two arrays that are initialized using array literals. You can use the `new`
statement and pass the compound literal as a parameter to the Array class
constructor, but you can also assign literal values directly when instantiating
instances of the following ActionScript core classes: Object, Array, String,
Number, int, uint, XML, XMLList, and Boolean.

    // Use new statement.
    var myStrings:Array = new Array(["alpha", "beta", "gamma"]);
    var myNums:Array = new Array([1,2,3,5,8]);

    // Assign literal directly.
    var myStrings:Array = ["alpha", "beta", "gamma"];
    var myNums:Array = [1,2,3,5,8];

Literals can also be used to initialize a generic object. A generic object is an
instance of the Object class. Object literals are enclosed in curly brackets
(`{}`) and use the comma to separate object properties. Each property is
declared with the colon character (`:`), which separates the name of the
property from the value of the property.

You can create a generic object using the `new` statement, and pass the object
literal as a parameter to the Object class constructor, or you can assign the
object literal directly to the instance you are declaring. The following example
demonstrates two alternative ways to create a new generic object and initialize
the object with three properties (`propA`, `propB`, and `propC`), each with
values set to 1, 2, and 3, respectively:

    // Use new statement and add properties.
    var myObject:Object = new Object();
    myObject.propA = 1;
    myObject.propB = 2;
    myObject.propC = 3;

    // Assign literal directly.
    var myObject:Object = {propA:1, propB:2, propC:3};

## Semicolons

You can use the semicolon character (`;`) to terminate a statement.
Alternatively, if you omit the semicolon character, the compiler assumes that
each line of code represents a single statement. Because many programmers are
accustomed to using the semicolon to denote the end of a statement, your code
may be easier to read if you consistently use semicolons to terminate your
statements.

Using a semicolon to terminate a statement allows you to place more than one
statement on a single line, but this may make your code more difficult to read.

## Parentheses

You can use parentheses (`()`) in three ways in ActionScript 3.0. First, you can
use parentheses to change the order of operations in an expression. Operations
that are grouped inside parentheses are always executed first. For example,
parentheses are used to alter the order of operations in the following code:

    trace(2 + 3 * 4); // 14
    trace((2 + 3) * 4); // 20

Second, you can use parentheses with the comma operator (`,`) to evaluate a
series of expressions and return the result of the final expression, as shown in
the following example:

    var a:int = 2;
    var b:int = 3;
    trace((a++, b++, a+b)); // 7

Third, you can use parentheses to pass one or more parameters to functions or
methods, as shown in the following example, which passes a String value to the
`trace()` function:

    trace("hello"); // hello

## Comments

ActionScript 3.0 code supports two types of comments: single-line comments and
multiline comments. These commenting mechanisms are similar to the commenting
mechanisms in C++ and Java. The compiler ignores text that is marked as a
comment.

Single-line comments begin with two forward slash characters (`//`) and continue
until the end of the line. For example, the following code contains a
single-line comment:

    var someNumber:Number = 3; // a single line comment

Multiline comments begin with a forward slash and asterisk (`/*`) and end with
an asterisk and forward slash (`*/`).

    /* This is multiline comment that can span
    more than one line of code. */

## Keywords and reserved words

_Reserved words_ are words that you cannot use as identifiers in your code
because the words are reserved for use by ActionScript. Reserved words include
_lexical keywords_, which are removed from the program namespace by the
compiler. The compiler reports an error if you use a lexical keyword as an
identifier. The following table lists ActionScript 3.0 lexical keywords.

|            |            |          |          |
| ---------- | ---------- | -------- | -------- |
| as         | break      | case     | catch    |
| class      | const      | continue | default  |
| delete     | do         | else     | extends  |
| false      | finally    | for      | function |
| if         | implements | import   | in       |
| instanceof | interface  | internal | is       |
| native     | new        | null     | package  |
| private    | protected  | public   | return   |
| super      | switch     | this     | throw    |
| to         | true       | try      | typeof   |
| use        | var        | void     | while    |
| with       |            |          |          |

There is a small set of keywords, called _syntactic keywords_, that can be used
as identifiers, but that have special meaning in certain contexts. The following
table lists ActionScript 3.0 syntactic keywords.

|          |         |       |           |
| -------- | ------- | ----- | --------- |
| each     | get     | set   | namespace |
| include  | dynamic | final | native    |
| override | static  |       |           |

There are also several identifiers that are sometimes referred to as _future
reserved words_. These identifiers are not reserved by ActionScript 3.0, though
some of them may be treated as keywords by software that incorporates
ActionScript 3.0. You might be able to use many of these identifiers in your
code, but Adobe recommends that you do not use them because they may appear as
keywords in a subsequent version of the language.

|          |           |           |              |
| -------- | --------- | --------- | ------------ |
| abstract | boolean   | byte      | cast         |
| char     | debugger  | double    | enum         |
| export   | float     | goto      | intrinsic    |
| long     | prototype | short     | synchronized |
| throws   | to        | transient | type         |
| virtual  | volatile  |           |              |

## Constants

ActionScript 3.0 supports the `const` statement, which you can use to create
constants. Constants are properties with a fixed value that cannot be altered.
You can assign a value to a constant only once, and the assignment must occur in
close proximity to the declaration of the constant. For example, if a constant
is declared as a member of a class, you can assign a value to that constant only
as part of the declaration or inside the class constructor.

The following code declares two constants. The first constant, `MINIMUM`, has a
value assigned as part of the declaration statement. The second constant,
`MAXIMUM`, has a value assigned in the constructor. Note that this example only
compiles in standard mode because strict mode only allows a constant’s value to
be assigned at initialization time.

    class A
    {
        public const MINIMUM:int = 0;
        public const MAXIMUM:int;

        public function A()
        {
            MAXIMUM = 10;
        }
    }

    var a:A = new A();
    trace(a.MINIMUM); // 0
    trace(a.MAXIMUM); // 10

An error results if you attempt to assign an initial value to a constant in any
other way. For example, if you attempt to set the initial value of `MAXIMUM`
outside the class, a run-time error occurs.

    class A
    {
        public const MINIMUM:int = 0;
        public const MAXIMUM:int;
    }

    var a:A = new A();
    a["MAXIMUM"] = 10; // run-time error

ActionScript 3.0 defines a wide range of constants for your use. By convention,
constants in ActionScript use all capital letters, with words separated by the
underscore character (`_`). For example, the MouseEvent class definition uses
this naming convention for its constants, each of which represents an event
related to mouse input:

    package flash.events
    {
        public class MouseEvent extends Event
        {
            public static const CLICK:String = "click";
            public static const DOUBLE_CLICK:String = "doubleClick";
            public static const MOUSE_DOWN:String = "mouseDown";
            public static const MOUSE_MOVE:String = "mouseMove";
            ...
        }
    }

More Help topics

![](../img/as3LinkIndicator.png) 
[Working with strings](https://web.archive.org/web/20120102124212mp_/http://help.adobe.com/en_US/as3/dev/WS5b3ccc516d4fbf351e63e3d118a9b8d6e8-7ff2.html)

![](../img/as3LinkIndicator.png) 
[Using regular expressions](https://web.archive.org/web/20120102124212mp_/http://help.adobe.com/en_US/as3/dev/WS5b3ccc516d4fbf351e63e3d118a9b90204-7fdb.html)

![](../img/as3LinkIndicator.png) 
[Initializing XML variables](https://web.archive.org/web/20120102124212mp_/http://help.adobe.com/en_US/as3/dev/WS5b3ccc516d4fbf351e63e3d118a9b90204-7f95.html)
