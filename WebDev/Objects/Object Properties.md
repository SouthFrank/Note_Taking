There are two kinds of [[Object Properties]].
1. Data properties. All properties that we have been using up this point have been data properties.
2. Accessor properties. They are essentially functions that execute on getting and setting a value, but they look like regular properties to an external code.

Please note that a property can be either an accessor (has get/set methods) or a data property (has a value), but it cannot be both.
### Data Properties

### Accessor Properties
Accessor properties are represent by **getter** and **setter** methods. In an [[object literal]] they are denoted by **get** and **set**.

![[Pasted image 20231115094552.png]]
The getter works when obj.propName is read, the setter works when it is assigned a value.

![[Pasted image 20231115094913.png]]
From the outside, an accessor property looks like a regular one. That's the idea of accessor properties. We don't *call* user.fullName as a function, we *read* it normally: the getter runs behind the scenes.

As a result of the above code, we have a **"virtual" property** fullName. It is both readable and writable.

#### Accessor Descriptors
Descriptors for accessor properties are different from those for data properties.

For accessor properties, there is no **value** or **writable**, but instead there **get** and **set** functions.

An accessor descriptor may have the following: 
- **get** - a function without arguments, that works when a property is read
- **set** - a function with one argument, that is called when the property is set
- **enumerable** - same as for data properties
- **configurable** - same as for data properties

#### Smarter getters/setters
Getters and setters can be used as wrappers over "real" property values to gain more control over operations with them.

For instance, if we want to forbid short names for `user`, we can have a setter `name` and keep the value in a separate property `_name`, like so:
![[Pasted image 20231115100240.png]]
So, the name is stored in the `_name` property, and the access is done via **getter** and **setter**.

Technically, external code is able to access the name directly by using `user._name`. But there is a widely known convention that properties starting with an underscore `"_"` are internal and should not be touched from outside the object.

#### Using for compatibility
One of the great uses of accessors is that they allow to take control over "regular" data properties at any moment by replacing it with a getter and a setter and tweak its behavior.

Imagine we started implementing user objects using data properties `name` and `age`:
![[Pasted image 20231115101110.png]]
...But sooner or later, things may change. Instead of `age` we may decide to store `birthday`, because it's more precise and convenient:
![[Pasted image 20231115101151.png]]
Now what to do with the old code that still uses `age` property?

We can try to find all such places and fix them, but that takes time and can be hard todo if that code is used by many other people. And besides, `age` is a nice thing to have in `user`, right? Let's keep it.

Adding a **getter** for `age` solves the problem:
![[Pasted image 20231115101359.png]]
Now the old code works too and we've got a nice additional property.