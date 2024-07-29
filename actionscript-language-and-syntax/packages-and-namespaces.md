# Packages and namespaces

Packages and namespaces are related concepts. Packages allow you to bundle class
definitions together in a way that facilitates code sharing and minimizes naming
conflicts. Namespaces allow you to control the visibility of identifiers, such
as property and method names, and can be applied to code whether it resides
inside or outside a package. Packages let you organize your class files, and
namespaces let you manage the visibility of individual properties and methods.

## Packages

Packages in ActionScript 3.0 are implemented with namespaces, but are not
synonymous with them. When you declare a package, you are implicitly creating a
special type of namespace that is guaranteed to be known at compile time.
Namespaces, when created explicitly, are not necessarily known at compile time.

The following example uses the `package` directive to create a simple package
containing one class:

    package samples
    {
        public class SampleCode
        {
            public var sampleGreeting:String;
            public function sampleFunction()
            {
                trace(sampleGreeting + " from sampleFunction()");
            }
        }
    }

The name of the class in this example is SampleCode. Because the class is inside
the samples package, the compiler automatically qualifies the class name at
compile time into its fully qualified name: samples.SampleCode. The compiler
also qualifies the names of any properties or methods, so that `sampleGreeting`
and `sampleFunction()` become `samples.SampleCode.sampleGreeting` and
`samples.SampleCode.sampleFunction()`, respectively.

Many developers, especially those with Java programming backgrounds, may choose
to place only classes at the top level of a package. ActionScript 3.0, however,
supports not only classes at the top level of a package, but also variables,
functions, and even statements. One advanced use of this feature is to define a
namespace at the top level of a package so that it is available to all classes
in that package. Note, however, that only two access specifiers, `public` and
`internal`, are allowed at the top level of a package. Unlike Java, which allows
you to declare nested classes as private, ActionScript 3.0 doesn’t support
nested or private classes.

In many other ways, however, ActionScript 3.0 packages are similar to packages
in the Java programming language. As you can see in the previous example, fully
qualified package references are expressed using the dot operator (`.`), just as
they are in Java. You can use packages to organize your code into an intuitive
hierarchical structure for use by other programmers. This facilitates code
sharing by allowing you to create your own package to share with others, and to
use packages created by others in your code.

The use of packages also helps to ensure that the identifier names that you use
are unique and do not conflict with other identifier names. In fact, some would
argue that this is the primary benefit of packages. For example, two programmers
who want to share their code with each other may have each created a class
called SampleCode. Without packages, this would create a name conflict, and the
only resolution would be to rename one of the classes. With packages, however,
the name conflict is easily avoided by placing one, or preferably both, of the
classes in packages with unique names.

You can also include embedded dots in your package name to create nested
packages. This allows you to create a hierarchical organization of packages. A
good example of this is the flash.display package provided by ActionScript 3.0.
The flash.display package is nested inside the flash package.

Most of ActionScript 3.0 is organized under the flash package. For example, the
flash.display package contains the display list API, and the flash.events
package contains the new event model.

## Creating packages

ActionScript 3.0 provides significant flexibility in the way you organize your
packages, classes, and source files. Previous versions of ActionScript allowed
only one class per source file and required the name of the source file to match
the name of the class. ActionScript 3.0 allows you to include multiple classes
in one source file, but only one class in each file can be made available to
code that is external to that file. In other words, only one class in each file
can be declared inside a package declaration. You must declare any additional
classes outside your package definition, which makes those classes invisible to
code outside that source file. The name of the class declared inside the package
definition must match the name of the source file.

ActionScript 3.0 also provides more flexibility in the way you declare packages.
In previous versions of ActionScript, packages merely represented directories in
which you placed source files, and you didn’t declare packages with the
`package` statement, but rather included the package name as part of the fully
qualified class name in your class declaration. Although packages still
represent directories in ActionScript 3.0, packages can contain more than just
classes. In ActionScript 3.0, you use the `package` statement to declare a
package, which means that you can also declare variables, functions, and
namespaces at the top level of a package. You can even include executable
statements at the top level of a package. If you do declare variables,
functions, or namespaces at the top level of a package, the only attributes
available at that level are `public` and `internal`, and only one package-level
declaration per file can use the `public` attribute, whether that declaration is
a class, variable, function, or namespace.

Packages are useful for organizing your code and for preventing name conflicts.
You should not confuse the concept of packages with the unrelated concept of
class inheritance. Two classes that reside in the same package have a namespace
in common, but are not necessarily related to each other in any other way.
Likewise, a nested package may have no semantic relationship to its parent
package.

## Importing packages

If you want to use a class that is inside a package, you must import either the
package or the specific class. This differs from ActionScript 2.0, where
importing classes was optional.

For example, consider the SampleCode class example presented previously. If the
class resides in a package named samples, you must use one of the following
import statements before using the SampleCode class:

    import samples.*;

or

    import samples.SampleCode;

In general, `import` statements should be as specific as possible. If you plan
to use only the SampleCode class from the samples package, you should import
only the SampleCode class rather than the entire package to which it belongs.
Importing entire packages may lead to unexpected name conflicts.

You must also place the source code that defines the package or class within
your _classpath_. The classpath is a user-defined list of local directory paths
that determines where the compiler searches for imported packages and classes.
The classpath is sometimes called the _build path_ or _source path_.

After you have properly imported the class or package, you can use either the
fully qualified name of the class (samples.SampleCode) or merely the class name
by itself (SampleCode).

Fully qualified names are useful when identically named classes, methods, or
properties result in ambiguous code, but can be difficult to manage if used for
all identifiers. For example, the use of the fully qualified name results in
verbose code when you instantiate a SampleCode class instance:

    var mySample:samples.SampleCode = new samples.SampleCode();

As the levels of nested packages increase, the readability of your code
decreases. In situations where you are confident that ambiguous identifiers are
not a problem, you can make your code easier to read by using simple
identifiers. For example, instantiating a new instance of the SampleCode class
is much less verbose if you use only the class identifier:

    var mySample:SampleCode = new SampleCode();

If you attempt to use identifier names without first importing the appropriate
package or class, the compiler can’t find the class definitions. On the other
hand, if you do import a package or class, any attempt to define a name that
conflicts with an imported name generates an error.

When a package is created, the default access specifier for all members of that
package is `internal`, which means that, by default, package members are only
visible to other members of that package. If you want a class to be available to
code outside the package, you must declare that class to be `public`. For
example, the following package contains two classes, SampleCode and
CodeFormatter:

    // SampleCode.as file
    package samples
    {
        public class SampleCode {}
    }

    // CodeFormatter.as file
    package samples
    {
        class CodeFormatter {}
    }

The SampleCode class is visible outside the package because it is declared as a
`public` class. The CodeFormatter class, however, is visible only within the
samples package itself. If you attempt to access the CodeFormatter class outside
the samples package, it generates an error, as the following example shows:

    import samples.SampleCode;
    import samples.CodeFormatter;
    var mySample:SampleCode = new SampleCode(); // okay, public class
    var myFormatter:CodeFormatter = new CodeFormatter(); // error

If you want both classes to be available outside the package, you must declare
both classes to be `public`. You cannot apply the `public` attribute to the
package declaration.

Fully qualified names are useful for resolving name conflicts that may occur
when using packages. Such a scenario may arise if you import two packages that
define classes with the same identifier. For example, consider the following
package, which also has a class named SampleCode:

    package langref.samples
    {
        public class SampleCode {}
    }

If you import both classes, as follows, you have a name conflict when using the
SampleCode class:

    import samples.SampleCode;
    import langref.samples.SampleCode;
    var mySample:SampleCode = new SampleCode(); // name conflict

The compiler has no way of knowing which SampleCode class to use. To resolve
this conflict, you must use the fully qualified name of each class, as follows:

    var sample1:samples.SampleCode = new samples.SampleCode();
    var sample2:langref.samples.SampleCode = new langref.samples.SampleCode();

> **Note:** Programmers with a C++ background often confuse the `import`
> statement with `#include`. The `#include` directive is necessary in C++
> because C++ compilers process one file at a time, and don’t look in other
> files for class definitions unless a header file is explicitly included.
> ActionScript 3.0 has an `include` directive, but it is not designed to import
> classes and packages. To import classes or packages in ActionScript 3.0, you
> must use the `import` statement and place the source file that contains the
> package in the class path.

## Namespaces

Namespaces give you control over the visibility of the properties and methods
that you create. Think of the `public`, `private`, `protected,` and `internal`
access control specifiers as built-in namespaces. If these predefined access
control specifiers do not suit your needs, you can create your own namespaces.

If you are familiar with XML namespaces, much of this discussion will not be new
to you, although the syntax and details of the ActionScript implementation are
slightly different from those of XML. If you have never worked with namespaces
before, the concept itself is straightforward, but the implementation has
specific terminology that you will need to learn.

To understand how namespaces work, it helps to know that the name of a property
or method always contains two parts: an identifier and a namespace. The
identifier is what you generally think of as a name. For example, the
identifiers in the following class definition are `sampleGreeting` and
`sampleFunction()`:

    class SampleCode
    {
        var sampleGreeting:String;
        function sampleFunction () {
            trace(sampleGreeting + " from sampleFunction()");
        }
    }

Whenever definitions are not preceded by a namespace attribute, their names are
qualified by the default `internal` namespace, which means they are visible only
to callers in the same package. If the compiler is set to strict mode, the
compiler issues a warning that the `internal` namespace applies to any
identifier without a namespace attribute. To ensure that an identifier is
available everywhere, you must specifically precede the identifier name with the
`public` attribute. In the previous example code, both `sampleGreeting` and
`sampleFunction()` have a namespace value of `internal`.

There are three basic steps to follow when using namespaces. First, you must
define the namespace using the `namespace` keyword. For example, the following
code defines the `version1` namespace:

    namespace version1;

Second, you apply your namespace by using it instead of an access control
specifier in a property or method declaration. The following example places a
function named `myFunction()` into the `version1` namespace:

    version1 function myFunction() {}

Third, once you’ve applied the namespace, you can reference it with the `use`
directive or by qualifying the name of an identifier with a namespace. The
following example references the `myFunction()` function through the `use`
directive:

    use namespace version1;
    myFunction();

You can also use a qualified name to reference the `myFunction()` function, as
the following example shows:

    version1::myFunction();

#### Defining namespaces

Namespaces contain one value, the Uniform Resource Identifier (URI), which is
sometimes called the _namespace name_. A URI allows you to ensure that your
namespace definition is unique.

You create a namespace by declaring a namespace definition in one of two ways.
You can either define a namespace with an explicit URI, as you would define an
XML namespace, or you can omit the URI. The following example shows how a
namespace can be defined using a URI:

    namespace flash_proxy = "http://www.adobe.com/flash/proxy";

The URI serves as a unique identification string for that namespace. If you omit
the URI, as in the following example, the compiler creates a unique internal
identification string in place of the URI. You do not have access to this
internal identification string.

    namespace flash_proxy;

Once you define a namespace, with or without a URI, that namespace cannot be
redefined in the same scope. An attempt to define a namespace that has been
defined earlier in the same scope results in a compiler error.

If a namespace is defined within a package or a class, the namespace may not be
visible to code outside that package or class unless the appropriate access
control specifier is used. For example, the following code shows the
`flash_proxy` namespace defined within the flash.utils package. In the following
example, the lack of an access control specifier means that the `flash_proxy`
namespace would be visible only to code within the flash.utils package and would
not be visible to any code outside the package:

    package flash.utils
    {
        namespace flash_proxy;
    }

The following code uses the `public` attribute to make the `flash_proxy`
namespace visible to code outside the package:

    package flash.utils
    {
        public namespace flash_proxy;
    }

#### Applying namespaces

Applying a namespace means placing a definition into a namespace. Definitions
that can be placed into namespaces include functions, variables, and constants
(you cannot place a class into a custom namespace).

Consider, for example, a function declared using the `public` access control
namespace. Using the `public` attribute in a function definition places the
function into the public namespace, which makes the function available to all
code. Once you have defined a namespace, you can use the namespace that you
defined the same way you would use the `public` attribute, and the definition is
available to code that can reference your custom namespace. For example, if you
define a namespace `example1`, you can add a method called `myFunction()`using
`example1` as an attribute, as the following example shows:

    namespace example1;
    class someClass
    {
        example1 myFunction() {}
    }

Declaring the `myFunction()` method using the namespace `example1` as an
attribute means that the method belongs to the `example1` namespace.

You should bear in mind the following when applying namespaces:

- You can apply only one namespace to each declaration.

- There is no way to apply a namespace attribute to more than one definition at
  a time. In other words, if you want to apply your namespace to ten different
  functions, you must add your namespace as an attribute to each of the ten
  function definitions.

- If you apply a namespace, you cannot also specify an access control specifier
  because namespaces and access control specifiers are mutually exclusive. In
  other words, you cannot declare a function or property as `public`, `private`,
  `protected,` or `internal` in addition to applying your namespace.

#### Referencing namespaces

There is no need to explicitly reference a namespace when you use a method or
property declared with any of the access control namespaces, such as `public`,
`private`, `protected`, and `internal`. This is because access to these special
namespaces is controlled by context. For example, definitions placed into the
`private` namespace are automatically available to code within the same class.
For namespaces that you define, however, such context sensitivity does not
exist. To use a method or property that you have placed into a custom namespace,
you must reference the namespace.

You can reference namespaces with the `use namespace` directive or you can
qualify the name with the namespace using the name qualifier (`::`) punctuator.
Referencing a namespace with the `use namespace` directive “opens” the
namespace, so that it can apply to any identifiers that are not qualified. For
example, if you have defined the `example1` namespace, you can access names in
that namespace by using `use namespace example1`:

    use namespace example1;
    myFunction();

You can open more than one namespace at a time. Once you open a namespace with
`use namespace`, it remains open throughout the block of code in which it was
opened. There is no way to explicitly close a namespace.

Having more than one open namespace, however, increases the likelihood of name
conflicts. If you prefer not to open a namespace, you can avoid the
`use namespace` directive by qualifying the method or property name with the
namespace and the name qualifier punctuator. For example, the following code
shows how you can qualify the name `myFunction()` with the `example1` namespace:

    example1::myFunction();

#### Using namespaces

You can find a real-world example of a namespace that is used to prevent name
conflicts in the flash.utils.Proxy class that is part of ActionScript 3.0. The
Proxy class, which is the replacement for the `Object.__resolve` property from
ActionScript 2.0, allows you to intercept references to undefined properties or
methods before an error occurs. All of the methods of the Proxy class reside in
the `flash_proxy` namespace to prevent name conflicts.

To better understand how the `flash_proxy` namespace is used, you need to
understand how to use the Proxy class. The functionality of the Proxy class is
available only to classes that inherit from it. In other words, if you want to
use the methods of the Proxy class on an object, the object’s class definition
must extend the Proxy class. For example, if you want to intercept attempts to
call an undefined method, you would extend the Proxy class and then override the
`callProperty()` method of the Proxy class.

You may recall that implementing namespaces is usually a three-step process of
defining, applying, and then referencing a namespace. Because you never
explicitly call any of the Proxy class methods, however, the `flash_proxy`
namespace is only defined and applied, but never referenced. ActionScript 3.0
defines the `flash_proxy` namespace and applies it in the Proxy class. Your code
only needs to apply the `flash_proxy` namespace to classes that extend the Proxy
class.

The `flash_proxy` namespace is defined in the flash.utils package in a manner
similar to the following:

    package flash.utils
    {
        public namespace flash_proxy;
    }

The namespace is applied to the methods of the Proxy class as shown in the
following excerpt from the Proxy class:

    public class Proxy
    {
        flash_proxy function callProperty(name:*, ... rest):*
        flash_proxy function deleteProperty(name:*):Boolean
        ...
    }

As the following code shows, you must first import both the Proxy class and the
`flash_proxy` namespace. You must then declare your class such that it extends
the Proxy class (you must also add the `dynamic` attribute if you are compiling
in strict mode). When you override the `callProperty()` method, you must use the
`flash_proxy` namespace.

    package
    {
        import flash.utils.Proxy;
        import flash.utils.flash_proxy;

        dynamic class MyProxy extends Proxy
        {
            flash_proxy override function callProperty(name:*, ...rest):*
            {
                trace("method call intercepted: " + name);
            }
        }
    }

If you create an instance of the MyProxy class and call an undefined method,
such as the `testing()` method called in the following example, your Proxy
object intercepts the method call and executes the statements inside the
overridden `callProperty()` method (in this case, a simple `trace()` statement).

    var mySample:MyProxy = new MyProxy();
    mySample.testing(); // method call intercepted: testing

There are two advantages to having the methods of the Proxy class inside the
`flash_proxy` namespace. First, having a separate namespace reduces clutter in
the public interface of any class that extends the Proxy class. (There are about
a dozen methods in the Proxy class that you can override, all of which are not
designed to be called directly. Placing all of them in the public namespace
could be confusing.) Second, use of the `flash_proxy` namespace avoids name
conflicts in case your Proxy subclass contains instance methods with names that
match any of the Proxy class methods. For example, you may want to name one of
your own methods `callProperty()`. The following code is acceptable, because
your version of the `callProperty()` method is in a different namespace:

    dynamic class MyProxy extends Proxy
    {
        public function callProperty() {}
        flash_proxy override function callProperty(name:*, ...rest):*
        {
            trace("method call intercepted: " + name);
        }
    }

Namespaces can also be helpful when you want to provide access to methods or
properties in a way that cannot be accomplished with the four access control
specifiers (`public`, `private`, `internal`, and `protected`). For example, you
may have a few utility methods that are spread out across several packages. You
want these methods available to all of your packages, but you don’t want the
methods to be public. To accomplish this, you can create a namespace and use it
as your own special access control specifier.

The following example uses a user-defined namespace to group two functions that
reside in different packages. By grouping them into the same namespace, you can
make both functions visible to a class or package through a single
`use namespace` statement.

This example uses four files to demonstrate the technique. All of the files must
be within your classpath. The first file, myInternal.as, is used to define the
`myInternal` namespace. Because the file is in a package named example, you must
place the file into a folder named example. The namespace is marked as `public`
so that it can be imported into other packages.

    // myInternal.as in folder example
    package example
    {
        public namespace myInternal = "http://www.adobe.com/2006/actionscript/examples";
    }

The second and third files, Utility.as and Helper.as, define the classes that
contain methods that should be available to other packages. The Utility class is
in the example.alpha package, which means that the file should be placed inside
a folder named alpha that is a subfolder of the example folder. The Helper class
is in the example.beta package, which means that the file should be placed
inside a folder named beta that is also a subfolder of the example folder. Both
of these packages, example.alpha and example.beta, must import the namespace
before using it.

    // Utility.as in the example/alpha folder
    package example.alpha
    {
        import example.myInternal;

        public class Utility
        {
            private static var _taskCounter:int = 0;

            public static function someTask()
            {
                _taskCounter++;
            }

            myInternal static function get taskCounter():int
            {
                return _taskCounter;
            }
        }
    }

    // Helper.as in the example/beta folder
    package example.beta
    {
        import example.myInternal;

        public class Helper
        {
            private static var _timeStamp:Date;

            public static function someTask()
            {
                _timeStamp = new Date();
            }

            myInternal static function get lastCalled():Date
            {
                return _timeStamp;
            }
        }
    }

The fourth file, NamespaceUseCase.as, is the main application class, and should
be a sibling to the example folder. In Flash Professional, this class would be
used as the document class for the FLA. The NamespaceUseCase class also imports
the `myInternal` namespace and uses it to call the two static methods that
reside in the other packages. The example uses static methods only to simplify
the code. Both static and instance methods can be placed in the `myInternal`
namespace.

    // NamespaceUseCase.as
    package
    {
        import flash.display.MovieClip;
        import example.myInternal; // import namespace
        import example.alpha.Utility;// import Utility class
        import example.beta.Helper;// import Helper class

        public class NamespaceUseCase extends MovieClip
        {
            public function NamespaceUseCase()
            {
                use namespace myInternal;

                Utility.someTask();
                Utility.someTask();
                trace(Utility.taskCounter); // 2

                Helper.someTask();
                trace(Helper.lastCalled); // [time someTask() was last called]
            }
        }
    }
