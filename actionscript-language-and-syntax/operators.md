# Operators

Operators are special functions that take one or more operands and return a
value. An _operand_ is a value—usually a literal, a variable, or an
expression—that an operator uses as input. For example, in the following code,
the addition (`+`) and multiplication (`*`) operators are used with three
literal operands (2, 3`,` and 4`)` to return a value. This value is then used by
the assignment (`=`) operator to assign the returned value, 14, to the variable
`sumNumber`.

    var sumNumber:uint = 2 + 3 * 4; // uint = 14

Operators can be unary, binary, or ternary. A _unary_ operator takes one
operand. For example, the increment (`++`) operator is a unary operator, because
it takes only one operand. A _binary_ operator takes two operands. For example,
the division (`/`) operator takes two operands. A _ternary_ operator takes three
operands. For example, the conditional (`?:`) operator takes three operands.

Some operators are _overloaded_, which means that they behave differently
depending on the type or quantity of operands passed to them. The addition (`+`)
operator is an example of an overloaded operator that behaves differently
depending on the data type of the operands. If both operands are numbers, the
addition operator returns the sum of the values. If both operands are strings,
the addition operator returns the concatenation of the two operands. The
following example code shows how the operator behaves differently depending on
the operands:

    trace(5 + 5); // 10
    trace("5" + "5"); // 55

Operators can also behave differently based on the number of operands supplied.
The subtraction (`-`) operator is both a unary and binary operator. When
supplied with only one operand, the subtraction operator negates the operand and
returns the result. When supplied with two operands, the subtraction operator
returns the difference between the operands. The following example shows the
subtraction operator used first as a unary operator, and then as a binary
operator.

    trace(-3); // -3
    trace(7 - 2); // 5

## Operator precedence and associativity

Operator precedence and associativity determine the order in which operators are
processed. Although it may seem natural to those familiar with arithmetic that
the compiler processes the multiplication (`*`) operator before the addition
(`+`) operator, the compiler needs explicit instructions about which operators
to process first. Such instructions are collectively referred to as _operator
precedence_. ActionScript defines a default operator precedence that you can
alter using the parentheses (`()`) operator. For example, the following code
alters the default precedence in the previous example to force the compiler to
process the addition operator before the multiplication operator:

    var sumNumber:uint = (2 + 3) * 4; // uint == 20

You may encounter situations in which two or more operators of the same
precedence appear in the same expression. In these cases, the compiler uses the
rules of _associativity_ to determine which operator to process first. All of
the binary operators, except the assignment operators, are _left-associative_,
which means that operators on the left are processed before operators on the
right. The assignment operators and the conditional (`?:`) operator are
_right-associative_, which means that the operators on the right are processed
before operators on the left.

For example, consider the less-than (`<`) and greater-than (`>`) operators,
which have the same precedence. If both operators are used in the same
expression, the operator on the left is processed first because both operators
are left-associative. This means that the following two statements produce the
same output:

    trace(3 > 2 < 1); // false
    trace((3 > 2) < 1); // false

The greater-than operator is processed first, which results in a value of
`true`, because the operand 3 is greater than the operand 2. The value `true` is
then passed to the less-than operator along with the operand 1. The following
code represents this intermediate state:

    trace((true) < 1);

The less-than operator converts the value `true` to the numeric value 1 and
compares that numeric value to the second operand 1 to return the value `false`
(the value 1 is not less than 1).

    trace(1 < 1); // false

You can alter the default left associativity with the parentheses operator. You
can instruct the compiler to process the less-than operator first by enclosing
that operator and its operands in parentheses. The following example uses the
parentheses operator to produce a different output using the same numbers as the
previous example:

    trace(3 > (2 < 1)); // true

The less-than operator is processed first, which results in a value of `false`
because the operand 2 is not less than the operand 1. The value `false` is then
passed to the greater-than operator along with the operand 3. The following code
represents this intermediate state:

    trace(3 > (false));

The greater-than operator converts the value `false` to the numeric value 0 and
compares that numeric value to the other operand 3 to return `true` (the value 3
is greater than 0).

    trace(3 > 0); // true

The following table lists the operators for ActionScript 3.0 in order of
decreasing precedence. Each row of the table contains operators of the same
precedence. Each row of operators has higher precedence than the row appearing
below it in the table.

| Group          | Operators                                     |
| -------------- | --------------------------------------------- | --- | --- |
| Primary        | `[] {x:y} () f(x) new x.y x[y] <></> @ :: ..` |
| Postfix        | `x++ x--`                                     |
| Unary          | `++x --x + - ~ ! delete typeof void`          |
| Multiplicative | `* / %`                                       |
| Additive       | `+ -`                                         |
| Bitwise shift  | `<< >> >>>`                                   |
| Relational     | `< > <= >= as in instanceof is`               |
| Equality       | `== != === !==`                               |
| Bitwise AND    | `&`                                           |
| Bitwise XOR    | `^`                                           |
| Bitwise OR     | `                                             | `   |
| Logical AND    | `&&`                                          |
| Logical OR     | `                                             |     | `   |
| Conditional    | `?:`                                          |
| Assignment     | `= \*= /= %= += -= <<= >>= >>>= &= ^=         | =`  |
| Comma          | `,`                                           |

## Primary operators

The primary operators include those used for creating Array and Object literals,
grouping expressions, calling functions, instantiating class instances, and
accessing properties.

All the primary operators, as listed in the following table, have equal
precedence. Operators that are part of the E4X specification are indicated by
the (E4X) notation.

| Operator   | Operation performed                     |
| ---------- | --------------------------------------- |
| `[]`       | Initializes an array                    |
| `{x:y}`    | Initializes an object                   |
| `()`       | Groups expressions                      |
| `f(x)`     | Calls a function                        |
| `new`      | Calls a constructor                     |
| `x.y x[y]` | Accesses a property                     |
| `<></>`    | Initializes an XMLList object (E4X)     |
| `@`        | Accesses an attribute (E4X)             |
| `::`       | Qualifies a name (E4X)                  |
| `..`       | Accesses a descendant XML element (E4X) |

## Postfix operators

The postfix operators take one operator and either increment or decrement the
value. Although these operators are unary operators, they are classified
separately from the rest of the unary operators because of their higher
precedence and special behavior. When a postfix operator is used as part of a
larger expression, the expression’s value is returned before the postfix
operator is processed. For example, the following code shows how the value of
the expression `xNum++` is returned before the value is incremented:

    var xNum:Number = 0;
    trace(xNum++); // 0
    trace(xNum); // 1

All the postfix operators, as listed in the following table, have equal
precedence:

| Operator | Operation performed  |
| -------- | -------------------- |
| `++`     | Increments (postfix) |
| `--`     | Decrements (postfix) |

## Unary operators

The unary operators take one operand. The increment (`++`) and decrement (`--`)
operators in this group are _prefixoperators_, which means that they appear
before the operand in an expression. The prefix operators differ from their
postfix counterparts in that the increment or decrement operation is completed
before the value of the overall expression is returned. For example, the
following code shows how the value of the expression `++xNum` is returned after
the value is incremented:

    var xNum:Number = 0;
    trace(++xNum); // 1
    trace(xNum); // 1

All the unary operators, as listed in the following table, have equal
precedence:

| Operator | Operation performed      |
| -------- | ------------------------ |
| `++`     | Increments (prefix)      |
| `--`     | Decrements (prefix)      |
| `+`      | Unary +                  |
| `-`      | Unary - (negation)       |
| `!`      | Logical NOT              |
| `~`      | Bitwise NOT              |
| `delete` | Deletes a property       |
| `typeof` | Returns type information |
| `void`   | Returns undefined value  |

## Multiplicative operators

The multiplicative operators take two operands and perform multiplication,
division, or modulo calculations.

All the multiplicative operators, as listed in the following table, have equal
precedence:

| Operator | Operation performed |
| -------- | ------------------- |
| `*`      | Multiplication      |
| `/`      | Division            |
| `%`      | Modulo              |

## Additive operators

The additive operators take two operands and perform addition or subtraction
calculations. All the additive operators, as listed in the following table, have
equal precedence:

| Operator | Operation performed |
| -------- | ------------------- |
| `+`      | Addition            |
| `-`      | Subtraction         |

## Bitwise shift operators

The bitwise shift operators take two operands and shift the bits of the first
operand to the extent specified by the second operand. All the bitwise shift
operators, as listed in the following table, have equal precedence:

| Operator | Operation performed          |
| -------- | ---------------------------- |
| `<<`     | Bitwise left shift           |
| `>>`     | Bitwise right shift          |
| `>>>`    | Bitwise unsigned right shift |

## Relational operators

The relational operators take two operands, compare their values, and return a
Boolean value. All the relational operators, as listed in the following table,
have equal precedence:

| Operator     | Operation performed          |
| ------------ | ---------------------------- |
| `<`          | Less than                    |
| `>`          | Greater than                 |
| `<=`         | Less than or equal to        |
| `>=`         | Greater than or equal to     |
| `as`         | Checks data type             |
| `in`         | Checks for object properties |
| `instanceof` | Checks prototype chain       |
| `is`         | Checks data type             |

## Equality operators

The equality operators take two operands, compare their values, and return a
Boolean value. All the equality operators, as listed in the following table,
have equal precedence:

| Operator | Operation performed |
| -------- | ------------------- |
| `==`     | Equality            |
| `!=`     | Inequality          |
| `===`    | Strict equality     |
| `!==`    | Strict inequality   |

## Bitwise logical operators

The bitwise logical operators take two operands and perform bit-level logical
operations. The bitwise logical operators differ in precedence and are listed in
the following table in order of decreasing precedence:

| Operator | Operation performed |
| -------- | ------------------- | ---------- |
| `&`      | Bitwise AND         |
| `^`      | Bitwise XOR         |
| `        | `                   | Bitwise OR |

## Logical operators

The logical operators take two operands and return a Boolean result. The logical
operators differ in precedence and are listed in the following table in order of
decreasing precedence:

| Operator | Operation performed |
| -------- | ------------------- | --- | ---------- |
| `&&`     | Logical AND         |
| `        |                     | `   | Logical OR |

## Conditional operator

The conditional operator is a ternary operator, which means that it takes three
operands. The conditional operator is a shorthand method of applying the
`if..else`conditional statement.

| Operator | Operation performed |
| -------- | ------------------- |
| `?:`     | Conditional         |

## Assignment operators

The assignment operators take two operands and assign a value to one operand,
based on the value of the other operand. All the assignment operators, as listed
in the following table, have equal precedence:

| Operator | Operation performed                     |
| -------- | --------------------------------------- | --------------------- |
| `=`      | Assignment                              |
| `*=`     | Multiplication assignment               |
| `/=`     | Division assignment                     |
| `%=`     | Modulo assignment                       |
| `+=`     | Addition assignment                     |
| `-=`     | Subtraction assignment                  |
| `<<=`    | Bitwise left shift assignment           |
| `>>=`    | Bitwise right shift assignment          |
| `>>>=`   | Bitwise unsigned right shift assignment |
| `&=`     | Bitwise AND assignment                  |
| `^=`     | Bitwise XOR assignment                  |
| `        | =`                                      | Bitwise OR assignment |
