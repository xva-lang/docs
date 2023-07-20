[< Back to Basic Concepts](basic_concepts.md)

# Variables
Variables in Xva are exactly the same as other languages. They "bind" a value to a name, to be used by the programmer to refer to a value by a more friendly name, instead of the programmer having to remember potentially hundreds of seemingly random bits of information. 

## Declaring a variable
Xva variables are declared using the `let` keyword, followed by a name for the variable. Optionally, you may specify a *type* that the variable should hold. We'll talk more about types in a later section. Additionally, you may optionally assign a value to the variable in the same step as declaring it.

The following snippet is an example of some variable declarations.

`src/main.xva:`
```xva
let hello = "Hello, world!"
let number: int = 0
let unassigned_variable
```

> The colon (`:`) after the variable name indicates the start of an **annotation**. We'll talk more about annotations in a later section.

Variables can also be assigned with the values of other variables:

`src/main.xva:`
```xva
let mutable first_number = 3
let second_number = 4
first_number = second_number
```

The above code snippet simply copies the contents of `second_number` into the slot reserved for `first_number`, so that the value of `first_number` is now `4`.

## Mutability
Xva treats variables a little bit differently than most languages. When a variable is declared, it is automatically **immutable**. 

> immutable: *not capable of or susceptible to change*

The effect of this is that all variables, by default, can be assigned a value only once. Consider the following snippet:


`src/main.xva:`
```xva
let number = 123
number = 246
```
> This code does not compile.

The second line contains an assignment of a new value to the variable named `number`. This is not allowed in Xva, and will raise a compiler error because the variable `number` is automatically immutable. 

What if we do want to change the value? We must tell Xva that we intend to change the value. We modify the declaration slightly to make the variable **mutable**:

`src/main.xva:`
```xva
let mutable number = 123
number = 246
```

By adding the `mutable` keyword, we tell the compiler that we intend to re-assign different values to the variable named `number`.

### What's the point?
The reason Xva has this behaviour is actually two reasons:
1. Safety
2. Clarity of intention

The first reason, safety, is due to the fact that Xva guarantees that a variable's value won't change if it isn't **expected** to change. This is ideal for the programmer, because unintentionally modifying a variable could lead to a bug in your program. Xva makes this kind of bug less common by making you specify whether you intend to change this variable's value further along in the program. Additionally, Xva can make some internal optimisations with immutable variables, because it knows that the value will be assigned once and never change.

Which leads us to the second reason, clarity of intention. We just spoke about how the concept of immutable-by-default helps the programmer (and Xva itself), but it also forms a kind of self-documenting code. When you see a variable declared with `mutable`, this is a big hint to you, and potentionally other programmers who work with your code, that you are planning to modify this variable later in the program. 
