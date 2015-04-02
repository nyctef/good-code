Proposal: the SOLID principles can all be derived from S, or the Single Responsibility Principle.

The **Interface Segregation Principle** is easy: it's pretty much just SRP for interfaces

The **Dependency Inversion Principle** is a bit trickier .. we could just say that 'dependency management' is a separate
responsibility (and a big one--consider how many DI frameworks and IoC container libraries have been written!) but that
is a bit of a copout. 

Instead, let's look at the heart of dependency inversion--that implementations should depend on abstractions, rather than
the other way round. Classes that know about other implementations slowly get poisoned by those implementation details,
and take on additional responsibilities as the set of things that the class knows about grows. Abstractions around
dependencies act as a barrier to this extra information, preventing the class from taking on extra responsibilities.

The **Liskov Substitution Principle** can be shown by counterexample. Imagine that we have implementations of an abstraction
that do not follow LSP. Then, each time that abstraction is consumed by another class, it will have to know about each of the
possible implementations that it might be using. This is obviously an extra responsibility (and a lot of duplicated code!)
that gets added to each consuming class.

The **Open/Closed principle** is [problematic in a lot of ways][skeetocp]. Taken literally, it requires all
methods to be virtual, since they have to be overridden instead of being modified directly. It can be useful to [*measure*
the set of open classes][measureocp] (those changed in a recent period) as a metric for architecture quality, and the OCP
is most useful as a goal rather than an instruction on how to write code.

Given that OCP is implemented by following DIP and LSP, it obviously follows on from the Single Responsibility Principle.


[skeetocp]: http://codeblog.jonskeet.uk/2013/03/15/the-open-closed-principle-in-review/
[measureocp]: http://www.fatvat.co.uk/2014/02/the-first-international-conference-on.html
