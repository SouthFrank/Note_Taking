## General Info

#### What is a class?
So, what exactly is a `class`? That's not an entirely new language-level entity, as one might think. In JavaScript, a class is a kind of function. Take a look:
![[Pasted image 20231117101903.png]]
What `class User {...}` construct really does is this:
1. Creates a function named `User`, that becomes the result of the class declaration. The function code is taken from the `constructor` method (assumed empty is we don't write such method).
2. Stores class methods, such as `sayHi` in `User.prototype`.

After `new User` object is created, when we call its method, it's taken from the prototype. So the object has access to class methods.

We can illustrate the result of `class User` declaration as:
![[Pasted image 20231117102325.png]]
And here's the code to introspect it:
![[Pasted image 20231117102402.png]]


JavaScript does not have classes in the same sense as other Object Oriented [[languages]] like Java or Ruby. The syntax for object creation that uses the **class** keyword was introduced in [[ES6]]. It is basically a new syntax that does the *exact* same thing as [[object constructors]] and [[prototypes]].

#### Class Basic Syntax

The basic syntax is:
![[Pasted image 20231117101503.png]]
Then you can use `new MyClass()` to create a new object with all of the listed methods.

The `constructor()` method is called automatically by **new**, so we can initialize the object there.
#### Why do some people dislike classes?

Opponents argue that **class** is basically just *syntactic sugar* over the existing prototype-based constructors and that it's dangerous and/or misleading to obscure what's *really* going on with these objects.

Despite the controversy, classes are beginning to show up in code bases and you are certainly going to encounter classes when uses [[frameworks]] such as React.

#### Not just syntactic sugar
Sometimes people say that `class` is a "syntactic sugar", because we could actually declare the same thing without using the `class` keyword at all:
![[Pasted image 20231117103142.png]]
The result of the definition is about the same. So, there are indeed reasons why `class` can be considered a syntactic sugar to define a constructor together with its prototype methods.

Still, there are important differences.
1. First, a function created by `class` is labelled by a special internal property `[[IsClassConstructor]]:true`. So it's not entirely the same as creating it manually. 
	The language checks for that property in a variety of places. For example, unlike a regular function, it must be called with `new`:
	![[Pasted image 20231117105609.png]]
	Also, a string representation of a class constructor in most JavaScript engines starts with the "class..."
	![[Pasted image 20231117105703.png]]
2. Class methods are non-enumerable. A class definition sets `enumerable` flag to `flase` for all methods in the `"prototype"`.
	That's good, because if we `for..in` over an object, we usually don't want its class methods.
3. Classes always `use strict`. All code inside the class construct is automatically in strict mode.

Besides, `class` syntax brings many other features that we'll explore later.

#### Class Expression
Just like with functions, classes can be defined inside another expression, passed around, returned, assigned, etc.
![[Pasted image 20231117110059.png]]
If a class expression has a name, it's visible inside the class only:
![[Pasted image 20231117110214.png]]
We can even make classes dynamically on demand:
![[Pasted image 20231117110236.png]]

#### Computed Names
Here's an example with a computed method using brackets `[...]`:
![[Pasted image 20231117110421.png]]
Such features are easy to remember, as they resemble that of literal objects.
#### Class Fields
"Class fields" is a syntax that allows to add any properties.
For instance, let's add `name` property to `class User`:
![[Pasted image 20231117110639.png]]
So, we just write " = " in the declaration, and that's it.
The important difference of class fields is that they are set on individual objects, not `User.prototype`:
![[Pasted image 20231117110741.png]]
We can also assign values using more complex expressions and function calls:
![[Pasted image 20231117110806.png]]

##### Making bound methods with class fields
As demonstrated previously, functions in JavaScript have a dynamic `this`. It depends on the context of the call.
So if an object method is passed around and called in another context, `this` won't be a reference to its object anymore. For instance, this code will show `undefined`:
![[Pasted image 20231117111006.png]]
The problem is called "losing `this`".
There are two approaches to fixing it.
1. Pass a wrapper-function, such as `setTimeout(() => button.click(), 1000)`.
2. Bind the method to an object, e.g. in the constructor.

**Class fields** provide another, quite elegant syntax:
![[Pasted image 20231117111258.png]]
The class field `click = () => {...}` is created on a per-object basis, there's a separate function for each `Button` object, with `this` inside it referencing that object. We can pass `button.click` around anywhere, and the value of `this` will always be correct.

That's especially useful in browser environment, for [[event listeners]].

### Static Methods & Properties
A static method is one that belongs to the original class, but is not creating and used in each individual instance. Similarly, you can set up a static property, although they are not officially adopted in [[ES6]]. Static properties are common in [[React]], and in order to interact with them, we use [[Babel]]. Babel can help you when using *unofficial* properties in ES6.
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