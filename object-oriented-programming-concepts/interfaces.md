# Interfaces

An interface is a collection of method declarations that allows unrelated
objects to communicate with one another. For example, ActionScript 3.0 defines
the IEventDispatcher interface, which contains method declarations that a class
can use to handle event objects. The IEventDispatcher interface establishes a
standard way for objects to pass event objects to one another. The following
code shows the definition of the IEventDispatcher interface:

    public interface IEventDispatcher
    {
    function addEventListener(type:String, listener:Function,
            useCapture:Boolean=false, priority:int=0,
            useWeakReference:Boolean = false):void;
    function removeEventListener(type:String, listener:Function,
            useCapture:Boolean=false):void;
    function dispatchEvent(event:Event):Boolean;
    function hasEventListener(type:String):Boolean;
    function willTrigger(type:String):Boolean;
    }

Interfaces are based on the distinction between a method’s interface and its
implementation. A method’s interface includes all the information necessary to
call that method, including the name of the method, all of its parameters, and
its return type. A method’s implementation includes not only the interface
information, but also the executable statements that carry out the method’s
behavior. An interface definition contains only method interfaces, and any class
that implements the interface is responsible for defining the method
implementations.

In ActionScript 3.0, the EventDispatcher class implements the IEventDispatcher
interface by defining all of the IEventDispatcher interface methods and adding
method bodies to each of the methods. The following code is an excerpt from the
EventDispatcher class definition:

    public class EventDispatcher implements IEventDispatcher
    {
    function dispatchEvent(event:Event):Boolean
    {
        /* implementation statements */
    }

    ...
    }

The IEventDispatcher interface serves as a protocol that EventDispatcher
instances use to process event objects and pass them to other objects that have
also implemented the IEventDispatcher interface.

Another way to describe an interface is to say that it defines a data type just
as a class does. Accordingly, an interface can be used as a type annotation,
just as a class can. As a data type, an interface can also be used with
operators, such as the `is` and `as` operators, that require a data type. Unlike
a class, however, an interface cannot be instantiated. This distinction has led
many programmers to think of interfaces as abstract data types and classes as
concrete data types.

## Defining an interface

The structure of an interface definition is similar to that of a class
definition, except that an interface can contain only methods with no method
bodies. Interfaces cannot include variables or constants but can include getters
and setters. To define an interface, use the `interface` keyword. For example,
the following interface, IExternalizable, is part of the flash.utils package in
ActionScript 3.0. The IExternalizable interface defines a protocol for
serializing an object, which means converting an object into a format suitable
for storage on a device or for transport across a network.

    public interface IExternalizable
    {
    function writeExternal(output:IDataOutput):void;
    function readExternal(input:IDataInput):void;
    }

The IExternalizable interface is declared with the `public` access control
modifier. Interface definitions can only be modified by the `public` and
`internal` access control specifiers. The method declarations inside an
interface definition cannot have any access control specifiers.

ActionScript 3.0 follows a convention in which interface names begin with an
uppercase `I`, but you can use any legal identifier as an interface name.
Interface definitions are often placed at the top level of a package. Interface
definitions cannot be placed inside a class definition or inside another
interface definition.

Interfaces can extend one or more other interfaces. For example, the following
interface, IExample, extends the IExternalizable interface:

    public interface IExample extends IExternalizable
    {
    function extra():void;
    }

Any class that implements the IExample interface must include implementations
not only for the `extra()` method, but also for the `writeExternal()` and
`readExternal()` methods inherited from the IExternalizable interface.

## Implementing an interface in a class

A class is the only ActionScript 3.0 language element that can implement an
interface. Use the `implements` keyword in a class declaration to implement one
or more interfaces. The following example defines two interfaces, IAlpha and
IBeta `,` and a class, Alpha, that implements them both:

    interface IAlpha
    {
    function foo(str:String):String;
    }

    interface IBeta
    {
    function bar():void;
    }

    class Alpha implements IAlpha, IBeta
    {
    public function foo(param:String):String {}
    public function bar():void {}
    }

In a class that implements an interface, implemented methods must do the
following:

- Use the `public` access control identifier.

- Use the same name as the interface method.

- Have the same number of parameters, each with data types that match the
  interface method parameter data types.

- Use the same return type.

      public function foo(param:String):String {}

You do have some flexibility, however, in how you name the parameters of methods
that you implement. Although the number of parameters and the data type of each
parameter in the implemented method must match that of the interface method, the
parameter names do not need to match. For example, in the previous example the
parameter of the `Alpha.foo()` method is named `param`:

But the parameter is named `str` in the `IAlpha.foo()` interface method:

    function foo(str:String):String;

You also have some flexibility with default parameter values. An interface
definition can include function declarations with default parameter values. A
method that implements such a function declaration must have a default parameter
value that is a member of the same data type as the value specified in the
interface definition, but the actual value does not have to match. For example,
the following code defines an interface that contains a method with a default
parameter value of 3:

    interface IGamma
    {
    function doSomething(param:int = 3):void;
    }

The following class definition implements the IGamma interface but uses a
different default parameter value:

    class Gamma implements IGamma
    {
    public function doSomething(param:int = 4):void {}
    }

The reason for this flexibility is that the rules for implementing an interface
are designed specifically to ensure data type compatibility, and requiring
identical parameter names and default parameter values is not necessary to
achieve that objective.
