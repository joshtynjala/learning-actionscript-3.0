# Introduction to ActionScript 3.0

## About ActionScript

ActionScript is the programming language for the Adobe® Flash® Player and Adobe®
AIR™ run-time environments. It enables interactivity, data handling, and much
more in Flash, Flex, and AIR content and applications.

ActionScript executes in the ActionScript Virtual Machine (AVM), which is part
of Flash Player and AIR. ActionScript code is typically transformed into
bytecode format by a compiler. (_Bytecode_ is a type of programming language
that’s written and understood by computers.) Examples of compilers include the
one built in to Adobe® Flash® Professional and the one that is built in to
Adobe® Flash® Builder™ and available in the Adobe® Flex™ SDK. The bytecode is
embedded in SWF files, which Flash Player and AIR execute.

ActionScript 3.0 offers a robust programming model that is familiar to
developers with a basic knowledge of object-oriented programming. Some of the
key features of ActionScript 3.0 that improve over previous ActionScript
versions include the following:

- A new ActionScript Virtual Machine, called AVM2, that uses a new bytecode
  instruction set and provides significant performance improvements

- A more modern compiler code base that performs deeper optimizations than
  previous versions of the compiler

- An expanded and improved application programming interface (API), with
  low-level control of objects and a true object-oriented model

- An XML API based on the ECMAScript for XML (E4X) specification (ECMA-357
  edition 2). E4X is a language extension to ECMAScript that adds XML as a
  native data type of the language.

- An event model based on the Document Object Model (DOM) Level 3 Events
  Specification

## Advantages of ActionScript 3.0

ActionScript 3.0 goes beyond the scripting capabilities of previous versions of
ActionScript. It is designed to facilitate the creation of highly complex
applications with large data sets and object-oriented, reusable code bases.
ActionScript 3.0 is not required for content that runs in Adobe Flash Player.
However, it opens the door to performance improvements that are only available
with the AVM2 (the ActionScript 3.0 virtual machine). ActionScript 3.0 code can
execute up to ten times faster than legacy ActionScript code.

The previous version of ActionScript Virtual Machine, AVM1, executes
ActionScript 1.0 and ActionScript 2.0 code. Flash Player 9 and 10 support AVM1
for backward compatibility.

## What’s new in ActionScript 3.0

ActionScript 3.0 contains many classes and features that are similar to
ActionScript 1.0 and 2.0. However, ActionScript 3.0 is architecturally and
conceptually different from previous versions of ActionScript. The enhancements
in ActionScript 3.0 include new features of the core language and an improved
API that provides increased control of low-level objects.

### Core language features

The core language defines the basic building blocks of the programming language,
such as statements, expressions, conditions, loops, and types. ActionScript 3.0
contains many features that speed up the development process.

#### Run-time exceptions

ActionScript 3.0 reports more error conditions than previous versions of
ActionScript. Run-time exceptions are used for common error conditions,
improving the debugging experience and enabling you to develop applications that
handle errors robustly. Run-time errors can provide stack traces annotated with
source file and line number information, helping you quickly pinpoint errors.

#### Run-time types

In ActionScript 3.0, type information is preserved at run time. This information
is used to perform run-time type checking, improving the system’s type safety.
Type information is also used to represent variables in native machine
representations, which improves performance and reduces memory usage. By way of
comparison, in ActionScript 2.0 type annotations are primarily a developer aid
and all values are dynamically typed at run time.

#### Sealed classes

ActionScript 3.0 includes the concept of sealed classes. A sealed class
possesses only the fixed set of properties and methods that are defined at
compile time; additional properties and methods cannot be added. The inability
of changing a class at run time enables stricter compile-time checking,
resulting in more robust programs. It also improves memory usage by not
requiring an internal hash table for each object instance. Dynamic classes are
also possible using the `dynamic` keyword. All classes in ActionScript 3.0 are
sealed by default, but can be declared to be dynamic with the `dynamic` keyword.

#### Method closures

ActionScript 3.0 enables a method closure to automatically remember its original
object instance. This feature is useful for event handling. In ActionScript 2.0,
method closures do not remember what object instance they were extracted from,
leading to unexpected behavior when the method closure is called.

#### ECMAScript for XML (E4X)

ActionScript 3.0 implements ECMAScript for XML (E4X), recently standardized as
ECMA-357. E4X offers a natural, fluent set of language constructs for
manipulating XML. In contrast to traditional XML-parsing APIs, XML with E4X
performs like a native data type of the language. E4X streamlines the
development of applications that manipulate XML by drastically reducing the
amount of code needed.

To view the ECMA E4X specification, go to
[www.ecma-international.org](https://ecma-international.org/publications-and-standards/standards/ecma-357/).

#### Regular expressions

ActionScript 3.0 includes native support for regular expressions so that you can
quickly search for and manipulate strings. ActionScript 3.0 implements support
for regular expressions as they are defined in the ECMAScript (ECMA-262) edition
3 language specification.

#### Namespaces

Namespaces are similar to the traditional access specifiers used to control
visibility of declarations (`public`, `private`, `protected`). They work as
custom access specifiers, which can have names of your choice. Namespaces are
outfitted with a Universal Resource Identifier (URI) to avoid collisions, and
are also used to represent XML namespaces when you work with E4X.

#### New primitive types

ActionScript 3.0 contains three numeric types: Number, int, and uint. Number
represents a double-precision, floating-point number. The int type is a 32-bit
signed integer that lets ActionScript code take advantage of the fast integer
math capabilities of the CPU. The int type is useful for loop counters and
variables where integers are used. The uint type is an unsigned, 32-bit integer
type that is useful for RGB color values, byte counts, and more. In contrast,
ActionScript 2.0 only has a single numeric type, Number.

### API features

The APIs in ActionScript 3.0 contain many classes that allow you to control
objects at a low level. The architecture of the language is designed to be more
intuitive than previous versions. While there are too many classes to cover in
detail, some significant differences are worth noting.

#### DOM3 event model

Document Object Model Level 3 event model (DOM3) provides a standard way of
generating and handling event messages. This event model is designed to allow
objects within applications to interact and communicate, maintain their state,
and respond to change. The ActionScript 3.0 event model is patterned after the
World Wide Web Consortium DOM Level 3 Events Specification. This model provides
a clearer and more efficient mechanism than the event systems available in
previous versions of ActionScript.

Events and error events are located in the flash.events package. The Flash
Professional components and Flex framework use the same event model, so the
event system is unified across the Flash Platform.

#### Display list API

The API for accessing the display list—the tree that contains any visual
elements in the application—consists of classes for working with visual
primitives.

The Sprite class is a lightweight building block, designed to be a base class
for visual elements such as user interface components. The Shape class
represents raw vector shapes. These classes can be instantiated naturally with
the `new` operator and can be dynamically reparented at any time.

Depth management is automatic. Methods are provided for specifying and managing
the stacking order of objects.

#### Handling dynamic data and content

ActionScript 3.0 contains mechanisms for loading and handling assets and data in
your application that are intuitive and consistent across the API. The Loader
class provides a single mechanism for loading SWF files and image assets and
provides a way to access detailed information about loaded content. The
URLLoaderclass provides a separate mechanism for loading text and binary data in
data-driven applications. The Socket class provides a means to read and write
binary data to server sockets in any format.

#### Low-level data access

Various APIs provide low-level access to data. For data that is being
downloaded, the URLStream class provides access to data as raw binary data while
it is being downloaded. The ByteArray class lets you optimize reading, writing,
and working with binary data. The sound API provides detailed control of sound
through the SoundChannel and SoundMixer classes. Security APIs provide
information about the security privileges of a SWF file or loaded content,
enabling you to handle security errors.

#### Working with text

ActionScript 3.0 contains a flash.text package for all text-related APIs. The
TextLineMetrics class provides detailed metrics for a line of text within a text
field; it replaces the `TextFormat.getTextExtent()` method in ActionScript 2.0.
The TextField class contains low-level methods that provide specific information
about a line of text or a single character in a text field. For example, the
`getCharBoundaries()` method returns a rectangle representing the bounding box
of a character. The `getCharIndexAtPoint()` method returns the index of the
character at a specified point. The `getFirstCharInParagraph()` method returns
the index of the first character in a paragraph. Line-level methods include
`getLineLength()`, which returns the number of characters in a specified line of
text, and `getLineText()`, which returns the text of the specified line. The
Font class provides a means to manage embedded fonts in SWF files.

For even lower-level control over text, the classes in the flash.text.engine
package make up the Flash Text Engine. This set of classes provide low-level
control over text and are designed for creating text frameworks and components.
