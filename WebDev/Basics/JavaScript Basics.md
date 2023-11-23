
## Variables

Variables in JavaScript can be defined using the [[const]], [[let]], or [[var]] keywords.

`let` or `var` can reference different values over their lifetime. For example, `myFirstVariable` can be defined and redefined many times using the assignment operator `=`:
![[Pasted image 20231121104257.png]]

In contrast to `let` and `var`, variables that are defined with `const` can only be assigned once. This is used to define constants in JavaScript.

**camelCasing** your variables is the common and best practice in JavaScript. The ALL_CAPS style of naming is not as common in JavaScript, but will still serve, for example, as aliases for magic numbers or string values. Example:
![[Pasted image 20231121104641.png]]

Prior to `const`, there was only `var` so capitalization was the only way you could communicate that a variable should never be re-assigned. The variable is still sometimes capitalized when it should never be re-assigned, is not relative, and will never change in the future. Example:
`const SSN = 123-45-6789`
`const CREATED_ON = 312314123`
`const PI = 3.14`

Sometimes all caps can be used in teams for all [[global variables]].

## Function Declarations

In JavaScript, units of functionality are encapsulated in **functions**, usually grouping functions together in the same file if they belong together. These functions can take parameters (arguments), and can `return` a value using the `return` keyword. Functions are invoked using `()` syntax.

There are many ways to declare a function in JS, this is the most basic:
![[Pasted image 20231121105345.png]]

## Exposing functions to other files

To make a `function`, a `constant`, or a `variable` available in other files, they need to be **exported** using the `export` keyword. This is also known as the [[module system]]. A great example is how all the tests work. Each exercise has at least one file, for example `lasagna.js`, which contains the implementation. Additionally, there is at least one other file, for example `lasagna.spec.js`, that contains the *tests*. This file *imports* the public (i.e. exported) entities to test the implementation:
![[Pasted image 20231121105640.png]]


## Numbers
Many programming languages have specific numeric types to represent different types of numbers, but JavaScript has only two:
- `number`: a numeric data type in the double-precision 64-bit floating-point formate (IEEE 754). Examples are `-6`, `-2.4`, `0`, `0.1`, `1`, `3.14`, `16.984025`, `25`, `976`, `1024.0`, `500000`.
- `bigint`: a numeric data type that can represent integers in the arbitrary precision format. Examples are `12n`, `0n`, `4n`, and `9007199254740991n`.

If you require arbitrary precision work with extremely large numbers, use the `bigint` type. Otherwise, the `number` type is likely the better option.

#### Rounding
There is a built-in global object called `Math` that provides various rounding functions. For example, you can round down (`floor`) or round up (`ceil`) decimal numbers to the nearest whole number.
![[Pasted image 20231121111734.png]]

## Booleans
A boolean represents one of two values: `true` or `false`. Logical operators (`!`, `&&`, `||`) are typically used with boolean values and they return a boolean value.
## Strings
A **string** is the JavaScript data type to store text data.

You create a string by wrapping the text in single quotes or double quotes. 
![[Pasted image 20231122092117.png]]

#### Strings as Lists of Characters
A string can be treated as a list of characters where the first character has index `0`. You can access an individual character of the string using square brackets and the index of the letter you want to retrieve.
`'cat'[1]` //a
You can determine the number of characters in a string by accessing the `length` property.
`'cat'.length` //3
The simplest way to concatenate strings is to use the addition operator `+`.
`'I like' + ' ' + 'cats.'`; // "I like cats."

Strings provide a lot of helper methods, called [[String Methods]].
## Arrays
In JavaScript, an array is a list-like structure with no fixed length which can hold any type of primitives or objects, even in mixed types.

To create an array, add elements between square brackets `[]`. To read from the array, put the index in square brackets `[]` after the identifier. The indices of an array starts at zero. For example:
![[Pasted image 20231122095638.png]]
To retrieve the number of elements that are in an array, use the `length` property:
![[Pasted image 20231122100803.png]]
To change an element in the array, you assign a value at the index:
![[Pasted image 20231122101216.png]]
Some of the [methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) that are available on every Array object can be used to add or remove from the array. [[Array Methods]] are important to learn, they allow manipulation of data in many different scenarios.


## Conditionals & Operators
A common way to conditionally execute logic in JS is the if-statement. The code block will only be executed if the condition evaluates to `true`.
![[Pasted image 20231123091707.png]]

#### Comparison Operators
In JavaScript, numbers can be compared using the following relational and equality operators:
![[Pasted image 20231123091846.png]]
The comparison result is always a [[boolean]]: `true` or `false`:
![[Pasted image 20231123091924.png]]
In JavaScript, the comparison operators above can also be used to compare strings. In that case, a dictionary (lexicographical) order is applied. You can find a list of the exact order of all the characters [here](https://www.fileformat.info/info/charset/UTF-16/list.htm).
![[Pasted image 20231123092051.png]]
