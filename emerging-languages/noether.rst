Noether: Symmetry in Prog Lang Design
=====================================

:Authors: Daira Hopwood
:Time: 11:00 - 11:30
:Session: https://thestrangeloop.com/sessions/noether-symmetry-in-programming-language-design
:Link: https://groups.google.com/forum/?fromgroups#!forum/noether-dev
:Slides:

One of the questions facing language designers is how do we expression
the abstractions necessary to program *gigantic* computers. Thirty
years ago Djkstra warned that as computers increased 1000 fold in
power, they would become too complex to program. In reality, computing
power has increased 1,000,000 fold in that time frame. But the
languages haven't fundamentally changed to address this.

So the "software cirsis" is still here:

Programs are too large, complex, and diffiult to maintain. No one
knows how to write secure, veriably correct programs.

Imposing symmetries aid reasoning abot programming. A suymmetry gives
a set of possible transofmratinos that do not change a given property.
So in geometry, this tanslation is rotation and reflection. In physics
it's time and location invariance (eg, general relativeity). In
programming, language-dependent symmetries exist; for example:

* Confluence describes the symmetry of evaluation order in purely
  functinoal langauges.
* Renaming
* Trait flattening

But programming languages also have features/properties that interfer
with symmetries. For example, side effects and state, failure
handling, and concurrency are essential features that interfer with
adding symmetry. Other non-essential, common features that interfere
include dynamic binding, overloading, implicit coercion, and global
state.

If we want the strongest symmetries possible for any given
expressiveness, the solution is tratified languages. This isn't a new
idea: Erlang, Oz, and Haskell all have it. Noether takes it futher.

At each level we add one or more features nad break a symmetry. Some
symmetries are so useful that they should be preserved globallhy (eg,
memory safety). If you start designing the language with one level per
broken symmetry, then you can collapse levels later if you correct the
brokenness [not sure i got this right]. The sublanguages at each level
don't *need* to be nested, but it simplifies understanding the entire
system.

Noether is an object capability language with strong symmetry
properties. [Slides contain an incredible amount of text; will try to
find, read, and link.]

Noether is actually composed of a set of nested sub-languages, each of
which adds additional funtionality and symmetry.
