[< Back to Basic Concepts](basic_concepts.md)

# Types

## In this chapter
1. [Introduction](#introduction)
2. [Built-in types](built_in_types.md)

## Introduction
All constructs in Xva (variables, functions etc.) have a certain data type, which we refer to as its **type**. Xva is both statically-typed and strongly-typed, which means that:
1. Statically-typed: the type of everything in the program must be known to the compiler before any code starts running, and
2. Strongly-typed: the type of something cannot change in unexpected ways.

Xva can figure out what type most things should be based on how it is used in the program. We refer to this ability as **type inference**. 

> type inference: *The automatic detection of the type of an expression in a formal language*.

If you're coming to Xva from a language like C, you'll know that for the most part, you have to specify the type of every single variable in every single program. This can quickly become very tiresome, as we want to spend our time writing some cool programs, not thinking about types! Even though Xva requires a type for every piece of code, it can use its type inference to save you some time, and also write code that is more compact.

Consider the following snippet:

`src/main.xva:`
```xva
let number = 12
let fraction = 0.42
let message = "Type inference is pretty cool!"
```

Based on the values assigned to each of the variables in the above snippet, Xva has inferred the types of each variable (`int`, `float` and `string`, respectively).

However, as much as we'd like to think so, Xva is not all-knowing. Sometimes, Xva is unable to infer the type of something, in which case you have to specify the type. Additionally, Xva may infer a different type than what you as the programmer prefer. In both cases, you should explicitly specify the type of something. We do this by adding a **type annotation**:

`src/main.xva`
```xva
let typed_number: int = 12
let typed_fraction: float = 0.42
let typed_message: string = "Type inference is pretty cool!"
```

## What's the point?

### Static typing
Going back to Xva's emphasis on safe code, the reason for static typing in Xva is mainly to catch common typing errors before the code starts running. Because Xva does not allow code with typing problems to start executing, Xva will guarantee that all of your code is type-safe before you put it somewhere important.

Consider the Python programming language. Python is also strongly-typed, but unlike Xva, it is **dynamically-typed**. This means that the type of something in Python is determined at runtime.

>The words **at runtime** means "while the program is running". This is in constrast to **compile time**, which is before the program runs and while the compiler is analysing your code.

In a dynamically-typed language, if an operation is attempted that is not valid for one or more of the types in the operation (for example, adding a number and a string) an error will occur while the program is running, which may cause problems for your software, **especially** in mission-critical environments. This kind of error is called a **typing error**. Xva solves this by doing checks on all types in the program at compile time, so that it can guarantee that once your program starts running, no typing errors will occur. Of course, with anything, there are tradeoffs:

- Compile time type checking: slower compile times, faster runtimes.
- Runtime type checking: faster compile times, slower runtimes, potential for runtime typing errors.

This doesn't mean dynamically-typed languages are bad - in fact, Python is an incredibly powerful language used by the biggest software companies in the world, from micro-services to artifical intelligence and everything in between. We just decided to do things a little differently with Xva.


### Strong typing
Strong typing ensures that something's type cannot change in odd or unexplainable ways, and that an operation on one or more items can only be performed if the operation has those items' types in its "allowed types". 

Consider the following code snippet:

`src/main.xva:`
```xva
let item: int = 123
print(item + "4")
```
> This code does not compile.

This code attempts to add a string `"4"` to a number `123`. In Xva, such operations are not allowed. If it were allowed, the result will probably be a string, and therefore the type of the expression has changed in an unexpected way. Xva catches errors like this at compile time and prevents the code from running, so that you avoid confusion when troubleshooting your code.

[Next: Built-in types >](built_in_types.md)

