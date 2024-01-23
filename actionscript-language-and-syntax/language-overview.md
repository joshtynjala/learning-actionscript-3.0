# Language overview

Objects lie at the heart of the ActionScript 3.0 language—they are its
fundamental building blocks. Every variable you declare, every function you
write, and every class instance you create is an object. You can think of an
ActionScript 3.0 program as a group of objects that carry out tasks, respond to
events, and communicate with one another.

Programmers familiar with object-oriented programming (OOP) in Java or C++ may
think of objects as modules that contain two kinds of members: data stored in
member variables or properties, and behavior accessible through methods.
ActionScript 3.0 defines objects in a similar but slightly different way. In
ActionScript 3.0, objects are simply collections of properties. These properties
are containers that can hold not only data, but also functions or other objects.
If a function is attached to an object in this way, it is called a method.

While the ActionScript 3.0 definition may seem a little odd to programmers with
a Java or C++ background, in practice, defining object types with ActionScript
3.0 classes is very similar to the way classes are defined in Java or C++. The
distinction between the two definitions of object is important when discussing
the ActionScript object model and other advanced topics, but in most other
situations the term _properties_ means class member variables as opposed to
methods. ActionScript 3.0 Reference for the Adobe Flash Platform, for example,
uses the term _properties_ to mean variables or getter-setter properties. It
uses the term _methods_ to mean functions that are part of a class.

One subtle difference between classes in ActionScript and classes in Java or C++
is that in ActionScript, classes are not just abstract entities. ActionScript
classes are represented by _class objects_ that store the class’s properties and
methods. This allows for techniques that may seem alien to Java and C++
programmers, such as including statements or executable code at the top level of
a class or package.

Another difference between ActionScript classes and Java or C++ classes is that
every ActionScript class has something called a _prototypeobject_. In previous
versions of ActionScript, prototype objects, linked together into _prototype
chains,_ served collectively as the foundation of the entire class inheritance
hierarchy. In ActionScript 3.0, however, prototype objects play only a small
role in the inheritance system. The prototype object can still be useful,
however, as an alternative to static properties and methods if you want to share
a property and its value among all the instances of a class.

In the past, advanced ActionScript programmers could directly manipulate the
prototype chain with special built-in language elements. Now that the language
provides a more mature implementation of a class-based programming interface,
many of these special language elements, such as `__proto__` and `__resolve,`
are no longer part of the language. Moreover, optimizations of the internal
inheritance mechanism that provide significant performance improvements preclude
direct access to the inheritance mechanism.
