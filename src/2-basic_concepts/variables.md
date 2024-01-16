# Variables

Variables are ways of storing pieces of data for use in a program. They "bind" a value to a name, to be used by the programmer to refer to a value by a more friendly name, instead of the programmer having to remember potentially hundreds of seemingly random bits of information.

## Declaring a variable

Xva variables are declared using the `let` keyword, followed by a name for the variable. Optionally, you may specify a _type_ that the variable should hold. We'll talk more about types in a later section. Additionally, you may optionally assign a value to the variable in the same step as declaring it.

The following snippet is an example of some variable declarations.

```xva
let hello = "Hello, world!"
let number: int = 0
let unassigned_variable
```

> The colon (`:`) after the variable name indicates the start of an **annotation**. We'll talk more about annotations in a later section.

Note the lack of `=` on the third line. We can _declare_ variables and _initialise_ them in the same line, by _assigning_ a value to them, using the `=` symbol.

Variables can also be assigned the values of other variables:

```xva
let mutable first_number = 3
let second_number = 4
first_number = second_number
```

The above code snippet simply copies the contents of `second_number` into the slot reserved for `first_number`, so that the value of `first_number` is now `4`.

## Mutability

In the above code snippet, you may have noticed the word `mutable` just before the name of `first_number` in that declaration. When a variable is declared, that variable is **immutable**.

> immutable: _not capable of or susceptible to change_

The effect of this is that all variables, by default, can be assigned a value only once. Consider the following snippet:

> This code does not compile.

```xva
let number = 123
number = 246
```

The second line contains an assignment of a new value to the variable named `number`. This is not allowed in Xva, and will raise an error because the variable `number` is immutable.

What if we **do** want to be able to change a variable more than once? We must tell Xva that we intend to do so. We modify the declaration slightly to make the variable **mutable**:

```xva
var number = 123
number = 246
```

By replacing the `let` keyword with the `var` keyword, we tell the compiler that we intend to re-assign different values to the variable named `number`.

### Why is this necessary?

The reason Xva has this mutability behaviour is actually two reasons:

1. Safety
2. Clarity of intention

The first reason, safety, is due to the fact that Xva guarantees that a variable's value won't change if it isn't **expected** to change. This is ideal for the programmer, because unintentionally modifying a variable could lead to a bug in your program. Xva makes this kind of bug less common by making you specify whether you intend to change this variable's value further along in the program. Additionally, Xva can make some internal optimisations with immutable variables, because it knows that the value will be assigned once and never change.

Which leads us to the second reason, clarity of intention. We just spoke about how the concept of immutable-by-default helps the programmer (and Xva itself), but it also forms a kind of self-documenting code. When you see a variable declared with `mutable`, this is a big hint to you, and potentionally other programmers who work with your code, that you are planning to modify this variable later in the program.

## Constants

Constants are technically not variables, but are really just named values. They must be initialised when you declare them, and you can't change the values that they are storing. Constants are declared with the `const` keyword. Constants are used to refer to some value by a friendlier name.

Here's how you would declare a few constants:

```xva
const DAYS_IN_A_WEEK = 7
const DAYS_IN_JANUARY: int = 31
```

### Why can't we just use `let`?

You can! It will give you the same behaviour as a constant, if you initialise the variable declared with `let` as part of the declaration. However, constants are given special treatment by Xva, in that their data is placed in a special "constants pool" which enables Xva to be faster when accessing those values.
