### Inheritance

- Inheritance is a mechanism whereby an object can inherit from another object’s definition, thus gaining the parent object’s data and behavior without you having to define them again.

You choose inheritance for two main reasons.
- One is for reuse of code: you can implement particular behavior for one type, and inheritance enables you to reuse that implementation for a different type.
- The other reason to use inheritance relates to the type system: to enable a child type to be used in the same places as the parent type. This is also called polymorphism

- Inheritance has recently fallen out of favor as a programming design solution in many programming languages because it’s often at risk of sharing more code than necessary. Subclasses shouldn’t always share all characteristics of their parent class but will do so with inheritance. This can make a program’s design less flexible. It also introduces the possibility of calling methods on subclasses that don’t make sense or that cause errors because the methods don’t apply to the subclass. In addition, some languages will only allow a subclass to inherit from one class, further restricting the flexibility of a program’s design.
