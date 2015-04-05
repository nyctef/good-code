Rather than just being limited to classes, SRP should apply at all levels, up to the repository or even the product itself
(eg the 'unix philosophy' of doing one thing well).

Often, implementing the same idea at two different levels of abstraction should become two separate responsibilities.

When you have an interface, separating out implementations that do error handling, logging and the real work can result in
much simpler code for the 'real work' part, and potentially automated generation of the error/logging code.

Balancing high cohesion and low coupling in classes probably the hardest part of OO design, since the two ideals tend
to conflict with each other in most cases. As responsibilites are spread over more classes, the chance of any particular
change impacting multiple classes significantly increases. Conversely, the easiest way to achieve low coupling is to
put all code into one module.

Generally, prefer small cohesive classes where possible--while you may have to add or change multiple classes, the ease of
changing each class should be small enough that this is not a problem.
