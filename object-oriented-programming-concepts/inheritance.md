# Inheritance

Inheritance is a form of code reuse that allows programmers to develop new
classes that are based on existing classes. The existing classes are often
called _base classes_ or _superclasses_, while the new classes are called
_subclasses_. A key advantage of inheritance is that it allows you to reuse code
from a base class yet leave the existing code unmodified. Moreover, inheritance
requires no changes to the way that other classes interact with the base class.
Rather than modifying an existing class that may have been thoroughly tested or
may already be in use, using inheritance you can treat that class as an
integrated module that you can extend with additional properties or methods.
Accordingly, you use the `extends` keyword to indicate that a class inherits
from another class.

Inheritance also allows you to take advantage of _polymorphism_ in your code.
Polymorphism is the ability to use a single method name for a method that
behaves differently when applied to different data types. A simple example is a
base class named Shape with two subclasses named Circle and Square. The Shape
class defines a method named `area()`, which returns the area of the shape. If
polymorphism is implemented, you can call the `area()` method on objects of type
Circle and Square and have the correct calculations done for you. Inheritance
enables polymorphism by allowing subclasses to inherit and redefine, or
_override_, methods from the base class. In the following example, the `area()`
method is redefined by the Circle and Square classes:

    class Shape
    {
        public function area():Number
        {
            return NaN;
        }
    }

    class Circle extends Shape
    {
        private var radius:Number = 1;
        override public function area():Number
        {
            return (Math.PI * (radius * radius));
        }
    }

    class Square extends Shape
    {
        private var side:Number = 1;
        override public function area():Number
        {
            return (side * side);
        }
    }

    var cir:Circle = new Circle();
    trace(cir.area()); // output: 3.141592653589793
    var sq:Square = new Square();
    trace(sq.area()); // output: 1

Because each class defines a data type, the use of inheritance creates a special
relationship between a base class and a class that extends it. A subclass is
guaranteed to possess all the properties of its base class, which means that an
instance of a subclass can always be substituted for an instance of the base
class. For example, if a method defines a parameter of type Shape, it is legal
to pass an argument of type Circle because Circle extends Shape, as in the
following:

    function draw(shapeToDraw:Shape) {}

    var myCircle:Circle = new Circle();
    draw(myCircle);

## Instance properties and inheritance

An instance property, whether defined with the `function`, `var`, or `const`
keywords, is inherited by all subclasses as long as the property is not declared
with the `private` attribute in the base class. For example, the Event class in
ActionScript 3.0 has a number of subclasses that inherit properties common to
all event objects.

For some types of events, the Event class contains all the properties necessary
to define the event. These types of events do not require instance properties
beyond those defined in the Event class. Examples of such events are the
`complete` event, which occurs when data has loaded successfully, and the
`connect` event, which occurs when a network connection has been established.

The following example is an excerpt from the Event class that shows some of the
properties and methods that are inherited by subclasses. Because the properties
are inherited, an instance of any subclass can access these properties.

    public class Event
    {
        public function get type():String;
        public function get bubbles():Boolean;
        ...

        public function stopPropagation():void {}
        public function stopImmediatePropagation():void {}
        public function preventDefault():void {}
        public function isDefaultPrevented():Boolean {}
        ...
    }

Other types of events require unique properties not available in the Event
class. These events are defined using subclasses of the Event class so that new
properties can be added to the properties defined in the Event class. An example
of such a subclass is the MouseEvent class, which adds properties unique to
events associated with mouse movement or mouse clicks, such as the `mouseMove`
and `click` events. The following example is an excerpt from the MouseEvent
class that shows the definition of properties that exist on the subclass but not
on the base class:

    public class MouseEvent extends Event
    {
        public static const CLICK:String= "click";
        public static const MOUSE_MOVE:String = "mouseMove";
        ...

        public function get stageX():Number {}
        public function get stageY():Number {}
        ...
    }

#### Access control specifiers and inheritance

If a property is declared with the `public` keyword, the property is visible to
code anywhere. This means that the `public` keyword, unlike the `private`,
`protected`, and `internal` keywords, places no restrictions on property
inheritance.

If a property is declared with `private` keyword, it is visible only in the
class that defines it, which means that it is not inherited by any subclasses.
This behavior is different from previous versions of ActionScript, where the
`private` keyword behaved more like the ActionScript 3.0 `protected` keyword.

The `protected` keyword indicates that a property is visible not only within the
class that defines it, but also to all subclasses. Unlike the `protected`
keyword in the Java programming language, the `protected` keyword in
ActionScript 3.0 does not make a property visible to all other classes in the
same package. In ActionScript 3.0, only subclasses can access a property
declared with the `protected` keyword. Moreover, a protected property is visible
to a subclass whether the subclass is in the same package as the base class or
in a different package.

To limit the visibility of a property to the package in which it is defined, use
the `internal` keyword or do not use any access control specifier. The
`internal` access control specifier is the default access control specifier that
applies when one is not specified. A property marked as `internal` is only
inherited by a subclass that resides in the same package.

You can use the following example to see how each of the access control
specifiers affects inheritance across package boundaries. The following code
defines a main application class named AccessControl and two other classes named
Base and Extender. The Base class is in a package named foo and the Extender
class, which is a subclass of the Base class, is in a package named bar. The
AccessControl class imports only the Extender class and creates an instance of
Extender that attempts to access a variable named `str` that is defined in the
Base class. The `str` variable is declared as `public` so that the code compiles
and runs as shown in the following excerpt:

    // Base.as in a folder named foo
    package foo
    {
        public class Base
        {
            public var str:String = "hello"; // change public on this line
        }
    }

    // Extender.as in a folder named bar
    package bar
    {
        import foo.Base;
        public class Extender extends Base
        {
            public function getString():String {
                return str;
            }
        }
    }

    // main application class in file named AccessControl.as
    package
    {
        import flash.display.MovieClip;
        import bar.Extender;
        public class AccessControl extends MovieClip
        {
            public function AccessControl()
            {
                var myExt:Extender = new Extender();
                trace(myExt.str);// error if str is not public
                trace(myExt.getString()); // error if str is private or internal
            }
        }
    }

To see how the other access control specifiers affect compilation and execution
of the preceding example, change the `str` variable’s access control specifier
to `private`, `protected`, or `internal` after deleting or commenting out the
following line from the `AccessControl` class:

    trace(myExt.str);// error if str is not public

#### Overriding variables not permitted

Properties that are declared with the `var` or `const` keywords are inherited
but cannot be overridden. To override a property means to redefine the property
in a subclass. The only type of property that can be overridden are get and set
accessors (properties declared with the `function` keyword). Although you cannot
override an instance variable, you can achieve similar functionality by creating
getter and setter methods for the instance variable and overriding the methods.

## Overriding methods

To override a method means to redefine the behavior of an inherited method.
Static methods are not inherited and cannot be overridden. Instance methods,
however, are inherited by subclasses and can be overridden as long as the
following two criteria are met:

- The instance method is not declared with the `final` keyword in the base
  class. When used with an instance method, the `final` keyword indicates the
  programmer’s intent to prevent subclasses from overriding the method.

- The instance method is not declared with the `private` access control
  specifier in the base class. If a method is marked as `private` in the base
  class, there is no need to use the `override` keyword when defining an
  identically named method in the subclass, because the base class method is not
  visible to the subclass.

  To override an instance method that meets these criteria, the method
  definition in the subclass must use the `override` keyword and must match the
  superclass version of the method in the following ways:

- The override method must have the same level of access control as the base
  class method. Methods marked as internal have the same level of access control
  as methods that have no access control specifier.

- The override method must have the same number of parameters as the base class
  method.

- The override method parameters must have the same data type annotations as the
  parameters in the base class method.

- The override method must have the same return type as the base class method.

The names of the parameters in the override method, however, do not have to
match the names of the parameters in the base class, as long as the number of
parameters and the data type of each parameter matches.

#### The super statement

When overriding a method, programmers often want to add to the behavior of the
superclass method they are overriding instead of completely replacing the
behavior. This requires a mechanism that allows a method in a subclass to call
the superclass version of itself. The `super` statement provides such a
mechanism, in that it contains a reference to the immediate superclass. The
following example defines a class named Base that contains a method named
`thanks()` and a subclass of the Base class named Extender that overrides the
`thanks()` method. The `Extender.thanks()` method uses the `super` statement to
call `Base.thanks()`.

    package {
    import flash.display.MovieClip;
        public class SuperExample extends MovieClip
        {
            public function SuperExample()
            {
                var myExt:Extender = new Extender()
                trace(myExt.thanks()); // output: Mahalo nui loa
            }
        }
    }

    class Base {
        public function thanks():String
        {
            return "Mahalo";
        }
    }

    class Extender extends Base
    {
        override public function thanks():String
        {
            return super.thanks() + " nui loa";
        }
    }

#### Overriding getters and setters

Although you cannot override variables defined in a superclass, you can override
getters and setters. For example, the following code overrides a getter named
`currentLabel` that is defined in the MovieClip class in ActionScript 3.0.:

    package
    {
        import flash.display.MovieClip;
        public class OverrideExample extends MovieClip
        {
            public function OverrideExample()
            {
                trace(currentLabel)
            }
            override public function get currentLabel():String
            {
                var str:String = "Override: ";
                str += super.currentLabel;
                return str;
            }
        }
    }

The output of the `trace()` statement in the OverrideExample class constructor
is `Override: null`, which shows that the example was able to override the
inherited `currentLabel` property.

## Static properties not inherited

Static properties are not inherited by subclasses. This means that static
properties cannot be accessed through an instance of a subclass. A static
property can be accessed only through the class object on which it is defined.
For example, the following code defines a base class named Base and a subclass
that extends Base named Extender. A static variable named `test` is defined in
the Base class. The code as written in the following excerpt does not compile in
strict mode and generates a run-time error in standard mode.

    package {
        import flash.display.MovieClip;
        public class StaticExample extends MovieClip
        {
            public function StaticExample()
            {
                var myExt:Extender = new Extender();
                trace(myExt.test);// error
            }
        }
    }

    class Base {
        public static var test:String = "static";
    }

    class Extender extends Base { }

The only way to access the static variable `test` is through the class object,
as shown in the following code:

    Base.test;

It is permissible, however, to define an instance property using the same name
as a static property. Such an instance property can be defined in the same class
as the static property or in a subclass. For example, the Base class in the
preceding example could have an instance property named `test`. The following
code compiles and executes because the instance property is inherited by the
Extender class. The code would also compile and execute if the definition of the
test instance variable is moved, but not copied, to the Extender class.

    package
    {
        import flash.display.MovieClip;
        public class StaticExample extends MovieClip
        {
            public function StaticExample()
            {
                var myExt:Extender = new Extender();
                trace(myExt.test);// output: instance
            }
        }
    }

    class Base
    {
        public static var test:String = "static";
        public var test:String = "instance";
    }

    class Extender extends Base {}

## Static properties and the scope chain

Although static properties are not inherited, they are within the scope chain of
the class that defines them and any subclass of that class. As such, static
properties are said to be _in scope_ of both the class in which they are defined
and any subclasses. This means that a static property is directly accessible
within the body of the class that defines the static property and any subclass
of that class.

The following example modifies the classes defined in the previous example to
show that the static `test` variable defined in the Base class is in scope of
the Extender class. In other words, the Extender class can access the static
`test` variable without prefixing the variable with the name of the class that
defines `test`.

    package
    {
        import flash.display.MovieClip;
        public class StaticExample extends MovieClip
        {
            public function StaticExample()
            {
                var myExt:Extender = new Extender();
            }
        }
    }

    class Base {
        public static var test:String = "static";
    }

    class Extender extends Base
    {
        public function Extender()
        {
            trace(test); // output: static
        }

    }

If an instance property is defined that uses the same name as a static property
in the same class or a superclass, the instance property has higher precedence
in the scope chain. The instance property is said to _shadow_ the static
property, which means that the value of the instance property is used instead of
the value of the static property. For example, the following code shows that if
the Extender class defines an instance variable named `test`, the `trace()`
statement uses the value of the instance variable instead of the value of the
static variable.:

    package
    {
        import flash.display.MovieClip;
        public class StaticExample extends MovieClip
        {
            public function StaticExample()
            {
                var myExt:Extender = new Extender();
            }
        }
    }

    class Base
    {
        public static var test:String = "static";
    }

    class Extender extends Base
    {
        public var test:String = "instance";
        public function Extender()
        {
            trace(test); // output: instance
        }

    }
