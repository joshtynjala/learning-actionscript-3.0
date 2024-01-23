# Example: Animation portfolio piece (Flash Professional)

This example is designed to give you a first opportunity to see how you can
piece together bits of ActionScript into a complete application. The animation
portfolio piece is an example of how you could take an existing linear animation
and add some minor interactive elements. For example, you could incorporate an
animation created for a client into an online portfolio. The interactive
behavior that you’ll add to the animation includes two buttons the viewer can
click: one to start the animation, and one to navigate to a separate URL (such
as the portfolio menu or the author’s home page).

The process of creating this piece can be divided into these main sections:

1.  Prepare the FLA file for adding ActionScript and interactive elements.

2.  Create and add the buttons.

3.  Write the ActionScript code.

4.  Test the application.

## Preparing to add interactivity

Before you can add interactive elements to your animation, it’s helpful to set
up the FLA file by creating some places to add your new content. This task
includes creating actual space on the Stage where buttons can be placed. It also
includes creating “space” in the FLA file for keeping different items separate.

#### To set up your FLA for adding interactive elements:

1.  Create a FLA file with a simple animation such as a single motion tween or
    shape tween. If you already have a FLA file containing the animation that
    you’re showcasing in the project, open that file and save it with a new
    name.

2.  Decide where on the screen you’ll want the two buttons to appear. One button
    is to start the animation and one is to link to the author portfolio or home
    page. If necessary, clear or add some space on the Stage for this new
    content. If the animation doesn’t already have one, you can create a startup
    screen on the first frame. In that case you’ll probably want to shift the
    animation over so it starts on Frame 2 or later.

3.  Add a new layer, above the other layers in the Timeline, and name it
    **buttons**. This layer is where you’ll add the buttons.

4.  Add a new layer, above the buttons layer, and name it **actions**. This
    layer is where you’ll add ActionScript code to your application.

## Creating and adding buttons

Next, you’ll actually create and position the buttons that form the center of
the interactive application.

#### To create and add buttons to the FLA:

1.  Using the drawing tools, create the visual appearance of your first button
    (the “play” button) on the buttons layer. For example, draw a horizontal
    oval with text on top of it.

2.  Using the Selection tool, select all the graphic parts of the single button.

3.  From the main menu, choose Modify \> Convert To Symbol.

4.  In the dialog box, choose Button as the symbol type, give the symbol a name,
    and click OK.

5.  With the button selected, in the Property inspector give the button the
    instance name **playButton**.

6.  Repeat steps 1 through 5 to create the button that takes the viewer to the
    author’s home page. Name this button **homeButton**.

## Writing the code

The ActionScript code for this application can be divided into three sets of
functionality, although you enter it all in the same place. The three things the
code does are:

- Stop the playhead as soon as the SWF file loads (when the playhead enters
  Frame 1).

- Listen for an event to start the SWF file playing when the user clicks the
  play button.

- Listen for an event to send the browser to the appropriate URL when the user
  clicks the author home page button.

#### To create code to stop the playhead when it enters Frame 1:

1.  Select the keyframe on Frame 1 of the actions layer.

2.  To open the Actions panel, from the main menu, choose Window \> Actions.

3.  In the Script pane, enter the following code:

        stop();

#### To write code to start the animation when the play button is clicked:

1.  At the end of the code entered in the previous steps, add two empty lines.

2.  Enter the following code at the bottom of the script:

        function startMovie(event:MouseEvent):void
        {
            this.play();
        }

    This code defines a function called `startMovie()`. When `startMovie()`is
    called, it causes the main timeline to start playing.

3.  On the line following the code added in the previous step, enter this line
    of code:

        playButton.addEventListener(MouseEvent.CLICK, startMovie);

    This line of code registers the `startMovie()` function as a listener for
    `playButton`’s `click` event. In other words, it makes it so that whenever
    the button named `playButton` is clicked, the `startMovie()` function is
    called.

#### To write code to send the browser to a URL when the home page button is clicked:

1.  At the end of the code entered in the previous steps, add two empty lines.

2.  Enter this code at the bottom of the script:

        function gotoAuthorPage(event:MouseEvent):void
        {
            var targetURL:URLRequest = new URLRequest("http://example.com/");
            navigateToURL(targetURL);
        }

    This code defines a function called `gotoAuthorPage()`. This function first
    creates a URLRequest instance representing the URL http://example.com/. It
    then passes that URL to the `navigateToURL()` function, causing the user’s
    browser to open that URL.

3.  On the line following the code added in the previous step, enter this line
    of code:

        homeButton.addEventListener(MouseEvent.CLICK, gotoAuthorPage);

    This line of code registers the `gotoAuthorPage()` function as a listener
    for `homeButton`’s `click` event. In other words, it makes it so that
    whenever the button named `homeButton` is clicked, the `gotoAuthorPage()`
    function is called.

## Testing the application

The application is now completely functional. Let’s test it to make sure that’s
the case.

#### To test the application:

1.  From the main menu, choose Control \> Test Movie. Flash Professional creates
    the SWF file and opens it in a Flash Player window.

2.  Try both the buttons to make sure that they do what you expect them to.

3.  If the buttons don’t work, here are some things to check for:

    - Do the buttons both have distinct instance names?

    - Do the `addEventListener()` method calls use the same names as the
      buttons’ instance names?

    - Are the correct event names used in the `addEventListener()` method calls?

    - Is the correct parameter specified for each of the functions? (Both
      methods need a single parameter with the data type MouseEvent.)

    All of these mistakes and most other possible mistakes result in an error
    message. The error message can appear either when you choose the Test Movie
    command or when you click the button while testing the project. Look in the
    Compiler Errors panel for compiler errors (the ones that happen when you
    first choose Test Movie). Check the Output panel for run-time errors which
    happen while the content is playing, such as when you click a button.
