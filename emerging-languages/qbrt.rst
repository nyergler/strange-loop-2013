===================================================
 Qbrt Bytecode: Interface Between Code & Execution
===================================================

:Authors: Matthew Graham @lapsu
:Time: 14:45
:Session: https://thestrangeloop.com/sessions/qbrt-bytecode-interface-between-code-and-execution
:Link: http://github.com/mdg/qbrt
:Slides:

Software enginer at Etsy (personal project, not Etsy project).

Bytecode assembly language and virtual machine: make writing langauges
easier, make it possible to recombine quality features, and provide
novel error handling.

Qbrt was sort of an accident. Computers got faster for a long time,
and now they're not getting faster: they getting concurrent. The
programming languages of today were designed for hardware that was
going to keep getting faster.

Speaker invented a language called Jaz, and realized testing and
development would be easier if the language had its own assembly
language. So Qbrt was born.

Qbrt  sits between your language and the OS, much like the JVM. Many
languages could target the same bytecode assembly language, which
could make implementing DSLs, template languages, etc more
straight-forward.

Priorities for the Qbrt VM are concurrency, interoperability, and low
memory footprint. Straight line performance was *not* a priority.

Priorities for the Qbrt language was:

* accessibility
* wriable for a computer
* readable for client language designer
* debugabble in client lange

It does *not* need to be readable or writable by the client language
user. They may know it's there, but they shouldn't need to know about
what's actually going on.

There is precendent for this appraoch: Parrot, JVM, and Erlang runtime
(via Elixer) have gone before.

Qbrt is register based. It supports runtime polymorphism, static type
information, inline async i/o, and pattern matching.

[Hello, world demo, and again in UTF-8]

Concurrency
===========

Qbrt supports concurrency via processes and forks. Qbrt models CPUs as
Workers, which handle scheduling, etc.

Each worker has multiple processes. Qbrt's processes are inspired by
Erlang processes: each has a new call stack, and they communicate via
message passing.

Qbrt forks are a call tree, and communicate via promises. A function
*can not* return until all of its promises are resolved.

Failure
=======

Qbrt handles failure via exceptions or error values.

Exception handling isn't great: if you have an exception handler, it's
not always clear which thing failed, and the result ends up in one of
two places:

::

   try:
       a = foo()
       b = bar()
   except IOError as e:
       # do something

The result of ``foo`` winds up in ``a`` or ``e``. And if ``e`` is set,
which callable did the value originate with?

Error values have their own problems. How many C bugs are the result
of not checking for a negative (error) return value?

Qbrt has static type information; functions declare their type. But in
Qbrt everything can *also* return a failure type. This is implicit,
you do not need to declare it. In the Qbrt code, you can check for
failure using special instructions. *Or* you can ignore it, and Qbrt
will check for you. So if you try to access a value without error
checking, Qbrt will check and throw the error up the stack for you.

Multiple Dispatch
=================

Multi dispatch in Qbrt is more like multi parameter type classes. Qbrt
protocols are similar to Clojure protocols or Haskell classes.

[Presenter went quickly, running out of time.]

What's Next for Qbrt?
=====================

Runtime needs languages to be successful. Write a language :).
