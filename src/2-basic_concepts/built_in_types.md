# Built-in types

Xva has two categories of types:

- Scalar types, and
- Collection types

Scalar types represent a single value, like a number `123`, or an Emoji character.

Collection types represent a grouping of multiple values as a single type.

## Scalar types

Xva has four categories of scalar type:

- Integers (round numbers)
- Floating-point numbers (decimals or fractions)
- Booleans (true or false), and
- Characters (letters, Emojis or formatting characters)

### Integers

An integer is a round number that can be positive or negative. `-3`, `1632` and `0` are all integers.

You can specify integer values in a number of ways. Different base systems (octal, hexadecimal, etc.) require a prefix at the start.

- Decimal, or the "normal" way: `1024`
- Hexadecimal: `0xCAFE1234`
- Octal: `0o77`
- Binary: `0b11001010`

### Floating-point numbers

Floating-point numbers, or "floats", are numbers that do not have to be whole numbers. Some example of floats are `1.23`, `2.5e6` and `-4.0`.

> Floating-point: denoting a mode of representing numbers as two sequences of bits, one representing the digits in the number and the other an exponent which determines the position of the radix point.

There are two types of floats in Xva: `float` and `precise`. `float` is the more basic one, with approximately 15 digits of decimal precision, whereas `precise` has approximately 28 digits of decimal precision, at the expense of requiring both more space to store the value and taking Xva slightly longer to produce a result in mathematical operations.

For most values, you should use `float`. Use `precise` when you absolutely need the extra precision, like in cases of high-precision financial or scientific calculations, where losing some precision will have a bad effect on the output of your program. Imagine if you did all sorts of complex maths on your bank account and ended up with less money!

> For nerds: Xva uses the IEEE-754 standard for floats: 64-bit (binary64) for `float` and 128-bit (binary128) for `precise`. The computational expensiveness behind `precise` is the fact that it has to be emulated in software, whereas your processor has native support for `float`.

### Booleans

Booleans are super simple. They can only be `true` or `false`. Booleans are most commonly used in conditional expressions, which we'll talk about in a later chapter.

Booleans are annotated with `boolean`.

### Characters

Characters are a single textual character. You can represent a single letter, a diacritic or glyph, an Emoji, even letters from other languages!

A character must be specified with single quotes: `'x'`. Double quotes are used to specify strings - they are not interchangeable.

Characters are annotated with `char`.

> For nerds: a `char` is always stored as 4 bytes. This is to allow Xva to represent the entire Unicode Scalar Value space, from `U+0000` to `U+10FFFF`, inclusive. Each `char` value is encoded in UTF-8.

## Collection types

There are a few kinds of collections in Xva:

- Tuples, and
- Lists,

### Tuples

Tuples are the most basic compound type. A tuple is an immutable, ordered collection of values. It is:

- Immutable, because the tuple's values can't be changed, and
- Ordered, because the tuple's values are always in the same order as when the tuple was declared.

Tuples are used for passing around sets of values in a lightweight manner. The values inside don't have a name for themselves (they are not bound), but instead the tuple itself is a single value. It is commonly used to return multiple values from a function, that can be destructured later. We'll talk about destructuring in a later chapter.

A tuple type is annotated with the list of types that make up a the tuple, comma-seperated and wrapped in parentheses. It is assigned to with the values, also comma-separated and wrapped in parentheses. Consider the following snippet:

```xva
let tuple_item: (int, float, char) = (123, 1.23, 'x')
let inferred_tuple = ('f', 16, 12.06543)
```

The above snippet declares two tuples, one of which has its types inferred as `char`, `int` and `float`, respectively.

> "Tuple" is pronounced "**tuh**-pl"

### Lists

Lists are ways of grouping together multiple items of the same type. You can add items, remove items, and change their values in place. It is a mutable, ordered collection. Lists are homogenous, which means they may only store values that are all the same type.

A list is written as a comma-separated list of values, wrapped in square brackets `[]`. The list **type** is written as `List<T>` where `T` is the type of data the list contains.

Here's an example of creating a list:

```xva
let animals = ["dog", "cat", "bird", "fish", "bear"]
```

_The_ `<>` _symbols in the list type are part of the **generics** system, and are used to surround type parameters. We'll talk about these in a later chapter._
