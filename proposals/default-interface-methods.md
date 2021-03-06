# default interface methods

* [x] Proposed
* [ ] Prototype: None
* [ ] Implementation: None
* [ ] Specification: Not Started

## Summary
[summary]: #summary

Add support for _virtual extension methods_ - methods in interfaces with concrete implementations. A class that implements such an interface is required to have a single _most specific_ implementation for the interface method inherited from its base classes or interfaces. Virtual extension methods enable an API author to add methods to an interface in future versions without breaking source or binary compatibility with existing implementations of that interface.

These are similar to Java's ["Default Methods"](http://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html).

(Based on the likely implementation technique) this feature requires corresponding support in the CLI/CLR. Programs that take advantage of this feature cannot run on earlier versions of the platform.

## Motivation
[motivation]: #motivation

Virtual extension methods enable an API author to add methods to an interface in future versions without breaking source or binary compatibility with existing implementations of that interface. It also enables many programming patterns that require multiple inheritance without the issues of multiply inherited state.

## Detailed design
[design]: #detailed-design

(Note that this is merely an *outline* of the specification)

The syntax for an interface is extended to permit
- a method *body* for a method (i.e. a "default" implementation)
- a body for a property accessor
- static methods
- `private` methods (the default access is `public`)
- `override` methods

Methods and accesors with bodies permit the interface to provide a "default" implementation for the method in classes that do not provide an overriding implementation. Auto-properties are not supported in interfaces.

Static and private methods permit useful refactoring and organization of code used to implement the interface's public API.

Override declarations allow the programmer to provide a most specific implementation of a virtual member where the compiler would not otherwise find one. It also allows turning an abstract method in a super-interface into a default method in a derived interface.

The detailed specification will describe the resolution mechanism used at runtime to select the precise method to be invoked.

Some error messages are required on concrete class declarations when the resulting hierarchy does not contain a *most specific* implementation for some interface method. In this case the programmer can resolve the situation by overriding the method explicitly.

## Drawbacks
[drawbacks]: #drawbacks

This proposal requires a coordinated update to the CLR specification (to support concrete methods in interfaces and method resolution). It is therefore fairly "expensive" and is best done in combination with any other features that we also anticipate would require CLR changes.

## Alternatives
[alternatives]: #alternatives

None.

## Unresolved questions
[unresolved]: #unresolved-questions

Many aspects of the design have not been described in detail.

## Design meetings

None.



