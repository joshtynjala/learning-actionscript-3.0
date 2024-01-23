# Example: Creating a basic application

ActionScript 3.0 can be used within a number of application development
environments, including the Flash Professional and Flash Builder tools or any
text editor.

This example walks through the steps in creating and enhancing a simple
ActionScript 3.0 application using Flash Professional or Flash Builder. The
application you’ll build presents a simple pattern for using external
ActionScript 3.0 class files in Flash Professional and Flex.

## Designing your ActionScript application

This example ActionScript application is a standard “Hello World” application,
so its design is simple:

- The application is called HelloWorld.

- It displays a single text field containing the words “Hello World!”

- The application uses a single object-oriented class named Greeter. This design
  allows the class to be used from within a Flash Professional or Flex project.

- In this example, you first create a basic version of the application. Next you
  add functionality to have the user enter a user name and have the application
  check the name against a list of known users.

With that concise definition in place, you can start building the application
itself.

## Creating the HelloWorld project and the Greeter class

The design statement for the Hello World application says that its code is easy
to reuse. To achieve that goal, the application uses a single object-oriented
class named Greeter. You use that class from within an application that you
create in Flash Builder or Flash Professional.

#### To create the HelloWorld project and Greeter class in Flex:

1.  In Flash Builder, select File \> New\> Flex Project,

2.  Type HelloWorld as the Project Name. Make sure that the Application type is
    set to “Web (runs in Adobe Flash Player),” and then click Finish.

    Flash Builder creates your project and displays it in the Package Explorer.
    By default the project already contains a file named HelloWorld.mxml, and
    that file is open in the editor.

3.  Now to create a custom ActionScript class file in Flash Builder, select
    File \> New \> ActionScript Class.

4.  In the New ActionScript Class dialog box, in the Name field, type
    **Greeter** as the class name, and then click Finish.

    A new ActionScript editing window is displayed.

    Continue with adding code to the Greeter class.

#### To create the Greeter class in Flash Professional:

1.  In Flash Professional, select File \> New.

2.  In the New Document dialog box, select ActionScript file, and click OK.

    A new ActionScript editing window is displayed.

3.  Select File \> Save. Select a folder to contain your application, name the
    ActionScript file **Greeter.as**, and then click OK.

    Continue with adding code to the Greeter class.

## Adding code to the Greeter class

The Greeter class defines an object, `Greeter`, that you use in your HelloWorld
application.

#### To add code to the Greeter class:

1.  Type the following code into the new file (some of the code may have been
    added for you):

        package
        {
            public class Greeter
            {
                public function sayHello():String
                {
                    var greeting:String;
                    greeting = "Hello World!";
                    return greeting;
                }
            }
        }

    The Greeter class includes a single `sayHello()`method, which returns a
    string that says “Hello World!”.

2.  Select File \> Save to save this ActionScript file.

The Greeter class is now ready to be used in an application.

## Creating an application that uses your ActionScript code

The Greeter class that you have built defines a self-contained set of software
functions, but it does not represent a complete application. To use the class,
you create a Flash Professional document or Flex project.

The code needs an instance of the Greeter class. Here’s how to use the Greeter
class to your application.

#### To create an ActionScript application using Flash Professional:

1.  Select File \> New.

2.  In the New Document dialog box, select Flash File (ActionScript 3.0), and
    click OK.

    A new document window is displayed.

3.  Select File \> Save. Select the same folder that contains the Greeter.as
    class file, name the Flash document **HelloWorld.fla**, and click OK.

4.  In the Flash Professional tools palette, select the Text tool. Drag across
    the Stage to define a new text field approximately 300 pixels wide and 100
    pixels high.

5.  In the Properties panel, with the text field still selected on the Stage,
    set the text type to “Dynamic Text.” Type **mainText** as the instance name
    of the text field.

6.  Click the first frame of the main timeline. Open the Actions panel by
    choosing Window \> Actions.

7.  In the Actions panel, type the following script:

        var myGreeter:Greeter = new Greeter();
        mainText.text = myGreeter.sayHello();

8.  Save the file.

Continue with Publishing and testing your ActionScript application.

#### To create an ActionScript application using Flash Builder:

1.  Open the HelloWorld.mxml file, and add code to match the following listing:

        <?xml version="1.0" encoding="utf-8"?>
        <s:Application xmlns:fx="http://ns.adobe.com/mxml/2009"
            xmlns:s="library://ns.adobe.com/flex/spark"
            xmlns:mx="library://ns.adobe.com/flex/halo"
            minWidth="1024"
            minHeight="768""
            creationComplete="initApp()">

            <fx:Script>
                <![CDATA[
                    private var myGreeter:Greeter = new Greeter();

                    public function initApp():void
                    {
                        // says hello at the start, and asks for the user's name
                        mainTxt.text = myGreeter.sayHello();
                    }
                ]]>
            </fx:Script>

            <s:layout>
                <s:VerticalLayout/>
            </s:layout>

            <s:TextArea id="mainTxt" width="400"/>

        </s:Application>

    This Flex project includes four MXML tags:

    - An `<s:Application>` tag, which defines the Application container

    - An `<s:layout>` tag, which defines the layout style (vertical layout) for
      the Application tag

    - An `<fx:Script>` tag that includes some ActionScript code

    - An `<s:TextArea>` tag, which defines a field to display text messages to
      the user

    The code in the `<fx:Script>` tag defines an `initApp()` method that is
    called when the application loads. The `initApp()` method sets the text
    value of the `mainTxt` TextArea to the “Hello World!” string returned by the
    `sayHello()` method of the custom class Greeter, which you just wrote.

2.  Select File \> Save to save the application.

Continue with Publishing and testing your ActionScript application.

## Publishing and testing your ActionScript application

Software development is an iterative process. You write some code, try to
compile it, and edit the code until it compiles cleanly. You run the compiled
application and test it to see if it fulfills the intended design. If it
doesn’t, you edit the code again until it does. The Flash Professional and Flash
Builder development environments offer a number of ways to publish, test, and
debug your applications.

Here are the basic steps for testing the HelloWorld application in each
environment.

#### To publish and test an ActionScript application using Flash Professional:

1.  Publish your application and watch for compilation errors. In Flash
    Professional, select Control \> Test Movie to compile your ActionScript code
    and run the HelloWorld application.

2.  If any errors or warnings are displayed in the Output window when you test
    your application, fix these errors in the HelloWorld.fla or HelloWorld.as
    files. Then try testing the application again.

3.  If there are no compilation errors, you see a Flash Player window showing
    the Hello World application.

You have created a simple but complete object-oriented application that uses
ActionScript 3.0. Continue with Enhancing the HelloWorld application.

#### To publish and test an ActionScript application using Flash Builder:

1.  Select Run \> Run HelloWorld.

2.  The HelloWorld application starts.

    - If any errors or warnings are displayed in the Output window when you test
      your application, fix the errors in the HelloWorld.mxml or Greeter.as
      files. Then try testing the application again.

    - If there are no compilation errors, a browser window opens showing the
      Hello World application. The text “Hello World!” appears.

    You have created a simple but complete object-oriented application that uses
    ActionScript 3.0. Continue with Enhancing the HelloWorld application.

## Enhancing the HelloWorld application

To make the application a little more interesting, you’ll now make it ask for
and validate a user name against a predefined list of names.

First you update the Greeter class to add new functionality. Then you update the
application to use the new functionality.

#### To update the Greeter.as file:

1.  Open the Greeter.as file.

2.  Change the contents of the file to the following (new and changed lines are
    shown in boldface):

        package
        {
            public class Greeter
            {
                /**
                 * Defines the names that receive a proper greeting.
                 */
                public static var validNames:Array = ["Sammy", "Frank", "Dean"];

                /**
                 * Builds a greeting string using the given name.
                 */
                public function sayHello(userName:String = ""):String
                {
                    var greeting:String;
                    if (userName == "")
                    {
                        greeting = "Hello. Please type your user name, and then press "
                                    + "the Enter key.";
                    }
                    else if (validName(userName))
                    {
                        greeting = "Hello, " + userName + ".";
                    }
                    else
                    {
                        greeting = "Sorry " + userName + ", you are not on the list.";
                    }
                    return greeting;
                }

                /**
                 * Checks whether a name is in the validNames list.
                 */
                public static function validName(inputName:String = ""):Boolean
                {
                    if (validNames.indexOf(inputName) > -1)
                    {
                        return true;
                    }
                    else
                    {
                        return false;
                    }
                }
            }
        }

The Greeter class now has a number of new features:

- The `validNames` array lists valid user names. The array is initialized to a
  list of three names when the Greeter class is loaded.

- The `sayHello()` method now accepts a user name and changes the greeting based
  on some conditions. If the `userName` is an empty string (`""`), the
  `greeting` property is set to prompt the user for a name. If the user name is
  valid, the greeting becomes `"Hello,`_userName_`."` Finally, if either of
  those two conditions are not met, the `greeting` variable is set to
  `"Sorry`_userName_`, you are not on the list."`

- The `validName()` method returns `true` if the `inputName` is found in the
  `validNames` array, and `false` if it is not found. The statement
  `validNames.indexOf(inputName)` checks each of the strings in the `validNames`
  array against the `inputName` string. The `Array.indexOf()` method returns the
  index position of the first instance of an object in an array. It returns the
  value -1 if the object is not found in the array.

Next you edit the application file that references this ActionScript class.

#### To modify the application using Flash Professional:

1.  Open the HelloWorld.fla file.

2.  Modify the script in Frame 1 so that an empty string (`""`) is passed to the
    Greeter class’s `sayHello()` method:

        var myGreeter:Greeter = new Greeter();
        mainText.text = myGreeter.sayHello("");

3.  Select the Text tool in the tools palette. Create two new text fields on the
    Stage. Place them side by side directly under the existing `mainText` text
    field.

4.  In the first new text field, which is the label, type the text **User
    Name:**.

5.  Select the other new text field, and in the Property inspector, select Input
    Text as the type of text field. Select Single line as the Line type. Type
    **textIn** as the instance name.

6.  Click the first frame of the main timeline.

7.  In the Actions panel, add the following lines to the end of the existing
    script:

        mainText.border = true;
        textIn.border = true;

        textIn.addEventListener(KeyboardEvent.KEY_DOWN, keyPressed);

        function keyPressed(event:KeyboardEvent):void
        {
            if (event.keyCode == Keyboard.ENTER)
            {
                mainText.text = myGreeter.sayHello(textIn.text);
            }
        }

    The new code adds the following functionality:

    - The first two lines simply define borders for two text fields.

    - An input text field, such as the `textIn` field, has a set of events that
      it can dispatch. The `addEventListener()` method lets you define a
      function that runs when a type of event occurs. In this case, that event
      is the pressing of a key on the keyboard.

    - The `keyPressed()` custom function checks if the key that was pressed is
      the Enter key. If so it calls the `sayHello()` method of the
      `myGreeter`object, passing the text from the `textIn` text field as a
      parameter. That method returns a string greeting based on the value passed
      in. The returned string is then assigned to the `text` property of the
      `mainText` text field.

    The complete script for Frame 1 is the following:

        var myGreeter:Greeter = new Greeter();
        mainText.text = myGreeter.sayHello("");

        mainText.border = true;
        textIn.border = true;

        textIn.addEventListener(KeyboardEvent.KEY_DOWN, keyPressed);

        function keyPressed(event:KeyboardEvent):void
        {
            if (event.keyCode == Keyboard.ENTER)
            {
                mainText.text = myGreeter.sayHello(textIn.text);
            }
        }

8.  Save the file.

9.  Select Control \> Test Movie to run the application.

    When you run the application, it prompts you to enter a user name. If it is
    valid (Sammy, Frank, or Dean), the application displays the “hello”
    confirmation message.

#### To modify the application using Flash Builder:

1.  Open the HelloWorld.mxml file.

2.  Next modify the `<mx:TextArea>` tag to indicate to the user that it is for
    display only. Change the background color to a light gray and set the
    `editable` attribute to `false`:

            <s:TextArea id="mainTxt" width="400" backgroundColor="#DDDDDD" editable="false" />

3.  Now add the following lines right after the `<s:TextArea>` closing tag.
    These lines create a TextInput component that lets the user enter a user
    name value:

            <s:HGroup width="400">
                <mx:Label text="User Name:"/>
                <s:TextInput id="userNameTxt" width="100%" enter="mainTxt.text = myGreeter.sayHello(userNameTxt.text);" />
            </s:HGroup>

    The `enter` attribute defines what happens when the user presses the Enter
    key in the `userNameTxt` field. In this example, the code passes the text in
    the field to the `Greeter.sayHello()` method. The greeting in the `mainTxt`
    field changes accordingly.

    The HelloWorld.mxml file looks like the following:

        <?xml version="1.0" encoding="utf-8"?>
        <s:Application xmlns:fx="http://ns.adobe.com/mxml/2009"
            xmlns:s="library://ns.adobe.com/flex/spark"
            xmlns:mx="library://ns.adobe.com/flex/halo"
            minWidth="1024"
            minHeight="768""
            creationComplete="initApp()">

            <fx:Script>
                <![CDATA[
                    private var myGreeter:Greeter = new Greeter();

                    public function initApp():void
                    {
                        // says hello at the start, and asks for the user's name
                        mainTxt.text = myGreeter.sayHello();
                    }
                ]]>
            </fx:Script>

            <s:layout>
                <s:VerticalLayout/>
            </s:layout>

            <s:TextArea id="mainTxt" width="400" backgroundColor="#DDDDDD" editable="false"/>

            <s:HGroup width="400">
                <mx:Label text="User Name:"/>
                <s:TextInput id="userNameTxt" width="100%" enter="mainTxt.text = myGreeter.sayHello(userNameTxt.text);" />
            </s:HGroup>

        </s:Application>

4.  Save the edited HelloWorld.mxml file. Select Run \> Run HelloWorld to run
    the application.

    When you run the application, the application prompts you to enter a user
    name. If it is valid (Sammy, Frank, or Dean), the application displays the “
    `Hello,`_userName_” confirmation message.
