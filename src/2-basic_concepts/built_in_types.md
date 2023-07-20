[< Back to Types](types.md)

## Built-in types
Xva has two categories of types:
- Scalar types, and
- Compound types

Scalar types represent a single value, like a number `123`, or an Emoji character :heart:.

Compound types represent a grouping of multiple values as a single type. 

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

For most values, you should use `float`. Use `precise` when you absolutely need the extra precision, like in cases of high-precision financial or  scientific calculations, where losing some precision will have a bad effect on the output of your program. Imagine if you did all sorts of complex maths on your bank account and ended up with less money!

> For nerds: Xva uses the IEEE-754 standard for floats: 64-bit (binary64) for `float` and 128-bit (binary128) for `precise`. The computational expensiveness behind `precise` is the fact that it has to be emulated in software, whereas your processor has native support for `float`.


### Booleans
Booleans are super simple. They can only be `true` or `false`. Booleans are most commonly used in conditional expressions, which we'll talk about in a later chapter. 

Booleans are annotated with `boolean`.

### Characters
Characters are a single textual character. You can represent a single letter, a diacritic or glyph, an Emoji, even letters from other languages! 

A character must be specified with single quotes: `'x'`. Double quotes are used to specify strings - they are not interchangeable.

Characters are annotated with `char`.

> For nerds: a `char` is always stored as 4 bytes. This is to allow Xva to represent the entire Unicode Scalar Value space, from `U+0000` to `U+10FFFF`, inclusive. Each `char` value is encoded in UTF-8. 

## Compound types
There are two kinds of compound types in Xva:
- Tuples
- Vectors
- Records, and 
- Objects (todo)

### Tuples
Tuples are the most basic compound type. A tuple is an immutable, ordered collection of values. It is:
- Immutable, because the tuple's values can't be changed, and
- Ordered, because the tuple's values are always in the same order as when the tuple was declared.

Tuples are used for passing around sets of values in a lightweight manner. The values inside don't have a name for themselves (they are not bound), but instead the tuple is used as essentially a single value. It is commonly used to return multiple values from a function, that can be destructured later. We'll talk about destructuring in a later chapter.

A tuple type is annotated with the list of types that make up a the tuple, comma-seperated and wrapped in parentheses. It is assigned to with the list of values, also comma-separated and wrapped in parentheses. Consider the following snippet:

`src/main.xva:`
```xva
let tuple_item: (int, float, char) = (123, 1.23, 'x')
let inferred_tuple = ('f', 16, 12.06543)
```

The above snippet declares two tuples, one of which has its types inferred as `char`, `int` and `float`, respectively.

### Records
Records are essentially a tuple on steroids. They combine a collection of values, and bind the values to a name. They can be used to represent a complex piece of data in your program's logic. A record's fields can be any type, even another record!

> Record-ception!

For those coming from C or similar languages, a record is similar to a struct. For those coming from JavaScript or similar languages, a `record` is similar to an object. 

Consider the following snippet:

`src/record.xva:`
```xva
let money = record
    currency_type: int = 1
    amount: precise = 1723.445
end
```
> Note the use of `end` to signify the end of the declaration of a `record`.

The above snippet declares a variable `money` which has a type of `record<currency_type: int, amount: precise>`. 

That's type is really long! That's because fields of a `record` are bound to concrete names. You can't add an extra field to a `record`, nor can you remove or omit fields from a `record`. The type checker also needs the names of the fields because it further differentiates different `record` types by their structure, as well as their field types.

Consider the following snippet. Xva interprets these records as not being of the same type, even though their fields have the same types:

`src/main.xva:`
```xva
let record_one = record
    item_one: int = 1
end

let record_two = record
    item_two: int = 1
end

record_one = record_two
```
> This code does not compile.

Running this code causes a compiler error, because it attempts to assign a value to a variable of a different type.

A clear difference between records and tuples is that you can access the fields of a `record` by their name, whereas you cannot do so with a tuple (because tuple fields don't have a name). Accessing a `record` field is done by specifying the name of the `record` value, followed by a dot `.`, then the name of the desired field:

`src/record.xva:`
```xva
print(money.amount)
```

Another difference between records and tuples is that you can't add a type annotation of `record` to something. You must either assign a value to it that has a type of `record`, or annotate it with a custom type that you have defined with a **type definition**. We'll talk about type definitions in the next section. This rule also applies to the fields of a `record`.
