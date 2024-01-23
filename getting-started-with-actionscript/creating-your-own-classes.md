# Creating your own classes

The process of creating classes for use in your projects can seem daunting.
However, the more difficult part of creating a class is the task of designing
the class’s methods, properties, and events.

## Strategies for designing a class

The topic of object-oriented design is a complex one; entire careers have been
devoted to the academic study and professional practice of this discipline.
Nevertheless, here are a few suggested approaches that can help you get started.

1.  Think about the role that the instances of this class play in the
    application. Generally, objects serve one of these three roles:

    - Value object: These objects serve primarily as containers of data. They
      probably have several properties and fewer methods (or sometimes no
      methods). They are generally code representations of clearly defined
      items. For example, a music player application could include a Song class
      representing a single real-world song and a Playlist class representing a
      conceptual group of songs.

    - Display object: These are objects that actually appear on the screen.
      Examples include user-interface elements like a drop-down list or status
      readout, graphical elements like creatures in a video game, and so on.

    - Application structure: These objects play a broad range of supporting
      roles in the logic or processing performed by applications. For example,
      you can make an object to perform certain calculations in a biology
      simulation. You can make one that’s responsible for synchronizing values
      between a dial control and a volume readout in a music player application.
      Another one can manage the rules in a video game. Or you can make a class
      to load a saved picture in a drawing application.

2.  Decide the specific functionality that the class needs. The different types
    of functionality often become the methods of the class.

3.  If the class is intended to serve as a value object, decide the data that
    the instances include. These items are good candidates for properties.

4.  Since your class is being designed specifically for your project, what’s
    most important is that you provide the functionality that your application
    needs. Try to answer these questions for yourself:

    - What pieces of information is your application storing, tracking, and
      manipulating? Answering this question helps you identify any value objects
      and properties you need.

    - What sets of actions does the application perform? For example, what
      happens when the application first loads, when a particular button is
      clicked, when a movie stops playing, and so on? These are good candidates
      for methods. They can also be properties if the “actions” involve changing
      individual values.

    - For any given action, what information is necessary to perform that
      action? Those pieces of information become the parameters of the method.

    - As the application proceeds to do its work, what things change in your
      class that other parts of your application need to know about? These are
      good candidates for events.

5.  Is there is an existing object that is similar to the object you need except
    that it’s lacking some additional functionality you want to add? Consider
    creating a subclass. (A _subclass_ is a class which builds on the
    functionality of an existing class, rather than defining all of its own
    functionality.) For example, to create a class that is a visual object on
    the screen, use the behavior of an existing display object as a basis for
    your class. In that case, the display object (such as MovieClip or Sprite)
    would be the _base class_ , and your class would extend that class.

## Writing the code for a class

Once you have a design for your class, or at least some idea of what information
it stores and what actions it carries out, the actual syntax of writing a class
is fairly straightforward.

Here are the minimum steps to create your own ActionScript class:

1.  Open a new text document in your ActionScript text editor program.

2.  Enter a `class` statement to define the name of the class. To add a `class`
    statement, enter the words `public class` and then the class’s name. Add
    opening and closing curly brackets to contain the contents of the class (the
    method and property definitions). For example:

        public class MyClass
        {
        }

    The word `public` indicates that the class can be accessed from any other
    code. For other alternatives, see Access control namespace attributes.

3.  Type a `package` statement to indicate the name of the package that contains
    your class. The syntax is the word `package`, followed by the full package
    name, followed by opening and closing curly brackets around the `class`
    statement block) For example, change the code in the previous step to the
    following:

        package mypackage
        {
        public class MyClass
        {
        }
        }

4.  Define each property in the class using the `var` statement within the class
    body. The syntax is the same as you use to declare any variable (with the
    addition of the `public` modifier). For example, adding these lines between
    the opening and closing curly brackets of the class definition creates
    properties named `textProperty`, `numericProperty`, and `dateProperty`:

        public var textProperty:String = "some default value";
        public var numericProperty:Number = 17;
        public var dateProperty:Date;

5.  Define each method in the class using the same syntax that’s used to define
    a function. For example:

    - To create a `myMethod()` method, enter:

          public function myMethod(param1:String, param2:Number):void
          {
          // do something with parameters
          }

    - To create a constructor (the special method that is called as part of the
      process of creating an instance of a class), create a method whose name
      matches exactly the name of the class:

          public function MyClass()
          {
          // do stuff to set initial values for properties
          // and otherwise set up the object
          textVariable = "Hello there!";
          dateVariable = new Date(2001, 5, 11);
          }

      If you don’t include a constructor method in your class, the compiler
      automatically creates an empty constructor in your class. (In other words,
      a constructor with no parameters and no statements.)

    There are a few more class elements that you can define. These elements are
    more complex.

    - _Accessors_ are a special cross between a method and a property. When you
      write the code to define the class, you write the accessor like a method.
      You can perform multiple actions rather than just reading or assigning a
      value, which is all you can do when you define a property. However, when
      you create an instance of your class, you treat the accessor like a
      property and use the name to read or assign the value.

    - Events in ActionScript aren’t defined using a specific syntax. Instead,
      you define events in your class using the functionality of the
      EventDispatcher class.

More Help topics

![](../img/as3LinkIndicator.png)
[Handling events](http://help.adobe.com/en_US/as3/dev/WS5b3ccc516d4fbf351e63e3d118a9b90204-7fca.html)
