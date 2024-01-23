# Classes

A class is an abstract representation of an object. A class stores information
about the types of data that an object can hold and the behaviors that an object
can exhibit. The usefulness of such an abstraction is not necessarily apparent
when you write small scripts that contain only a few objects interacting with
one another. However, as the scope of a program grows the number of objects that
must be managed increases. In that case classes allow you to better control how
objects are created and how they interact with one another.

As far back as ActionScript 1.0, ActionScript programmers could use Function
objects to create constructs that resembled classes. ActionScript 2.0 added
formal support for classes with keywords such as `class` and `extends`.
ActionScript 3.0 not only continues to support the keywords introduced in
ActionScript 2.0. It also adds new capabilities. For example, ActionScript 3.0
includes enhanced access control with the `protected` and `internal` attributes.
It also provides better control over inheritance with the `final` and `override`
keywords.

For developers who have created classes in programming languages like Java, C++,
or C#, ActionScript provides a familiar experience. ActionScript shares many of
the same keywords and attribute names, such as `class`, `extends`, and `public`.

Note: In the Adobe ActionScript documentation, the term property means any
member of an object or class, including variables, constants, and methods. In
addition, although the terms class and static are often used interchangeably,
here these terms are distinct. For example, the phrase “class properties” is
used to mean all the members of a class, rather than only the static members.

## Class definitions

ActionScript 3.0 class definitions use syntax that is similar to the syntax used
in ActionScript 2.0 class definitions. Proper syntax for a class definition
calls for the `class` keyword followed by the class name. The class body,
enclosed by curly brackets ( `{}`), follows the class name. For example, the
following code creates a class named Shape that contains one variable, named
`visible`:

    public class Shape
    {
        var visible:Boolean = true;
    }

One significant syntax change involves class definitions that are inside a
package. In ActionScript 2.0, if a class is inside a package, the package name
must be included in the class declaration. In ActionScript 3.0, which introduces
the `package` statement, the package name must be included in the package
declaration instead of in the class declaration. For example, the following
class declarations show how the BitmapData class, which is part of the
flash.display package, is defined in ActionScript 2.0 and ActionScript 3.0:

    // ActionScript 2.0
    class flash.display.BitmapData {}

    // ActionScript 3.0
    package flash.display
    {
        public class BitmapData {}
    }

#### Class attributes

ActionScript 3.0 allows you to modify class definitions using one of the
following four attributes:

| Attribute            | Definition                                             |
| -------------------- | ------------------------------------------------------ |
| `dynamic`            | Allow properties to be added to instances at run time. |
| `final`              | Must not be extended by another class.                 |
| `internal` (default) | Visible to references inside the current package.      |
| `public`             | Visible to references everywhere.                      |

For each of these attributes, except for `internal`, you explicitly include the
attribute to get the associated behavior. For example, if you do not include the
`dynamic` attribute when defining a class, you can’t add properties to a class
instance at run time. You explicitly assign an attribute by placing it at the
beginning of the class definition, as the following code demonstrates:

    dynamic class Shape {}

Notice that the list does not include an attribute named `abstract`. Abstract
classes are not supported in ActionScript 3.0. Notice also that the list does
not include attributes named `private` and `protected`. These attributes have
meaning only inside a class definition, and cannot be applied to classes
themselves. If you do not want a class to be publicly visible outside a package,
place the class inside a package and mark the class with the `internal`
attribute. Alternatively, you can omit both the `internal` and `public`
attributes, and the compiler automatically adds the `internal` attribute for
you. You can also define a class to only be visible inside the source file in
which it is defined. Place the class at the bottom of your source file, below
the closing curly bracket of the package definition.

#### Class body

The class body is enclosed by curly brackets. It defines the variables,
constants, and methods of your class. The following example shows the
declaration for the Accessibility class in ActionScript 3.0:

    public final class Accessibility
    {
        public static function get active():Boolean;
        public static function updateProperties():void;
    }

You can also define a namespace inside a class body. The following example shows
how a namespace can be defined within a class body and used as an attribute of a
method in that class:

    public class SampleClass
    {
        public namespace sampleNamespace;
        sampleNamespace function doSomething():void;
    }

ActionScript 3.0 allows you to include not only definitions in a class body, but
also statements. Statements that are inside a class body, but outside a method
definition, are executed exactly once. This execution happens when the class
definition is first encountered and the associated class object is created. The
following example includes a call to an external function, `hello()`, and a
`trace` statement that outputs a confirmation message when the class is defined:

    function hello():String
    {
        trace("hola");
    }
    class SampleClass
    {
        hello();
        trace("class created");
    }
    // output when class is created
    hola
    class created

In ActionScript 3.0 it is permissible to define a static property and an
instance property with the same name in the same class body. For example, the
following code declares a static variable named `message` and an instance
variable of the same name:

    class StaticTest
    {
        static var message:String = "static variable";
        var message:String = "instance variable";
    }
    // In your script
    var myST:StaticTest = new StaticTest();
    trace(StaticTest.message); // output: static variable
    trace(myST.message); // output: instance variable

## Class property attributes

In discussions of the ActionScript object model, the term _property_ means
anything that can be a member of a class, including variables, constants, and
methods. However, in the Adobe ActionScript 3.0 Reference for the Adobe Flash
Platform the term is used more narrowly. In that context the term property
includes only class members that are variables or are defined by a getter or
setter method. In ActionScript 3.0, there is a set of attributes that can be
used with any property of a class. The following table lists this set of
attributes.

| Attribute                      | Definition                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------------- |
| `internal` (default)           | Visible to references inside the same package.                                        |
| `private`                      | Visible to references in the same class.                                              |
| `protected`                    | Visible to references in the same class and derived classes.                          |
| `public`                       | Visible to references everywhere.                                                     |
| `static`                       | Specifies that a property belongs to the class, as opposed to instances of the class. |
| ` `_`UserDefinedNamespace`_` ` | Custom namespace name defined by user.                                                |

### Access control namespace attributes

ActionScript 3.0 provides four special attributes that control access to
properties defined inside a class: `public`, `private`, `protected`, and
`internal`.

The `public` attribute makes a property visible anywhere in your script. For
example, to make a method available to code outside its package, you must
declare the method with the `public` attribute. This is true for any property,
whether it is declared using the `var`, `const`, or `function` keywords.

The `private` attribute makes a property visible only to callers within the
property’s defining class. This behavior differs from that of the `private`
attribute in ActionScript 2.0, which allowed a subclass to access a private
property in a superclass. Another significant change in behavior has to do with
run-time access. In ActionScript 2.0, the `private` keyword prohibited access
only at compile time and was easily circumvented at run time. In ActionScript
3.0, this is no longer true. Properties that are marked as `private` are
unavailable at both compile time and run time.

For example, the following code creates a simple class named PrivateExample with
one private variable, and then attempts to access the private variable from
outside the class.

    class PrivateExample
    {
        private var privVar:String = "private variable";
    }

    var myExample:PrivateExample = new PrivateExample();
    trace(myExample.privVar);// compile-time error in strict mode
    trace(myExample["privVar"]); // ActionScript 2.0 allows access, but in ActionScript 3.0, this is a run-time error.

In ActionScript 3.0, an attempt to access a private property using the dot
operator ( `myExample.privVar`) results in a compile-time error if you are using
strict mode. Otherwise, the error is reported at run time, just as it is when
you use the property access operator ( `myExample["privVar"]`).

The following table summarizes the results of attempting to access a private
property that belongs to a sealed (not dynamic) class:

|                          | Strict mode        | Standard mode  |
| ------------------------ | ------------------ | -------------- |
| dot operator ( `.`)      | compile-time error | run-time error |
| bracket operator ( `[]`) | run-time error     | run-time error |

In classes declared with the `dynamic` attribute, attempts to access a private
variable do not result in a run-time error. Instead, the variable is not
visible, so the value `undefined` is returned. A compile-time error occurs,
however, if you use the dot operator in strict mode. The following example is
the same as the previous example, except that the PrivateExample class is
declared as a dynamic class:

    dynamic class PrivateExample
    {
        private var privVar:String = "private variable";
    }

    var myExample:PrivateExample = new PrivateExample();
    trace(myExample.privVar);// compile-time error in strict mode
    trace(myExample["privVar"]); // output: undefined

Dynamic classes generally return the value `undefined` instead of generating an
error when code external to a class attempts to access a private property. The
following table shows that an error is generated only when the dot operator is
used to access a private property in strict mode:

|                          | Strict mode        | Standard mode |
| ------------------------ | ------------------ | ------------- |
| dot operator ( `.`)      | compile-time error | `undefined`   |
| bracket operator ( `[]`) | `undefined`        | `undefined`   |

The `protected` attribute, which is new for ActionScript 3.0, makes a property
visible to callers within its own class or in a subclass. In other words, a
protected property is available within its own class or to classes that lie
anywhere below it in the inheritance hierarchy. This is true whether the
subclass is in the same package or in a different package.

For those familiar with ActionScript 2.0, this functionality is similar to the
`private` attribute in ActionScript 2.0. The ActionScript 3.0 `protected`
attribute is also similar to the `protected` attribute in Java. It differs in
that the Java version also permits access to callers within the same package.
The `protected` attribute is useful when you have a variable or method that your
subclasses need but that you want to hide from code that is outside the
inheritance chain.

The `internal` attribute, which is new for ActionScript 3.0, makes a property
visible to callers within its own package. This is the default attribute for
code inside a package, and it applies to any property that does not have any of
the following attributes:

- `public`

- `private`

- `protected`

- a user-defined namespace

The `internal` attribute is similar to the default access control in Java,
although in Java there is no explicit name for this level of access, and it can
be achieved only through the omission of any other access modifier. The
`internal` attribute is available in ActionScript 3.0 to give you the option of
explicitly signifying your intent to make a property visible only to callers
within its own package.

### static attribute

The `static` attribute, which can be used with properties declared with the
`var`, `const`, or `function` keywords, allows you to attach a property to the
class rather than to instances of the class. Code external to the class must
call static properties by using the class name instead of an instance name.

Static properties are not inherited by subclasses, but the properties are part
of a subclass’s scope chain. This means that within the body of a subclass, a
static variable or method can be used without referencing the class in which it
was defined.

### User-defined namespace attributes

As an alternative to the predefined access control attributes, you can create a
custom namespace for use as an attribute. Only one namespace attribute can be
used per definition, and you cannot use a namespace attribute in combination
with any of the access control attributes ( `public`, `private`, `protected`,
`internal`).

## Variables

Variables can be declared with either the `var` or `const` keywords. Variables
declared with the `var` keyword can have their values changed multiple times
throughout the execution of a script. Variables declared with the `const`
keyword are called _constants_ , and can have values assigned to them only once.
An attempt to assign a new value to an initialized constant results in an error.

#### Static variables

Static variables are declared using a combination of the `static` keyword and
either the `var` or `const` statement. Static variables, which are attached to a
class rather than an instance of a class, are useful for storing and sharing
information that applies to an entire class of objects. For example, a static
variable is appropriate if you want to keep a tally of the number of times a
class is instantiated or if you want to store the maximum number of class
instances that are allowed.

The following example creates a `totalCount` variable to track the number of
class instantiations and a `MAX_NUM` constant to store the maximum number of
instantiations. The `totalCount` and `MAX_NUM` variables are static, because
they contain values that apply to the class as a whole rather than to a
particular instance.

    class StaticVars
    {
        public static var totalCount:int = 0;
        public static const MAX_NUM:uint = 16;
    }

Code that is external to the StaticVars class and any of its subclasses can
reference the `totalCount` and `MAX_NUM` properties only through the class
itself. For example, the following code works:

    trace(StaticVars.totalCount); // output: 0
    trace(StaticVars.MAX_NUM); // output: 16

You cannot access static variables through an instance of the class, so the
following code returns errors:

    var myStaticVars:StaticVars = new StaticVars();
    trace(myStaticVars.totalCount); // error
    trace(myStaticVars.MAX_NUM); // error

Variables that are declared with both the `static` and `const` keywords must be
initialized at the same time as you declare the constant, as the StaticVars
class does for `MAX_NUM`. You cannot assign a value to `MAX_NUM` inside the
constructor or an instance method. The following code generates an error,
because it is not a valid way to initialize a static constant:

    // !! Error to initialize static constant this way
    class StaticVars2
    {
        public static const UNIQUESORT:uint;
        function initializeStatic():void
        {
            UNIQUESORT = 16;
        }
    }

#### Instance variables

Instance variables include properties declared with the `var` and `const`
keywords, but without the `static` keyword. Instance variables, which are
attached to class instances rather than to an entire class, are useful for
storing values that are specific to an instance. For example, the Array class
has an instance property named `length`, which stores the number of array
elements that a particular instance of the Array class holds.

Instance variables, whether declared as `var` or `const`, cannot be overridden
in a subclass. You can, however, achieve functionality that is similar to
overriding variables by overriding getter and setter methods.

## Methods

Methods are functions that are part of a class definition. Once an instance of
the class is created, a method is bound to that instance. Unlike a function
declared outside a class, a method cannot be used apart from the instance to
which it is attached.

Methods are defined using the `function` keyword. As with any class property,
you can apply any of the class property attributes to methods, including
private, protected, public, internal, static, or a custom namespace. You can use
a function statement such as the following:

    public function sampleFunction():String {}

Or you can use a variable to which you assign a function expression, as follows:

    public var sampleFunction:Function = function () {}

In most cases, use a function statement instead of a function expression for the
following reasons:

- Function statements are more concise and easier to read.

- Function statements allow you to use the `override` and `final` keywords.

- Function statements create a stronger bond between the identifier (the name of
  the function) and the code within the method body. Because the value of a
  variable can be changed with an assignment statement, the connection between a
  variable and its function expression can be severed at any time. Although you
  can work around this issue by declaring the variable with `const` instead of
  `var`, such a technique is not considered a best practice. It makes the code
  hard to read and prevents the use of the `override` and `final` keywords.

One case in which you must use a function expression is when you choose to
attach a function to the prototype object.

### Constructor methods

Constructor methods, sometimes called _constructors_ , are functions that share
the same name as the class in which they are defined. Any code that you include
in a constructor method is executed whenever an instance of the class is created
with the `new` keyword. For example, the following code defines a simple class
named Example that contains a single property named `status`. The initial value
of the `status` variable is set inside the constructor function.

    class Example
    {
        public var status:String;
        public function Example()
        {
            status = "initialized";
        }
    }

    var myExample:Example = new Example();
    trace(myExample.status); // output: initialized

Constructor methods can only be public, but the use of the `public` attribute is
optional. You cannot use any of the other access control specifiers, including
`private`, `protected`, or `internal`, on a constructor. You also cannot use a
user-defined namespace with a constructor method.

A constructor can make an explicit call to the constructor of its direct
superclass by using the `super()` statement. If the superclass constructor is
not explicitly called, the compiler automatically inserts a call before the
first statement in the constructor body. You can also call methods of the
superclass by using the `super` prefix as a reference to the superclass. If you
decide to use both `super()` and `super` in the same constructor body, be sure
to call `super()` first. Otherwise, the `super` reference does not behave as
expected. The `super()` constructor should also be called before any `throw` or
`return` statement.

The following example demonstrates what happens if you attempt to use the
`super` reference before calling the `super()` constructor. A new class,
ExampleEx, extends the Example class. The ExampleEx constructor attempts to
access the status variable defined in its superclass, but does so before calling
`super()`. The `trace()` statement inside the ExampleEx constructor produces the
value `null`, because the `status` variable is not available until the `super()`
constructor executes.

    class ExampleEx extends Example
    {
        public function ExampleEx()
        {
            trace(super.status);
            super();
        }
    }

    var mySample:ExampleEx = new ExampleEx(); // output: null

Although it is legal to use the `return` statement inside a constructor, it is
not permissible to return a value. In other words, `return` statements must not
have associated expressions or values. Accordingly, constructor methods are not
allowed to return values, which means that no return type can be specified.

If you do not define a constructor method in your class, the compiler
automatically creates an empty constructor for you. If your class extends
another class, the compiler includes a `super()` call in the constructor it
generates.

### Static methods

Static methods, also called _class methods_ , are methods that are declared with
the `static` keyword. Static methods, which are attached to a class rather than
to an instance of a class, are useful for encapsulating functionality that
affects something other than the state of an individual instance. Because static
methods are attached to a class as a whole, static methods can be accessed only
through a class and not through an instance of the class.

Static methods are useful for encapsulating functionality that is not limited to
affecting the state of class instances. In other words, a method should be
static if it provides functionality that does not directly affect the value of a
class instance. For example, the Date class has a static method named `parse()`,
which takes a string and converts it to a number. The method is static because
it does not affect an individual instance of the class. Instead, the `parse()`
method takes a string that represents a date value, parses the string, and
returns a number in a format compatible with the internal representation of a
Date object. This method is not an instance method, because it does not make
sense to apply the method to an instance of the Date class.

Contrast the static `parse()` method with one of the instance methods of the
Date class, such as `getMonth()`. The `getMonth()` method is an instance method,
because it operates directly on the value of an instance by retrieving a
specific component, the month, of a Date instance.

Because static methods are not bound to individual instances, you cannot use the
keywords `this` or `super` within the body of a static method. Both the `this`
reference and the `super` reference have meaning only within the context of an
instance method.

In contrast with some other class-based programming languages, static methods in
ActionScript 3.0 are not inherited.

### Instance methods

Instance methods are methods that are declared without the `static` keyword.
Instance methods, which are attached to instances of a class instead of the
class as a whole, are useful for implementing functionality that affects
individual instances of a class. For example, the Array class contains an
instance method named `sort()`, which operates directly on Array instances.

Within the body of an instance method, both static and instance variables are in
scope, which means that variables defined in the same class can be referenced
using a simple identifier. For example, the following class, CustomArray,
extends the Array class. The CustomArray class defines a static variable named
`arrayCountTotal` to track the total number of class instances, an instance
variable named `arrayNumber` that tracks the order in which the instances were
created, and an instance method named `getPosition()` that returns the values of
these variables.

    public class CustomArray extends Array
    {
        public static var arrayCountTotal:int = 0;
        public var arrayNumber:int;

        public function CustomArray()
        {
            arrayNumber = ++arrayCountTotal;
        }

        public function getArrayPosition():String
        {
            return ("Array " + arrayNumber + " of " + arrayCountTotal);
        }
    }

Although code external to the class must access the `arrayCountTotal` static
variable through the class object using `CustomArray.arrayCountTotal`, code that
resides inside the body of the `getPosition()` method can refer directly to the
static `arrayCountTotal` variable. This is true even for static variables in
superclasses. Though static properties are not inherited in ActionScript 3.0,
static properties in superclasses are in scope. For example, the Array class has
a few static variables, one of which is a constant named `DESCENDING`. Code that
resides in an Array subclass can access the static constant `DESCENDING` using a
simple identifier:

    public class CustomArray extends Array
    {
        public function testStatic():void
        {
            trace(DESCENDING); // output: 2
        }
    }

The value of the `this` reference within the body of an instance method is a
reference to the instance to which the method is attached. The following code
demonstrates that the `this` reference points to the instance that contains the
method:

    class ThisTest
    {
        function thisValue():ThisTest
        {
            return this;
        }
    }

    var myTest:ThisTest = new ThisTest();
    trace(myTest.thisValue() == myTest); // output: true

Inheritance of instance methods can be controlled with the keywords `override`
and `final`. You can use the `override` attribute to redefine an inherited
method, and the `final` attribute to prevent subclasses from overriding a
method.

### Get and set accessor methods

Get and set accessor functions, also called _getters_ and _setters_ , allow you
to adhere to the programming principles of information hiding and encapsulation
while providing an easy-to-use programming interface for the classes that you
create. Get and set functions allow you to keep your class properties private to
the class, but allow users of your class to access those properties as if they
were accessing a class variable instead of calling a class method.

The advantage of this approach is that it allows you to avoid the traditional
accessor functions with unwieldy names, such as `getPropertyName()` and
`setPropertyName()`. Another advantage of getters and setters is that you can
avoid having two public-facing functions for each property that allows both read
and write access.

The following example class, named GetSet, includes get and set accessor
functions named `publicAccess()` that provide access to the private variable
named `privateProperty`:

    class GetSet
    {
        private var privateProperty:String;

        public function get publicAccess():String
        {
            return privateProperty;
        }

        public function set publicAccess(setValue:String):void
        {
            privateProperty = setValue;
        }
    }

If you attempt to access the property `privateProperty` directly, an error
occurs, as follows:

    var myGetSet:GetSet = new GetSet();
    trace(myGetSet.privateProperty); // error occurs

Instead, a user of the GetSet class uses something that appears to be a property
named `publicAccess`, but that is really a pair of get and set accessor
functions that operate on the private property named `privateProperty`. The
following example instantiates the GetSet class, and then sets the value of the
`privateProperty` using the public accessor named `publicAccess`:

    var myGetSet:GetSet = new GetSet();
    trace(myGetSet.publicAccess); // output: null
    myGetSet.publicAccess = "hello";
    trace(myGetSet.publicAccess); // output: hello

Getter and setter functions also make it possible to override properties that
are inherited from a superclass, something that is not possible when you use
regular class member variables. Class member variables that are declared using
the `var` keyword cannot be overridden in a subclass. Properties that are
created using getter and setter functions, however, do not have this
restriction. You can use the `override` attribute on getter and setter functions
that are inherited from a superclass.

### Bound methods

A bound method, sometimes called a _method closure_ , is simply a method that is
extracted from its instance. Examples of bound methods include methods that are
passed as arguments to a function or returned as values from a function. New in
ActionScript 3.0, a bound method is similar to a function closure in that it
retains its lexical environment even when extracted from its instance. The key
difference, however, between a bound method and a function closure is that the
`this` reference for a bound method remains linked, or bound, to the instance
that implements the method. In other words, the `this` reference in a bound
method always points to the original object that implemented the method. For
function closures, the `this` reference is generic, which means that it points
to whatever object the function is associated with at the time it is called.

Understanding bound methods is important if you use the `this` keyword. Recall
that the `this` keyword provides a reference to a method’s parent object. Most
ActionScript programmers expect that the `this` keyword always represents the
object or class that contains the definition of a method. Without method
binding, however, this would not always be true. In previous versions of
ActionScript, for example, the `this` reference did not always refer to the
instance that implemented the method. When methods are extracted from an
instance in ActionScript 2.0, not only is the `this` reference not bound to the
original instance, but also the member variables and methods of the instance’s
class are not available. This is not a problem in ActionScript 3.0, because
bound methods are automatically created when you pass a method as a parameter.
Bound methods ensure that the `this` keyword always references the object or
class in which a method is defined.

The following code defines a class named ThisTest, which contains a method named
`foo()` that defines the bound method, and a method named `bar()` that returns
the bound method. Code external to the class creates an instance of the ThisTest
class, calls the `bar()` method, and stores the return value in a variable named
`myFunc`.

    class ThisTest
    {
        private var num:Number = 3;
        function foo():void // bound method defined
        {
            trace("foo's this: " + this);
            trace("num: " + num);
        }
        function bar():Function
        {
            return foo; // bound method returned
        }
    }

    var myTest:ThisTest = new ThisTest();
    var myFunc:Function = myTest.bar();
    trace(this); // output: [object global]
    myFunc();
    /* output:
    foo's this: [object ThisTest]
    output: num: 3 */

The last two lines of code show that the `this` reference in the bound method
`foo()` still points to an instance of ThisTest class, even though the `this`
reference in the line just before it points to the global object. Moreover, the
bound method stored in the `myFunc` variable still has access to the member
variables of the ThisTest class. If this same code is run in ActionScript 2.0,
the `this` references would match, and the `num` variable would be `undefined`.

One area where the addition of bound methods is most noticeable is with event
handlers, because the `addEventListener()` method requires that you pass a
function or method as an argument.

## Enumerations with classes

_Enumerations_ are custom data types that you create to encapsulate a small set
of values. ActionScript 3.0 does not support a specific enumeration facility,
unlike C++ with its `enum` keyword or Java with its Enumeration interface. You
can, however, create enumerations using classes and static constants. For
example, the PrintJob class in ActionScript 3.0 uses an enumeration named
PrintJobOrientation to store the values `"landscape"` and `"portrait"`, as shown
in the following code:

    public final class PrintJobOrientation
    {
        public static const LANDSCAPE:String = "landscape";
        public static const PORTRAIT:String = "portrait";
    }

By convention, an enumeration class is declared with the `final` attribute,
because there is no need to extend the class. The class includes only static
members, which means that you do not create instances of the class. Instead, you
access the enumeration values directly through the class object, as shown in the
following code excerpt:

    var pj:PrintJob = new PrintJob();
    if(pj.start())
    {
        if (pj.orientation == PrintJobOrientation.PORTRAIT)
        {
            ...
        }
        ...
    }

All of the enumeration classes in ActionScript 3.0 contain only variables of
type String, int, or uint. The advantage of using enumerations instead of
literal string or number values is that typographical mistakes are easier to
find with enumerations. If you mistype the name of an enumeration, the
ActionScript compiler generates an error. If you use literal values, the
compiler does not complain if you spell a word incorrectly or use the wrong
number. In the previous example, the compiler generates an error if the name of
the enumeration constant is incorrect, as the following excerpt shows:

        if (pj.orientation == PrintJobOrientation.PORTRAI) // compiler error

However, the compiler does not generate an error if you misspell a string
literal value, as follows:

        if (pj.orientation == "portrai") // no compiler error

A second technique for creating enumerations also involves creating a separate
class with static properties for the enumeration. This technique differs,
however, in that each of the static properties contains an instance of the class
instead of a string or integer value. For example, the following code creates an
enumeration class for the days of the week:

    public final class Day
    {
        public static const MONDAY:Day = new Day();
        public static const TUESDAY:Day = new Day();
        public static const WEDNESDAY:Day = new Day();
        public static const THURSDAY:Day = new Day();
        public static const FRIDAY:Day = new Day();
        public static const SATURDAY:Day = new Day();
        public static const SUNDAY:Day = new Day();
    }

This technique is not used by ActionScript 3.0 but is used by many developers
who prefer the improved type checking that the technique provides. For example,
a method that returns an enumeration value can restrict the return value to the
enumeration data type. The following code shows not only a function that returns
a day of the week, but also a function call that uses the enumeration type as a
type annotation:

    function getDay():Day
    {
        var date:Date = new Date();
        var retDay:Day;
        switch (date.day)
        {
            case 0:
                retDay = Day.MONDAY;
                break;
            case 1:
                retDay = Day.TUESDAY;
                break;
            case 2:
                retDay = Day.WEDNESDAY;
                break;
            case 3:
                retDay = Day.THURSDAY;
                break;
            case 4:
                retDay = Day.FRIDAY;
                break;
            case 5:
                retDay = Day.SATURDAY;
                break;
            case 6:
                retDay = Day.SUNDAY;
                break;
        }
        return retDay;
    }

    var dayOfWeek:Day = getDay();

You can also enhance the Day class so that it associates an integer with each
day of the week, and provides a `toString()` method that returns a string
representation of the day.

## Embedded asset classes

ActionScript 3.0 uses special classes, called _embedded asset classes_ , to
represent embedded assets. An _embedded asset_ is an asset, such as a sound,
image, or font, that is included in a SWF file at compile time. Embedding an
asset instead of loading it dynamically ensures that it is available at run
time, but at the cost of increased SWF file size.

### Using embedded asset classes in Flash Professional

To embed an asset, first place the asset into a FLA file’s library. Next, use
the asset’s linkage property to provide a name for the asset’s embedded asset
class. If a class by that name cannot be found in the classpath, a class is
automatically generated for you. You can then create an instance of the embedded
asset class and use any properties and methods defined or inherited by that
class. For example, the following code can be used to play an embedded sound
that is linked to an embedded asset class named PianoMusic:

    var piano:PianoMusic = new PianoMusic();
    var sndChannel:SoundChannel = piano.play();

Alternatively, you can use the `[Embed]` metadata tag to embed assets in a Flash
Professional project, described next. If you use the `[Embed]` metadata tag in
your code, Flash Professional uses the Flex compiler to compile your project
instead of the Flash Professional compiler.

### Using embedded asset classes using the Flex compiler

If you are compiling your code using the Flex compiler, to embed an asset in
ActionScript code use the `[Embed]` metadata tag. Place the asset in the main
source folder or another folder that is in your project’s build path. When the
Flex compiler encounters an Embed metadata tag, it creates the embedded asset
class for you. You can access the class through a variable of data type Class
that you declare immediately following the `[Embed]` metadata tag. For example,
the following code embeds a sound named sound1.mp3 and uses a variable named
`soundCls` to store a reference to the embedded asset class associated with that
sound. The example then creates an instance of the embedded asset class and
calls the `play()` method on that instance:

    package
    {
        import flash.display.Sprite;
        import flash.media.SoundChannel;
        import mx.core.SoundAsset;

        public class SoundAssetExample extends Sprite
        {
            [Embed(source="sound1.mp3")]
            public var soundCls:Class;

            public function SoundAssetExample()
            {
                var mySound:SoundAsset = new soundCls() as SoundAsset;
                var sndChannel:SoundChannel = mySound.play();
            }
        }
    }

#### Adobe Flash Builder

To use the `[Embed]` metadata tag in a Flash Builder ActionScript project,
import any necessary classes from the Flex framework. For example, to embed
sounds, import the mx.core.SoundAsset class. To use the Flex framework, include
the file framework.swc in your ActionScript build path. This increases the size
of your SWF file.

#### Adobe Flex

Alternatively, in Flex you can embed an asset with the `@Embed()` directive in
an MXML tag definition.
