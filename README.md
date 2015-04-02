An attempt to figure out what I mean by "good code"

#### The Single Responsibility Principle is king

**High cohesion:** *A module should have one, and only one, reason to change.*

Much of the SOLID principles [actually just follow from SRP](solid-vs-srp.md).

Rather than just being limited to classes, SRP should apply at all levels, up to the repository or even the product itself
(eg the 'unix philosophy' of doing one thing well).

Often, implementing the same idea at two different levels of abstraction should become two separate responsibilities.

When you have an interface, separating out implementations that do error handling, logging and the real work can result in
much simpler code for the 'real work' part, and potentially automated generation of the error/logging code.

**Low coupling:** *A reason to change should affect one, and only one, module*

.. because if a change affects more than one module, those modules are coupled together in spirit, even if not in code.

Balancing high cohesion and low coupling in classes probably the hardest part of OO design, since the two ideals tend
to conflict with each other in most cases. As responsibilites are spread over more classes, the chance of any particular
change impacting multiple classes significantly increases. Conversely, the easiest way to achieve low coupling is to
put all code into one module.

Generally, prefer small cohesive classes where possible--while you may have to add or change multiple classes, the ease of
changing each class should be small enough that this is not a problem.

#### Tests pass in under a second
- massive productivity boost
- confidence
- code at the speed of thought

#### Pure and immutable where possible
- pure functions are very easy to unit-test
- being immutable removes a huge cognitive burden
- Exception: usually the boundaries of a system (UI, DB)
  - OO is good at modelling service abstractions (using state) / UI components (using state+inheritance)

#### Permissive and general rather than defensive and specific
- Defensive coding often just means lots of guard clauses and boilerplate checks
- Finding simple solutions which handle all edge cases is preferable
- Use language constructs where possible to enforce other situations of defensive programming
  - eg use `TaintedString` class intead of adding checks everywhere for bad strings

#### Use inheritance with caution
- Inheritance of behaviour is generally a bad idea
- Inheritance just to share methods is almost always a bad idea
- Inheritance of pure data classes works reasonably well--so long as the domain model fits into the type
system of the language (this is generally only true for simple models)
- Design for inheritance - making small tweaks to behaviour
  - good example: CookieAwareWebClient
  - avoid protected fields
  - use composition+DI instead for larger changes of behaviour

Exceptions: inheritance when required by language/frameworks
- eg sharing NUnit tests

#### Interfaces are hard; implementation is easy
- If you define boundaries correctly, changing individual implementations shouldn't affect system
- usable API vs fastest API
- thinking about API gives clues to implementation
- Test-driven design

#### Plain data objects are fine, even encouraged
- easy to serialize / construct for tests
- extension methods (C#) / immutable helper methods (other languages)
- work very well with pure functions in terms of SRP/test
- best API uses primitives + PDOs
- prefer PDOs for wrapping primitives (where language makes it easy)
