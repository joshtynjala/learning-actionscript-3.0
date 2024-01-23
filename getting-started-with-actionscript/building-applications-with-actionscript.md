# Building applications with ActionScript

The process of writing ActionScript to build an application involves more than
just knowing the syntax and the names of the classes you’ll use. Most of the
Flash Platform documentation covers those two topics (syntax and using
ActionScript classes). However, to build an ActionScript application you’ll also
want to know information such as:

- What programs can be used for writing ActionScript?

- How do you organize ActionScript code?

- How do you include ActionScript code in an application?

- What steps do you follow in developing an ActionScript application?

## Options for organizing your code

You can use ActionScript 3.0 code to power everything from simple graphics
animations to complex client-server transaction processing systems. Depending on
the type of application you’re building, use one or more of these different ways
of including ActionScript in your project.

#### Storing code in frames in a Flash Professional timeline

In Flash Professional, you can add ActionScript code to any frame in a timeline.
This code executes while the movie is playing back, when the playhead enters
that frame.

Placing ActionScript code in frames provides a simple way to add behaviors to
applications built in Flash Professional. You can add code to any frame in the
main timeline or to any frame in the timeline of any MovieClip symbol. However,
this flexibility comes with a cost. When you build larger applications, it
becomes easy to lose track of which frames contain which scripts. This
complicated structure can make the application more difficult to maintain over
time.

Many developers simplify the organization of their ActionScript code in the
Flash Professional by placing code only in the first frame of a timeline or on a
specific layer in the Flash document. Separating your code makes it easier to
locate and maintain the code in your Flash FLA files. However, the same code
can’t be used in another Flash Professional project without copying and pasting
the code into the new file.

To make it easier to use your ActionScript code in other Flash Professional
projects in the future, store your code in external ActionScript files (text
files with the .as extension).

#### Embedding code in Flex MXML files

In a Flex development environment such as Flash Builder, you can include
ActionScript code inside an `<fx:Script>` tag in a Flex MXML file. However, this
technique can add complexity to large projects and make it more difficult to use
the same code in another Flex project. To make it easier to use your
ActionScript code in other Flex projects in the future, store your code in
external ActionScript files.

Note: You can specify a source parameter for an `<fx:Script>` tag. Using a
source parameter lets you “import” ActionScript code from an external file as if
it was typed directly within the `<fx:Script>` tag. However, the source file
that you use cannot define its own class, which limits its reusability.

#### Storing code in ActionScript files

If your project involves significant ActionScript code, the best way to organize
your code is in separate ActionScript source files (text files with the .as
extension). An ActionScript file can be structured in one of two ways, depending
on how you intend to use it in your application.

- Unstructured ActionScript code: Lines of ActionScript code, including
  statements or function definitions, written as though they were entered
  directly in a timeline script or MXML file.

  ActionScript written in this way can be accessed using the `include` statement
  in ActionScript, or the `<fx:Script>` tag in Flex MXML. The ActionScript
  `include` statement tells the compiler to include the contents of an external
  ActionScript file at a specific location and within a given scope in a script.
  The result is the same as if the code were entered there directly. In the MXML
  language, using an `<fx:Script>` tag with a source attribute identifies an
  external ActionScript that the compiler loads at that point in the
  application. For example, the following tag loads an external ActionScript
  file named Box.as:

      <fx:Script source="Box.as" />

- ActionScript class definition: A definition of an ActionScript class,
  including its method and property definitions.

  When you define a class you can access the ActionScript code in the class by
  creating an instance of the class and using its properties, methods, and
  events. Using your own classes is identical to using any of the built-in
  ActionScript classes, and requires two parts:

  - Use the `import` statement to specify the full name of the class, so the
    ActionScript compiler knows where to find it. For example, to use the
    MovieClip class in ActionScript, import the class using its full name,
    including package and class:

        import flash.display.MovieClip;

    Alternatively, you can import the package that contains the MovieClip class,
    which is equivalent to writing separate `import` statements for each class
    in the package:

        import flash.display.*;

    The top-level classes are the only exception to the rule that a class must
    be imported to use that class in your code. Those classes are not defined in
    a package.

  - Write code that specifically uses the class name. For example, declare a
    variable with that class as its data type and create an instance of the
    class to store in the variable. By using a class in ActionScript code, you
    tell the compiler to load the definition of that class. For example, given
    an external class called Box, this statement creates an instance of the Box
    class:

        var smallBox:Box = new Box(10,20);

    The first time the compiler comes across the reference to the Box class it
    searches the available source code to locate the Box class definition.

## Choosing the right tool

You can use one of several tools (or multiple tools together) for writing and
editing your ActionScript code.

#### Flash Builder

Adobe Flash Builder is the premier tool for creating projects with the Flex
framework or projects that primarily consist of ActionScript code. Flash Builder
also includes a full-featured ActionScript editor as well as visual layout and
MXML editing capabilities. It can be used to create Flex or ActionScript-only
projects. Flex provides several benefits including a rich set of pre-built user
interface controls, flexible dynamic layout controls, and built-in mechanisms
for working with remote data and linking external data to user interface
elements. However, because of the additional code required to provide these
features, projects that use Flex can have a larger SWF file size than their
non-Flex counterparts.

Use Flash Builder if you are creating full-featured data-driven rich Internet
applications with Flex. Use it when you want to edit ActionScript code, edit
MXML code, and lay out your application visually, all within a single tool.

Many Flash Professional users who build ActionScript-heavy projects use Flash
Professional to create visual assets and Flash Builder as an editor for
ActionScript code.

#### Flash Professional

In addition to its graphics and animation creation capabilities, Flash
Professional includes tools for working with ActionScript code. The code can
either be attached to elements in a FLA file or in external ActionScript-only
files. Flash Professional is ideal for projects that involve significant
animation or video. It is valuable when you want to create most of the graphic
assets yourself. Another reason to use Flash Professional to develop your
ActionScript project is to create visual assets and write code in the same
application. Flash Professional also includes pre-built user interface
components. You can use those components to achieve smaller SWF file size and
use visual tools to skin them for your project.

Flash Professional includes two tools for writing ActionScript code:

- Actions panel: Available when working in a FLA file, this panel allows you to
  write ActionScript code attached to frames on a timeline.

- Script window: The Script window is a dedicated text editor for working with
  ActionScript (.as) code files.

#### Third-party ActionScript editor

Because ActionScript (.as) files are stored as simple text files, any program
that can edit plain text files can be used to write ActionScript files. In
addition to Adobe’s ActionScript products, several third-party text editing
programs with ActionScript-specific capabilities have been created. You can
write an MXML file or ActionScript classes using any text editor program. You
can then create an application from those files using the Flex SDK. The project
can use Flex or be an ActionScript-only application. Alternatively, some
developers use Flash Builder or a third-party ActionScript editor for writing
ActionScript classes, in combination with Flash Professional for creating
graphical content.

Reasons to choose a third-party ActionScript editor include:

- You prefer to write ActionScript code in a separate program and design visual
  elements in Flash Professional.

- You use an application for non-ActionScript programming (such as creating HTML
  pages or building applications in another programming language). You want to
  use the same application for your ActionScript coding as well.

- You want to create ActionScript-only or Flex projects using the Flex SDK
  without Flash Professional or Flash Builder.

Some of the notable code editors providing ActionScript-specific support
include:

- [Adobe Dreamweaver®](https://www.adobe.com/products/dreamweaver.html)

- [ASDT](https://sourceforge.net/projects/aseclipseplugin/)

- [FDT](https://fdt.powerflasher.com/)

- [FlashDevelop](https://www.flashdevelop.org)

- [PrimalScript](https://www.sapien.com/software/primalscript)

- [SE\|PY](https://sourceforge.net/projects/sepy/)

- [TextMate](https://macromates.com/)

- [Visual Studio Code](https://code.visualstudio.com/) (with
  [AS3, MXML, & SWF extension pack](https://marketplace.visualstudio.com/items?itemName=bowlerhatllc.vscode-nextgenas))

## The ActionScript development process

Whether your ActionScript project is large or small, using a process to design
and develop your application makes work more efficient and effective. The
following steps describe a basic development process for building an application
that uses ActionScript 3.0:

1.  Design your application.

    Describe your application in some way before you start building it.

2.  Compose your ActionScript 3.0 code.

    You can create ActionScript code using Flash Professional, Flash Builder,
    Dreamweaver, or a text editor.

3.  Create a Flash or Flex project to run your code.

    In Flash Professional, create a FLA file, set up the publish settings, add
    user interface components to the application, and reference the ActionScript
    code. In Flex, define the application, add user interface components using
    MXML, and reference the ActionScript code.

4.  Publish and test your ActionScript application.

    Testing your application involves running your application from within your
    development environment and making sure that it does everything you
    intended.

You don’t necessarily have to follow these steps in order, or completely finish
one step before working on another. For example, you can design one screen of
your application (step 1) and then create the graphics, buttons, and so on
(step 3) before writing ActionScript code (step 2) and testing (step 4). Or you
can design part of it and then add one button or interface element at a time,
writing ActionScript for each one and testing it as it’s built. It’s helpful to
remember these four stages of the development process. However, in real-world
development it’s more effective to move back and forth among the stages as
appropriate.

<div style="position: absolute; height: 1px; width: 1px; top: -1000px; left: -1000px;">

<span class="ygtvtm"> </span><span class="ygtvtmh"> </span><span class="ygtvtp"> </span><span class="ygtvtph"> </span><span class="ygtvln"> </span><span class="ygtvlm"> </span><span class="ygtvlmh"> </span><span class="ygtvlp"> </span><span class="ygtvlph"> </span><span class="ygtvloading"> </span>
