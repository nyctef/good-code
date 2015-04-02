An attempt to figure out what I mean by "good code"

#### The Single Responsibility Principle is king

High cohesion: *A module should have one, and only one, reason to change.*

Much of the SOLID principles [actually just follow from SRP](solid-vs-srp.md).

Rather than just being limited to classes, SRP should apply at all levels, up to the repository or even the product itself
(eg the 'unix philosophy' of doing one thing well).

Often, implementing the same idea at two different levels of abstraction should become two separate responsibilities.

When you have an interface, separating out implementations that do error handling, logging and the real work can result in
much simpler code for the 'real work' part, and potentially automated generation of the error/logging code.

Low coupling: *A reason to change should affect one, and only one, module*

.. because if a change affects more than one module, those modules are coupled together in spirit, even if not in code.

Balancing high cohesion and low coupling in classes probably the hardest part of OO design, since the two ideals tend
to conflict with each other in most cases. As responsibilites are spread over more classes, the chance of any particular
change impacting multiple classes significantly increases. Conversely, the easiest way to achieve low coupling is to
put all code into one module.

Generally, prefer small cohesive classes where possible--while you may have to add or change multiple classes, the ease of
changing each class should be small enough that this is not a problem.

#### Tests pass in under a second

#### Pure and immutable where possible

#### Permissive and general rather than defensive and specific

#### Use inheritance with caution

#### Interfaces are hard; implementation is easy

#### Plain data objects are fine, even encouraged
