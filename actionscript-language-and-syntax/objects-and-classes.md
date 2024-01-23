# Objects and classes

In ActionScript 3.0, every object is defined by a class. A class can be thought
of as a template or a blueprint for a type of object. Class definitions can
include variables and constants, which hold data values, and methods, which are
functions that encapsulate behavior bound to the class. The values stored in
properties can be _primitive values_ or other objects. Primitive values are
numbers, strings, or Boolean values.

ActionScript contains a number of built-in classes that are part of the core
language. Some of these built-in classes, such as Number, Boolean and String,
represent the primitive values available in ActionScript. Others, such as the
Array, Math, and XML classes, define more complex objects.

All classes, whether built-in or user-defined, derive from the Object class. For
programmers with previous ActionScript experience, it is important to note that
the Object data type is no longer the default data type, even though all other
classes still derive from it. In ActionScript 2.0, the following two lines of
code were equivalent because the lack of a type annotation meant that a variable
would be of type Object:

    var someObj:Object;
    var someObj;

ActionScript 3.0, however, introduces the concept of untyped variables, which
can be designated in the following two ways:

    var someObj:*;
    var someObj;

An untyped variable is not the same as a variable of type Object. The key
difference is that untyped variables can hold the special value `undefined`,
while a variable of type Object cannot hold that value.

You can define your own classes using the `class` keyword. You can declare class
properties in three ways: constants can be defined with the `const` keyword,
variables are defined with the `var` keyword, and getter and setter properties
are defined by using the `get` and `set` attributes in a method declaration. You
can declare methods with the `function` keyword.

You create an instance of a class by using the `new` operator. The following
example creates an instance of the Date class called `myBirthday`.

    var myBirthday:Date = new Date();
