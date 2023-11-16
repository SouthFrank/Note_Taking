## General Info

JavaScript does not have classes in the same sense as other Object Oriented [[languages]] like Java or Ruby. The syntax for object creation that uses the **class** keyword was introduced in [[ES6]]. It is basically a new syntax that does the *exact* same thing as [[object constructors]] and [[prototypes]].

#### Why do some people dislike classes?

Opponents argue that **class** is basically just *syntactic sugar* over the existing prototype-based constructors and that it's dangerous and/or misleading to obscure what's *really* going on with these objects.

Despite the controversy, classes are beginning to show up in code bases and you are certainly going to encounter classes when uses [[frameworks]] such as React.


## Lesson Overview

#### Describe the pros and cons of using classes in JavaScript.
#### Briefly discuss how JavaScript’s object creation differs from a language like Java or Ruby.
#### Explain the differences between an object constructor and a class.
#### Explain what “getters” and “setters” are.
There are two kinds of [[Object Properties]].
1. Data properties. All properties that we have been using up this point have been data properties.
2. Accessor properties. They are essentially functions that execute on getting and setting a value, but they look like regular properties to an external code.

Accessor properties are represented by "getter" and "setter" methods. In an [[object literal]] they are denoted by **get** and **set**.
```js
let obj = {
	get propName() {
		// getter, the code executed on getting obj.propName
	},

	set propName(value) {
		// setter, the code executed on setting obj.propName = value
	}
};
```
In the above example, the **getter** works when obj.propName is read, the **setter** works when it is assigned a new value.
#### Understand what computed names and class fields are.
#### Explain how to implement private class fields and methods.
#### Describe function binding.
#### Use inheritance with classes.
#### Understand why composition is generally preferred to inheritance.