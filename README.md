An attempt to figure out what I mean by "good code"

#### The Single Responsibility Principle is king

**High cohesion:** *A module should have one, and only one, reason to change.*
Much of the SOLID principles [actually just follow from SRP](solid-vs-srp.md).

**Low coupling:** *A reason to change should affect one, and only one, module*
...because if a change affects more than one module, those modules are coupled together in spirit, even if not in code.

**Good architecture:** *Each reason to change should have an obvious place to live.* (?) Not sure about this one, but it 
feels about right

[[More]](srp.md)

#### .. but prefer readability over terseness

It's very attractive to try and be as DRY as possible, but for the long term maintainability is obviously more important. 
Of course, the short *and* readable solutions are the best.

[[More]](readability.md)

#### Tests pass in under a second
- massive productivity boost
- confidence
- code at the speed of thought
- ideally this is all of the tests, but it might be all the *relevant* tests (note this is harder but allows more leeway)
- for simple/hobby projects this might be 'run the program and inspect the output' -- the important part is having a fast
feedback loop that provides confidence in the code.

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
- is this a reformulation of 'worse is better'?

#### Use inheritance with caution
- Inheritance of behaviour is generally a bad idea
- Inheritance just to share methods is almost always a bad idea
- Inheritance of pure data classes works reasonably well--so long as the domain model fits into the type
system of the language (this is generally only true for simple models -- see Eric Lippert's ['Wizards and Warriors'](http://ericlippert.com/2015/04/27/wizards-and-warriors-part-one/) article series for a good example)
- Design for inheritance - making small tweaks to behaviour
  - document how virtual methods are called - especially when one virtual method calls another
  - this often prevents you from changing implementation details in the base class
  - eg https://msdn.microsoft.com/en-us/library/fxzs3wwx(v=vs.110).aspx
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
- tests are more important than code (?)
  - tdd implementation tests vs acceptance tests vs regression tests?
  - test names are more important than tests

#### Plain data objects are fine, even encouraged
- easy to serialize / construct for tests
- extension methods (C#) / immutable helper methods (other languages)
- work very well with pure functions in terms of SRP/test
- best API uses primitives + PDOs
- prefer PDOs for wrapping primitives (where language makes it easy)
- Law of Demeter doesn't apply to PDOs (at least in the simplistic form where you're counting dots)

#### External resources
- [C# Design Strategies (Jon Skeet/Pluralsight)](http://www.pluralsight.com/courses/csharp-design-strategies) A brief but comprehensive overview of what good code looks like and why it matters. Unfortunately not free. Just skip the stuff on various singleton implementations.
- [Boundaries (Gary Bernhardt)](https://www.youtube.com/watch?v=yTkzNHF6rMs) The main place I steal all my ideas from.
