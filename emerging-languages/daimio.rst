Daimio: a language for sharing
==============================

:Authors: dann toliver
:Time: 9:40 - 10:10
:Session: https://thestrangeloop.com/sessions/daimio-a-language-for-sharing
:Link: http://daimio.org
:Slides:

"Make your applications programmable"

As we increasingly use web applications for everything -- bug
tracking, etc -- it's becoming more obvious when we *don't* use them.
Like code editing, because your editor is probably totally customized
and tricked out. For those of us building web applications, people are
probably using them in ways that you didn't intend. It'd be great if
we could allow our users to extend and customize our applications, and
share that, without exposing ourselves to rampant attack, or
endangering our users.

So what would an appropriate language look like? It'd have editable
interfaces, extensible functionality, and expressible interaction.

When it comes to interfaces, we'll need a templating language that
allows for *some* sort of code embedding (to avoid C-style printf, if
nothing else), some control structures, and most importantly, is *side
effect free*.

We'd need a composition and coordination language, as well -- the
ability to apply primative operations to one another to build up
larger functionality. [Presenter strongly prefers data flow languages
for things like this.] When it comes to coordination, we need
modularity, with some limits on the how entwined and tightly couple
components can become.

So what might it look like if we combined a few of these features,
what might that look like?

Well it's a data flow language, so that means pipes. And it uses a
directed acyclic graph, which means you need a way to do static single
assignment.

::

    { 3 | add 5 } ==> 8

For expressible interactions, we need some coordination language
model. We're interested in building graphical interfaces, so we can
assume that coordination is happening on a single machine, which
removes a bunch of possible problems (network variability, etc).

State is stored in "spaces", and spaces can have subspaces [I think?].
So where does code live in this model, since it co-exists with data?
Code has a thin wrapper called a station, and can be connected to
other spaces.

To avoid side effects, we push all of the I/O to "ports" on the
outermost space.

[Code examples]
