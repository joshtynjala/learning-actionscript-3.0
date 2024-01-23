# Common program elements

There are a few additional building blocks that you use to create an
ActionScript program.

## Operators

_Operators_ are special symbols (or occasionally words) that are used to perform
calculations. They are mostly used for math operations, and also used when
comparing values to each other. Generally, an operator uses one or more values
and “works out” to a single result. For example:

- The addition operator (`+`) adds two values together, resulting in a single
  number:

      var sum:Number = 23 + 32;

- The multiplication operator (`*`) multiplies one value by another, resulting
  in a single number:

      var energy:Number = mass * speedOfLight * speedOfLight;

- The equality operator (`==`) compares two values to see if they are equal,
  resulting in a single true-or-false (Boolean) value:

      if (dayOfWeek == "Wednesday")
      {
          takeOutTrash();
      }

  As shown here, the equality operator and the other “comparison” operators are
  most commonly used with the `if` statement to determine whether or not certain
  instructions are carried out.

## Comments

As you’re writing ActionScript, you’ll often want to leave notes to yourself.
For example, sometimes you want to explain how certain lines of code work or why
you made a particular choice. _Code comments_ are a tool you can use to write
text that the computer ignores in your code. ActionScript includes two kinds of
comments:

- Single-line comment: A single-line comment is designated by placing two
  slashes anywhere on a line. The computer ignores everything after the slashes
  up to the end of that line:

      // This is a comment; it's ignored by the computer.
      var age:Number = 10; // Set the age to 10 by default.

- Multiline comments: A multiline comment includes a starting comment marker
  (`/*`), then the comment content, and an ending comment marker (`*/`). The
  computer ignores everything between the starting and ending markers regardless
  of how many lines the comment spans:

      /*
      This is a long description explaining what a particular
      function is used for or explaining a section of code.

      In any case, the computer ignores these lines.
      */

Another common use of comments is to temporarily “turn off” one or more lines of
code. For example, you can use comments if you’re testing out a different way of
doing something. You can also use them to try to figure out why certain
ActionScript code isn’t working the way you expect.

## Flow control

Many times in a program, you want to repeat certain actions, perform only
certain actions and not others, perform alternative actions depending on certain
conditions, and so on. _Flow control_ is the control over which actions are
performed. There are several types of flow control elements available in
ActionScript.

- Functions: Functions are like shortcuts. They provide a way to group a series
  of actions under a single name, and can be used to perform calculations.
  Functions are necessary for handling events, but are also used as a general
  tool for grouping a series of instructions.

- Loops: Loop structures let you designate a set of instructions that the
  computer performs a set number of times or until some condition changes. Often
  loops are used to manipulate several related items, using a variable whose
  value changes each time the computer works through the loop.

- Conditional statements: Conditional statements provide a way to designate
  certain instructions that are carried out only under certain circumstances.
  They are also used to provide alternative sets of instructions for different
  conditions. The most common type of conditional statement is the `if`
  statement. The `if` statement checks a value or expression in its parentheses.
  If the value is `true,` the lines of code in curly brackets are carried out.
  Otherwise, they are ignored. For example:

      if (age < 20)
      {
          // show special teenager-targeted content
      }

  The `if` statement’s companion, the `else` statement, lets you designate
  alternative instructions that the computer performs if the condition is not
  `true`:

      if (username == "admin")
      {
          // do some administrator-only things, like showing extra options
      }
      else
      {
          // do some non-administrator things
      }
