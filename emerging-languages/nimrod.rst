Nimrod: A new approach to meta programming
==========================================

:Authors: Andreas Rumpf
:Time: 13:00
:Session: https://thestrangeloop.com/sessions/nimrod-a-new-approach-to-meta-programming
:Link: http://nimrod-code.org/
:Slides:

Agenda: Overview of Nimrod and some implementation aspects, followed by Hello
World and then moving into metaprogramming.

Nimrod is a statically typed systems programming language. It has a
clean syntax and strong meta-programming capability (for example, you
can declare the not equals operator for Nimrod in Nimrod). Nimrod
compiles to C, C++, and Objective-C. Portions of it also compile to
Javascript.

Nimrod provides a realtime GC with exhibits maximum pause times of 1-2
milliseconds. The compiles provides dead code elimination, and the
stdlib is designed to leverage this: for example, if you're using
parsing, it doesn't use regular expressions, so the regular expression
portion is optimized away. (The GC can also be optimized away!)

Example::

  echo "hello ", "world", 99

is rewritten to::

  echo([$"hello ", $"world", $99])

echo is declared as a procedure (function), and ``$`` (the toString
operator) is applied to every argument. This type conversion is local:
only in this context are the arguments converted [not sure what else
could happen?].

Nimrod's focus is meta programming via macros. For example::

  template htmlTag(Tag:expr) {.immediate.} =
    proc tag(): string = "<" & astToStr(tag) & ">"

  htmlTag(br)
  htmlTag(html)

  echo br()
  echo html()

Produces::

  <br>
  <html>

Note that calls to ``htmlTag`` use the parameter name to create a
procedure of the same name.

[Shows additional examples]

Macros can also be used to implement DSLs. [shows example of an HTML
templating DSL; looks pretty slick] Macros support rewriting as well
as simple expansion.

[Additional in depth metaprogramming examples.]

[Shows examples of % and optFormat]

Those look a lot alike, what about reducing duplication using
templates? Yup, Nimrod does that.
